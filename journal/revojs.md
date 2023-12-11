# Revojs: How a Local Conference in 🇷🇴 Romania turned into a Networking Gold Mine

Two large frontend events are happening in Romania each year, and one of them is **revojs** in Timisoara, which I attended for both of their on-site editions, that is October 2019 and October 2023.

## The Talks

Let's jump right in, one by one. Note - my notes are written based on my memory of the presentation. Later I saw they were published on YouTube. Expect discrepencies.

### Tug of War – Pushing and Pulling In JavaScript by Ben Lesh

Ben is best known for his involvement in writing RxJS, but also a dad of three, living in Texas. He touched upon the topic of Signals with a creative approach, the one of data pull and pushing: *"Each line of code either pulls or pushes"*. He surprised us by creating a set of logical operations which represented syntactical transformations of Promises and Observables by the "pull or push"-pattern, which he then applied to model Signals after the same pattern - proving Signals are not, in essence, much more different than Observables.

%[https://www.youtube.com/watch?v=JbL_kqTZAc4] 

### There Is No Such Thing as a 'Generic' by Matt Pocock

Matt is best known for his Typescript course called Total Typescript. *"Generic is overloaded"*: There is no such thing as a *Generic* (noun) because *generic* is an adjective, and it is used in constructs such as "generic functions" or "generic types". While the generic types have at least one parameter (type parameter), generic functions don't require type arguments, because they infer (resolve) the type.

%[https://www.youtube.com/watch?v=le5ciL1T7Hk] 

### Type-Safe Style Systems: The Future of CSS by Josh Goldberg, selected from ✍️ CFP

CART: Convenient. Assistable. Refactorable. Themeable. (Performant).  
We were presented with possible futures of CSS - circling around CSS modularizations, "themeable-ities" and developer experience while writing and organizing styles. I see I jotted down "@vanilla-extract/" and chackra-ui. Oh, and "squiglies".  
Josh couldn't find his favourite button-down shirt because his luggage chose a different flight. Luckily he got that back for the next day, and he was the one to volunteer (I presume) for a second talk standing in for a speaker that couldn't make it to the conference anymore.

%[https://www.youtube.com/watch?v=XMn9JnPH9ic] 

### New CSS Features You Can Use Today by Rachel Andrew

Rachel is Content Lead for Chrome DevRel at Google, and yeah, you could tell she's a professional tech writer; I'm just reading on her website that she has authored or co-authored more than 20 books! I love how articulate she is, providing all the right info for the right purpose on her website.  
But now back to her presentation. We got a primer on CSS latest standards adopted or soon to be adopted by browsers: sizing units based on viewport sizes (svw/svh, lvw/lvh, dvw/dvh), :focus-visible ("*browser: 'is focus ring required?'"*), Cascade Layers, @layer framework, layout, utilities, container queries, range operator for media queries, "High Definition CSS Color Guide", color-mix, gradient.style, :not(:has(img)), @property (type, initial - fallback), Web Platform Baseline.  
Never have I thought I'd write down so many notes on a CSS presentation.

%[https://www.youtube.com/watch?v=dUz72A96qqg] 

### Understanding Rendering Patterns by Atila Fassina, selected from ✍️ CFP

Atila learns Rust, was born in Brazil and lives in Berlin. This talk was a walkthrough on rendering patterns - including a live demo sampling a performance optimization in reactivity based on signals (hope I don't mix up). My doodles:  
*Abstract the DOM -&gt; batch changes -&gt; Reconcile*  
*prop drilling*  
*"tide" vs "wave" - the tide raises everyone, as opposed to the wave that only raises a subset*

%[https://www.youtube.com/watch?v=ATXgJR1H7Cs] 

### Demystifying Web Performance Tooling by Anna Migas

When you think you saw and read everything you could on web performance, then there's this presentation that can very well serve as a performance audit starting point. My doodles:

1. *Load web performance*
    
2. *Runtime web performance - jank, code splitting, animation optimization*
    
3. *Perceived web performance - Laboratory Data versus Field Data*
    

*PageSpeed Insights, Webpack, Web Vitals extension, devTools: Network, Performance, Lighthouse.  
Lighthouse: paint flashes, Layout Borders, Rendering tab -&gt; use a different Chrome Profile  
Network tab: Priority column*  
*Time to first byte (waiting for the server to respond). SpeedCurve, Calibre*

%[https://www.youtube.com/watch?v=X3PKBYmbTkU] 

### No-BS SEO for web developers by Martin Splitt

Martin put on a show. He made up (I think?) a website trying to sell toasters, in two flavours: the no-go one, and the SEO optimized. We had a good laugh since the *joke* was the brutal truth for many online businesses.  
I appreciate how Martin creates his GIF-s out of his personal video content - and avoids any comments on licensing - I do the same Martin, with my image content. My doodles:  
*content, strategy, technology  
"protoduction", "build an aeroplane while in flight"  
a fly on the wall of a company  
efficient & no sense of humour* (loved this joke - how many Germans do you need to change a💡? One. Because..)*  
evergreen, GoogleBot, crawl budget*

%[https://www.youtube.com/watch?v=xgyvh9TOdYM] 

### Security by(e) Design? by Benedek Gagyi, selected from ✍️ CFP

This talk draws attention to balancing web security and UX decisions. My doodles:  
*tea brewing, gongfu  
Devs &lt;-&gt; UX &lt;-&gt; Security  
Credentials API, Web OTP API, WebAuthn -&gt; Passkeys*

%[https://www.youtube.com/watch?v=O8LPgLTxKxk] 

### You Could Lint More by Josh Goldberg

Josh, previously selected through CFP, stepped in to hold this second talk as a replacement for a speaker on the agenda who couldn't make it to Timisoara because of personal reasons. The title is spot-on: indeed, es-lint is a gold mine for teams. My doodles:  
`--max-warnings` *- create a gate of a maximum number of warnings allowed in the CI pipeline. eslint-plugin-deprecated, eslint-comments, eslint-plugin-jsdoc, eslint-plugin-markdown, eslint-plugin-perfectionist, eslint-plugin-regexp regexp create-typescript-app, warp - terminal, vitest, pnpm*

%[https://www.youtube.com/watch?v=voYSdj3Xqvc] 

### The Ethical Choice by Alex Moldovan, selected from ✍️ CFP

This goes beyond accessibility or UX: what choice does it *feel* to be good or bad for the interest of the user when designing web experiences? We all know the annoying tiny "unsubscribe" links lacking contrast. Or the "opt-in" default selection. Yeap, those. I'm happy somebody framed this topic in a talk.

%[https://www.youtube.com/watch?v=qGjJ6-xNfM0] 

### Have You Heard the Joke About Async Debugging? I Promise It Is Good. by Jay Phelps

Async issues are the worst! Not to brag, but I spotted the one in the talk on time. Jay was top of the game on teaching - he led you in solving the mysterious bug by yourself. I can't wait to show this talk to my team. My doodles:  
*"input" event - including Paste*  
*request coming back out of order*  
*typescript-eslint/return-await: "error"*

%[https://www.youtube.com/watch?v=YOxgYrS4d8E] 

### Breaking Down JavaScript Complexities With Generative Art by Ritvi Mishra, selected from ✍️ CFP

How many of you are visual learners? Ritvi showed us how one can learn Javascript as their first programming language by coding visualisations: such as visually describing the steps in repetitive structures or the call stack.

%[https://www.youtube.com/watch?v=MQ1slSVl2tE] 

### Node.js in 2023 – What’s New in the Node.js Native Test Runner by Erick Wendel, selected from ✍️ CFP

I have to admit that this talk stretched my Javascript knowledge and attention. Erick is a high performing professional, contributing to nodejs's native test runner. Kudos for an enjoyable in-depth walk-through of such a difficult topic. My doodles:  
*v-test*  
*TAP - protocol*  
*dot; spec; junit; lcov*  
*test sharding & concurrency*  
*why-is-node-running*

%[https://www.youtube.com/watch?v=q3OQz5E1OpI] 

### Testing Your Testing Strategy by Trent Willis

I empathised a lot with this topic: what types of testing and how much testing do you need? How do you know "*you're good*" or "*yikes, too many tests to maintain, are they really paying off..*"? My doodles:  
*The value of testing is in quality, not in quantity*  
*Optimize invested time versus confidence. The trouble is - confidence can't be quantified  
*[*noti.st/trentmwillis*](http://noti.st/trentmwillis)

%[https://www.youtube.com/watch?v=kEkMqppoyHA] 

### Requiem for APIs – The Evolution of Web Development by Ciprian Caba

Ciprian created a sort of "time-lapse" for web development, showing us how the data rendering into the presentation layer has circled back from server to client to server, and pointing out API-s can get obsolete, once we use the full abilities of the new frameworks that can simply access the data model directly, on the server side.

%[https://www.youtube.com/watch?v=bmtW_IT63P4] 

### Beyond the Web of Today by Kenneth Rohde Christiansen

I had no idea about all the work involved to better support high-level API-s from the producers of hardware processing units. We're talking hardware that can speed up software related to (but not limited to) computer vision: blurring background, virtual background, eye-following, real-time visual filters, as well as anything that involves tensor calculus & whatnot. A hard subject. My dribbles:  
*Project Fugu*  
*Web Codecs*  
*WebGPU, NPU / TPU, Web Neural Network API (Web NN)*  
*ONNXM, MediaPipe, OpenCV.js*

%[https://www.youtube.com/watch?v=Vx-dlSUx18Y] 

## The Vibes

I can't thank the community of professionals in Timisoara enough for making **revojs** happen. I know it isn't easy. It takes time, energy, commitment, lots of helping hands, and sponsors (and trust me they do need a lot of sponsorships for such a scale of an event). The thing is - their commitment and their helping hands are something money can't buy for a conference to take place - and that's what makes revojs so special.

%[https://twitter.com/revojsro/status/1714239446269280344] 

Most of the participants are part of the local community. Both of the times I travelled by myself to the conference and made friends on the spot. This time, however, I couldn't see anyone familiar at the after-beer outdoorsy party, and I was fortunate enough to bump into Jay while ordering drinks and, long story short, I ended up having a great time drinking and chatting with all the speakers at the party, for hours. I even realised I had been walking very close to Matt's home address in Oxford when attending RenderConf 2016. Such a small world, isn't it?

Who would have imagined I would one day have a drink with Matt and talk about that conference in his hometown? Can't wait to see what the next revojs has in store.

%[https://twitter.com/erickwendel_/status/1710364519208251625]
