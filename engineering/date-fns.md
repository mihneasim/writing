# I once tried not to use date-fns

In one of my team's Pull Requests I noticed date-fns being added as dependency for our components library for one usage: transform a timestamp to "MM/yy" string, as it represented a debit card's expiration date.
Inspired by [You don't (may not) need lodash/underscore](https://github.com/you-dont-need/You-Dont-Need-Lodash-Underscore), I thought to myself - can't we just implement a 2-digit month and 2-digit year formatting? It looks simple, right?

Inspecting native Date's [documentation](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Date), we have `getMonth` - returns 0-indexed integer representing the month of the year. First gotcha here, you have to increment value for human-readable month. As for the year, we have `getFullYear`, which is pretty self explanatory.

Let us write a function - not necessarily for reusing it, but more so we can easily test it. And let's write the dumbest one, and improve it test by test ;)

```javascript
function expiration(date) {
  return `${date.getMonth() + 1}/${date.getFullYear() % 100}`;
}
```

that would work wonderfully for something like

```javascript
it('should return 11/22 for nov 2022 expiration', () => {
  expect(expiration(new Date(2022, 10)).toEqual('11/22');
});
```

but would of course fail for one-digit months

```javascript
it('should return 03/23 for March 2022 expiration', () => {
  expect(expiration(new Date(2023, 2)).toEqual('03/23');
});

// Expected "3/23" to equal "03/23"
```

We can address that by a fun trick: simply pad a heading `0` whatever the result is, and then retain the last two chars, using negative argument for `substr`

```javascript
function expiration(date) {
  return `0${date.getMonth() + 1}`.substr(-2) + 
         `/${date.getFullYear() % 100}`;
}
```

Seems finished? What's missing?
.
.
.
.
.
.
.
.
.
.
.
.
.
.
You got it. What if the remainder in date.getFullYear() % 100 is one digit?

```javascript
it('should return 03/00 for March 2100 expiration', () => {
  expect(expiration(new Date(2100, 2)).toEqual('03/00');
});

// Expected "03/0" to equal "03/00"
```

which leads us to 

```javascript
function expiration(date) {
  return `0${date.getMonth() + 1}`.substr(-2) +
         "/" +
         `0${date.getFullYear() % 100}`.substr(-2);
}
```


Phew! Now the only thing left to figure out: What is 00? 2000 or 2100?

How far have you gone implementing features that are available in libs like `date-fns`, `lodash`?
Is it worth the hassle (and the risks!) considering tree shaking* is doing a neat job in packaging optimal production JavaScript?

Last and not least, let me know if you'd write it differently. Have I missed a corner case? Hope you enjoyed my test-driven approach, although it's closer to a "test-before" rather than a "test-driven-development". 

*provided you are using modularization of both your code and your dependencies (i.e. using es-modules or other implementations), and that the bundler is capable of exploiting the modularization in order to trim unused code
