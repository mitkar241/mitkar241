# Code Coverage
---
## What is Code Coverage?
---
Code Coverage quantitatively measures how comprehensive a code base's tests are. Increasing code coverage often increases stability and reduces bugs.

Let's say you're taking over an existing code base. It's relatively large, at 100,000 lines of code. Over the years it's been adopted by hundreds of users, and you're expected to maintain it and add features to it without harming existing users.

The first place you look is at the unit tests - but they were never prioritized by the previous maintainers. A mismatch of libraries and naming conventions make it hard to tell which components of the application are well tested.

Before you write any new features, you'd like an objective way to measure how well things are tested. That way you can know which components need more care when being changed, and which are reasonably thoroughly tested already.

This is where code coverage really shines: You've got a complicated codebase that has existing users, and you'd like to write missing tests before accidentally breaking things.

## A simple example
---
Let's say you're writing a JavaScript program:
```
1. let f = n => {
2.   let x = "hello", result = [];
3.   for(let i = 0; i < n; i++) {
4.     result.push(x+i);
5.     if(i%50 == 49) {
6.       result.push("50th: "+x+i);
7.     }
8.   }
9.   return result;
10.}
```
To understand code coverage, it's useful to think about types of lines:

- Syntax lines are those which don't do anything and can't contain bugs - 1, 7, 8, and 10.
- Logic lines are those which contain actual code statements - 2, 4, 6, 9
- Branch lines are those which change what is executing - things like function calls, if statements, and loops - 3, 5

Code coverage for this program would be the ratio of non-syntax lines which are executed by tests over the total number of non-syntax lines.

Consider this test:
```
it("should work for two", () => {
  let expected = ["hello0", "hello1"];
  assertEquals(f(2), expected);
});
```
If this was the only test of the function above, our effective code coverage would be non-syntax lines executed over total non-syntax lines, so:

Since our condition on line 5 only executes for inputs greater than 49, line 6 is never executed by our test case. There are six lines of actual code in the function, so 5/6 = 83% test coverage.

## Branch Coverage
---
A very relevant concept to code coverage is "branch coverage" - instead of measuring how many lines of code, it measures groups of lines.

In our example above, there are two branches: lines 4-7 (the body of the for loop) only execute if n >= 1, and line 6 only executes if n >= 49.

Instead of looking at individual lines of code, we could instead look at branches: The body of the for loop, the body of the "if" statement, and the body of the main function.

Measuring branch coverage, our test above would score 2/3 or 66%, as two of the three branches are covered by tests.

Branch coverage is generally reported alongside line coverage. They are both code coverage measurements, and generally convey the same information.

## When to care about code coverage

We've already discussed one scenario when code coverage is important: When you've inherited an existing code base. However, code coverage is useful in many different situations.

In general, you should measure and optimize for code coverage if any of the following are true:

- Your product has users, and those users might leave if they are affected by bugs.
- You are working with developers that aren't immediately trustworthy like contractors or interns.
- You are working on a very large code base with many individually testable components - here code coverage analysis can compliment Test Driven Development as a project management tool.

A common mistake in code review automation is to make things too rigid before a product has users. If you force developers to write 2-5 unit tests for every new feature in order to maintain 100% code coverage, they will spend longer writing more code.

By writing tests, developers are solidifying the implementations of features that might be thrown out in response to user feedback. It's always easier to throw out and dramatically change features before they are tested.

## Common policies related to code coverage
---
Code coverage is useful as a metric,  but it's especially useful if combined with policies and automation as a check that code will not cause bugs for end users.

## Code coverage must not decrease
---
This is one of the easiest policies to automate - it's especially useful if you are taking over an existing under-tested code base.

The idea is that the code coverage ratio must never decrease - if the current code has 75% code coverage, and your new change introduces 40 lines of code, at least 30 of those must be tested. Otherwise, your change's code coverage would be <75% and so you'd be decreasing the average.

As with most code coverage policies - this will increase stability at the expense of speed.

An unfortunate side effect is that changes which would be harder to test (such as integrations) will be less likely to be worked on by developers, as those changes will require a lot more testing infrastructure to keep the code coverage numbers up.

## Code owners for test files
---
If you've used code coverage automation to keep code well tested, it is often beneficial to define "code owners" for the tests themselves. This means that developers can change implementation details without formal reviewers, but logic changes would need to be approved by a senior developer or manager.

For example, in a small team with an engineering manager, a GitHub CODEOWNERS file might contain:
```
*.spec.js @engineering-manager-username
```

## Conclusion
---
If you are working in a large codebase with Test Driven Development, hiring interns or contractors, or have users sensitive to bugs, it might be in your team's best interest to install a code coverage measurement tool.

Some popular choices include:

- https://codecov.io
- https://coveralls.io/
- https://codeclimate.com/
