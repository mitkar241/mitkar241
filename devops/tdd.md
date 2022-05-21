# Test Driven Development
---
## What is Test Driven Development?
---
Test driven development is a coding methodology where tests are written before the code is written.
Test Driven Development has been around for a long time: Kent Beck popularized it in the early 2000s with Test Driven Development: By Example. The idea is simple, but requires knowledge of how software testing usually works.

## Software testing
---
Common words in software development such as "quality assurance" and "unit test" have roots in factories building physical products.
If you were running a factory building coffee makers, you would test that it worked at varying levels of completion:

- Unit tests: Ensure individual components work on their own. Does the heater work? Does the tank hold water?
- Integration tests: Ensure a few components work together. Does the heater heat the water in the tank?
- System (end-to-end) tests: Ensure everything works together. Does the coffee maker brew a cup of coffee?
- Acceptance tests: After being launched (sent to consumers), are they satisfied with the result? Are they confused with the button layout or breaking their coffee maker within the warranty period?

All of these tests have software analogues - it's useful to know which component broke in order to diagnose a problem, but it's also useful to know that the whole system is working correctly.

## TDD: Before and after
---
Most developers that aren't using test driven development have a similar workflow:

- Choose something to work on (the specification is usually written somewhere by someone in the product team)
- Build it (ensuring that the thing built satisfies the specifications)
- Test it (write small scripts that ensure that the thing which was built does not break in the future)

Steps 1 and 3 are very connected. The tests written at the end essentially codify the specification. What is success for building a coffee maker? It should heat up in 5 seconds, so write a test for that. It should brew coffee of sufficient strength, so test for that, etc.

Test driven development uses the similarity of steps 1 & 3 to flip this process on its head:

- Choose something to work on.
- Write tests that would pass if the software actually worked.
- Keep building until all of the tests pass.

Here, the end result is the same (the software is built and tested), but all of the specifications can be clarified as the tests are being written. Test Driven Development ensures that the software created always fulfills its specification.

## Conclusion
---
Test Driven Development is an alternative way of writing well tested software. It uses tests as a way of building a specification for how things should work before a single line of code is written.
