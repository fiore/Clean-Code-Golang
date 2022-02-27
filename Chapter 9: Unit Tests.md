# Chapter 9: Unit Tests

## The Three Laws of TDD

TDD asks us to write unit tests first, before we write production code. Consider the following three laws:
- **First Law**: You may not write production code until you have written a failing unit test.
- **Second Law**: You may not write more of a unit test than is sufficient to fail, and not compiling is failing.
- **Third Law**: You may not write more production code than is sufficient to pass the currently failing test. 

## Keeping Tests Clean

Having dirty tests is equivalent to, if not worse than, having no tests. The tests must change as the production code evolves.
The dirtier the tests, the harder they are to change.

Without a test suite they could not ensure that changes to one part of their system did not break other parts of their system.

Test code is just as important as production code. It requires thought, design, and care. It must be kept as clean
as production code.

## Tests Enable the -ilities

If you have tests, you do not fear making changes to the code! Without tests every change is a possible bug.
Without tests you will be reluctant to make changes because of the fear that you will introduce undetected bugs.

The higher your test coverage, the less your fear. Indeed, you can improve that architecture and design without fear!
So having an automated suite of unit tests that cover the production code is the key to keeping your design and architecture as clean as possible, because tests enable change.

## Clean Tests

What makes a clean test? Readability.

BUILD-OPERATE-CHECK pattern: first, builds up the test data, second, operates on that test data, and third, checks that the operation yielded the expected results.

Test doesn't need be as efficient as production code. After all, it runs in a test environment, not a production environment, and those two environment have very different needs.
There are things that you might never do in a production environment that are perfectly fine in a test environment. Usually they involve issues of memory or CPU efficiency. But they never involve issues of cleanliness. 

## One Assert per Test

Use the common **Given-When-Then** convention for the names of the functions. This makes the tests even easier to read.
To avoid the code duplication, use the TEMPLATE METHOD pattern and putting the **Given/When** parts in the base class or in the @Before function, and the **Then** parts in different derivatives. 

The test should be split up into three independent tests because it tests three independent things.
Minimize the number of asserts per concept and test just one concept per test function.

## F.I.R.S.T.

- **Fast** Tests should be fast. They should run quickly. When tests run slow, you won't want to run them frequently. If you don't run them frequently, you won't find problems early enough to fix them easily. You won't feel as free to clean up the code. Eventually the code will begin to rot.

- **Independent** Tests should not depend on each other. One test should not set up the conditions for the next test. You should be able to run each test independently and run the tests in any order you like. When tests depend on each other, then the first one to fail causes a cascade of downstream failures, making diagnosis difficult and hiding downstream defects.

- **Repeatable** Tests should be repeatable in any environment. If your tests aren't repeatable in any environment, then you'll always have an excuse for why they fail. You'll also find yourself unable to run the tests when the environment isn't available.

- **Self-Validating** The tests should have a boolean output. Either they pass or fail. You should not have to read through a log file to tell whether the tests pass. 

- **Timely** The tests need to be written in a timely fashion. Unit tests should be written just before the production code that makes them pass. If you write tests after the production code, you may decide that some production code is too hard to test. You may not design the production code to be testable.
