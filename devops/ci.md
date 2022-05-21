# Continuous Integration
---
## What is CI?
---
Continuous Integration (CI) refers to developers continuously pushing small changes to a central Git repository numerous times per day. These changes are verified by automated software that runs comprehensive tests and ensures that no major issues are ever seen by customers.

Continuous Integration (CI) refers to developers continuously pushing small changes to a central Git repository numerous times per day. These changes are verified by automated software that runs comprehensive tests and ensures that no major issues are ever seen by customers.

## First, what are tests?
---
CI is usually defined in terms of tests. If a developer added a feature which let users enter their credit card information, they would push:

- The code for the feature itself
- Little scripts called "tests" that made sure that the code was working properly.

There are many types of tests, you can read more about them in our article on Test Driven Development.

## Why should I use CI?
---
CI is the first step to understanding DevOps. Imagine the simplest possible scenario: A single developer is working on a program that will be used by a small number of users. That developer makes the original program, releases it, and the project slowly builds traction.

Now, imagine that the developer has a critical bug found a year after they've last worked on the project. The developer goes back to work on the old code and says, "Gee, this is bad code - what was I thinking? I don't understand what's going on here."

This is how development works - developers get better year after year, and need to read and understand "bad code" that might only be a year old. The only way to be confident making changes to such code is to have a test suite that ensures that new changes do not break existing functionality, and the easiest way to run these tests is via CI.

CI improves developer speed because new changes can be made confidently without having to worry about breaking existing code if the tests pass.

CI also reduces customer churn and improves user satisfaction because problems with the software are unlikely to be merged into the codebase - If the CI test runner deems there to be a bug, that change is not allowed to be pushed to users.

## How do I integrate CI into my development process?

The most common approach to development at software development companies is a four-step approach that includes CI:

- Developers work on a feature branch and push at least a commit a day to that branch on a central git repository.
- After every commit to the feature branch, a CI server picks up the commits from the repository and runs tests, reporting any errors back to the developers of the code.
- Once the feature is complete, the developers open a "pull request" (github) or "merge request" (gitlab) to have their changes be merged into the "master" branch. Another developer on the same team makes sure that the feature makes sense, and that there are no stylistic issues in a "code review."
- At some point, the "master" branch gets "prod pushed" (pushed to production) so that end users see the code. This might happen automatically in CD (continuous deployment) scenarios, but is often triggered manually for smaller projects.

In the scenario above, there are two "branches" being worked on by separate developers. The "master branch" has been changing the website, and includes changes that add terms of service and privacy policy. The "feature branch" has been adding a new feature to the mobile app.

If there was a "prod push" at this point, the feature would not be shown to the users. Only the last commit on the master branch is ever sent to users after a prod push.

It's necessary for the developers of the feature branch to "merge" their changes into the master branch before they will be visible to users. That's where a solution like webapp.io can ensure that the newly added feature does not break existing functionality.

## Does this process cost me anything?
---
Central git repositories like GitHub, Gitlab and BitBucket all have generous free tiers that don't need a developer's attention to set up.

CI providers like webapp.io also have generous free tiers - webapp.io integrates effortlessly with GitHub. All you have to do is authenticate it with your repositories, then ensure that tests are set up by anyone making new features.

## Conclusion
---
CI is a vital tool for teams with any developers on them. It ensures that features written by another developer, or a long time ago continue to work as new changes are made. Following best practices and using Git and CI ensures that features aren't broken accidentally, which greatly reduces customer churn and improves user satisfaction.
