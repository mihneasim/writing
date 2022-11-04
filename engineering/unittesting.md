As a Chapter Lead, the most frequently requested training by latest joiners, is by far the one on Unit Testing. While we are performing good on testing coverage, I usually have to focus on how the unit tests are written during code review — pointing me the fact that the quality of unit testing is slightly neglected, to say the least. I'm taking advantage of this space to help improve that with a strong introduction into testing.


###The big picture of testing


###Unittests: when to write them

Test after
Test before
Test Driven

###Key principles

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


