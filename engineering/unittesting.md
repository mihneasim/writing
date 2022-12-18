As a Chapter Lead, the most frequently requested training by latest joiners, is by far the one on Unit Testing. While we are performing good on testing coverage, I usually have to focus on how the unit tests are written during code review — pointing me the fact that the quality of unit testing is slightly neglected, to say the least. Or as Theo put it, 100% coverage is actually bad, and a lot of poor written tests are worse than no tests at all, putting unnecessary work load on the team, instead of helping the team.

I'm taking advantage of this space to help improve that with a strong introduction into testing.

###The big picture of testing
You'll definitely hear about "The Pyramid of Testing". Nothing sacred here, and no, I am not going to include the scheme here, it's already in too many Powerpoint presentations. I'll just sum it up: Engineers saw different important layers of granularity in a software product, that deserve their own matching testing strategy. I'd call the "zoom levels": unit, component, system, product. Naming and layers may vary, but in essence, testing strategies start from unit tests (the smallest testable piece of code) up to functional, integration, system and the great "end to end"; which is supposed to test the product as if it were operated by the actual end user. We are only going to focus here on the most granular and small of them all - **the unit tests**.

###So, what is a unit?

Let me get very naive here: we're testing functions. Units are functions.

"Yes, but..". Yes, I'm shallow. There's a lot more to it, than just functions. We're testing the smallest representations of logic in whatever realm we're practicing our engineering. If you're writing unit tests for hardware models, your units may be gates or other logical circuits decomposed to smaller testable units.

In fact, a unit can be part of smaller units - units which we need to either test individually, or assume they work flawlessly. I.e. if your method uses `fetch`, you have to assume `fetch` works and performs as guaranteed by the browser. You don't need to test `fetch`. If you import lodash and use lodash.omit, expect `omit` to do what it says in its docs.

###Unittests: when to write them

No, it's not a question of morning or evening, Monday or Wednesday, it's about when to write them in comparison to the piece of code that is being tested. There are three aproaches.

1. Write the tests after you're done with the implementation. Still better than nothing, but you might need to amend the implementation once the tests reveal flaws.
1. Write the test before you start the implementation. Tests serve as a contract for what you, as developer, expect from your unit.
1. Test driven development, described by cycles as short as possible, each composed of:
   * one short "test before"
   * implementation (as minimum as possible, just to make the test pass)
   * followed up by a refactor where possible.
If TDD was initially seen as high quality development, requiring great mastery in both testing and development, today more and more engineers believe TDD is a mistake, arguing that the development is centered around testing, hurting the outcome for the maintainers and the consumers.

I'd say each of the strategy has its own place, and it's worth a separate discussion when to use which.

###Vocabulary

testing harness:
collecting (discover) tests
run them
assertion library
collection of results

Do not repeat the implementation
Don't be scared to hardcode values
If some problem seems to have a large audience, odds are there's an easier way to do it, built in the framework

###Anatomy of a test

Arrange
Act
Assert

Arrange - it's almost always the hardest part.

Pure functions
Impure - side effects
Challenges: Reachability

