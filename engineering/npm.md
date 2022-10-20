Long long time ago, when I used to do Rapid App Development using Python, my
package manager of choice was [pip]. And one feature I very much liked was being
able to output all the names and versions of the dependencies available in the environment,
one per line. You could simply redirect that output to a text file, add it to
the VCS, and later use that file to install the same version set.

```console
$ pip freeze > requirements.txt
$ cat requirements.txt
pytest==3.3.2
requests==2.18.4
requests-mock==1.4.0
```

It sounds simple enough, and it really was that simple, especially when combined with virtualenv.
But let's talk about JavaScript's infamous `npm`, self-titled on Twitter "The package
manager for JavaScript". Pip's _requirements.txt_ is equivalent to npm's _package.json_ and
there is no need for an npm _freeze_ command. `npm` will create and update it
for you every time you use it to manage requirements.

However, the actual "freeze" of a pip project is rather the equivalent of
_package-lock.json_, which contains the full list and metadata of the exact
version set in use. Apart from that, there is a command one
can use to inspect the versions of the installed packages and their relation -
`npm list`. Be advised that the behaviour of `npm list` changed in npm
version 7 (bundled with nodejs v15).

I stumbled upon the change myself, and I had to convince myself something indeed
had changed. The output was a flat list of deps, instead of the fluffy tree structure
I used to know. Running multiple versions of npm/nodejs is easy using
[nvm]. This way, I couldn't resist not showcasing this change to my own eyes.

```console
$ nvm install 14
$ nvm use 14
Now using node v14.17.4 (npm v6.14.14)
$ npm help list
...
   Description
       This command will print to stdout all the versions of packages that are installed, as well as their
       dependencies, in a tree-structure.
...

$ nvm install 15
$ nvm use 15
Now using node v15.14.0 (npm v7.7.6)
$ npm help list
...
   Description
       This command will print to stdout all the versions of packages that are installed, as well as their
       dependencies when --all is specified, in a tree structure.
...
       Also, in the years since npm got an ls command (in version 0.0.2!), dependency graphs have gotten
       much larger as a general rule.  Therefore, in order to avoid dumping an excessive amount of content
       to the terminal, npm ls now only shows the top level dependencies, unless --all is provided.
...
```

A-ha! So `npm list` in npm version <= 6 is `npm list --all` in npm version 7 or
higher; which is of course stated in their [v7 Changelog][1] - but looking up changelogs is way too
mainstream.

> npm ls
>
> Extraneous dependencies are listed based on their location in the node_modules tree.
>
> npm ls only prints the first level of dependencies by default. You can make it
> print more of the tree by using --depth=<n> to set a specific depth,
> or --all to print all of them.

### npm explain

Since the installed packages follow a tree-like structure, based on _dependency
transitivity_, i.e. A needs B, B needs C, so installing A, installs C, one might
fall into the trap of importing directly from C.

[ESLint] was not shy enough not to complain:

> 2:1 error 'stringify-object' should be listed in the project's dependencies.
> Run 'npm i -S stringify-object' to add it import/no-extraneous-dependencies

where line 2 was:

> import stringifyObject from 'stringify-object';

Fear not. This is where `npm explain` comes into play.

> This command will print the chain of dependencies causing a given package to
> be installed in the current project.

```console
$ npm explain stringify-object
stringify-object@3.3.0 dev
node_modules/stringify-object
  stringify-object@"^3.3.0" from lint-staged@10.5.4
  node_modules/lint-staged
    dev lint-staged@"^10.5.4" from the root project
  stringify-object@"^3.3.0" from workbox-build@6.5.4
  node_modules/workbox-build
    workbox-build@"^6.2.4" from rollup-plugin-workbox@6.2.0
    node_modules/rollup-plugin-workbox
      dev rollup-plugin-workbox@"^6.2.0" from the root project
      rollup-plugin-workbox@"^6.0.0" from @open-wc/building-rollup@2.0.2
      node_modules/@open-wc/building-rollup
        dev @open-wc/building-rollup@"^2.0.1" from the root project
```

But then, I thought - didn't `npm list` also have positional arguments -
accepting specific package names as input? Let's try that

```console
$  npm list stringify-object                                                      1 ↵
node-play@0.0.0 /Users/mihnea/code/node-play
├─┬ lint-staged@10.5.4
│ └── stringify-object@3.3.0
└─┬ rollup-plugin-workbox@6.2.0
  └─┬ workbox-build@6.5.4
    └── stringify-object@3.3.0 deduped
```

Gorgeous. `npm list` is indeed capable of focusing on one _leaf_ in the deps tree.

In closing, _package.json_ and _node_modules_ are one of the regrets
of nodejs creator Ryan Dahl, as beautifully and wholeheartedly stated in [JSConf 2018][2].
Luckily, having the proper knowledge on the npm tooling at hand, we can make
npm work for us, rather than against us.

[pip]: https://pip.pypa.io/en/stable/
[nvm]: https://github.com/nvm-sh/nvm
[1]: https://github.com/npm/cli/blob/v7.0.0/CHANGELOG.md#npm-ls
[2]: https://www.youtube.com/watch?v=M3BM9TB-8yA&t=591s
[eslint]: https://eslint.org/
