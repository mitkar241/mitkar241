# Linting
---
## Linting best practices
---
Linters are programs that look at a program's source code and find problems automatically. They are a common feature of pull request automation because they ensure that "obvious" bugs do not make it to production.

## An example of linting
---
Consider this JavaScript program:
```
var x = "5";
function f(elements) {console.log(elements)
let x = 0;
while(x < 100) {
  console.log(x)}
}
```
Without even running this program, an experienced JavaScript reviewer would be able to give several points of immediate feedback:

- Avoid mixing "var" and "let" (the latter has less surprises than the former)
- Inconsistent whitespace (on line 2, for example)
- The while loop cannot terminate (x is not incremented)
- The variable "x" is redeclared (shadowed) inside the function
- There are missing semicolons on several lines (which can cause strange side effects in javascript)
- The names "x" and "f" are not very descriptive (in a most codebases, it's very often net-negative to have single letter function names)

Notice that much of this feedback can be automated - a set of rules like "use let instead of var" could be applied to each proposed change automatically, so that human reviewers would not have to waste effort leaving code style comments. Tools that maintain and run such rules are called "linters."

## Style guides
---
Another class of code review feedback has to do with code style. It's easy for code reviewers to waste time pointing out stylistic choices like "tabs or spaces" or "camelCase vs pothole_case." These discussions bring no value to end users, and ultimately serve only to cause resentment and missed deadlines within engineering teams.

Engineering organizations should eventually adopt and maintain a Style Guide - in most cases, adopting the [Google Style Guide](https://google.github.io/styleguide/) wholesale is a good starting point. These guides often come with linter configurations which keep everything stylistically similar.

## The "nit" approach
---
Instead of blocking features on stylistic differences, it's better for code reviewers to leave small code review comments called "nits" which can be ignored for the purpose of the broader review. Things like variable naming should generally not block a change from being merged, but would still be pointed out as "nits" for future reference.

## Auto formatting
---
Once a style guide is adopted, it is possible to configure tools to automatically format code to follow that style guide. Such tools are called autoformatters. In the programming language Go, a command such as the following would use the standard formatter to clean up all of the source files in the repository automatically:
```
find . -name '.go' -not -path "/vendor/*" -exec gofmt -s -w {} ;
```
With the gofmt command above, developers could be asked to format their code before opening a pull request.

## Linting automatically in CI
---
Programmers shouldn't have to wait for a human reviewer to tell them whether their code is linted and styled appropriately. In most cases, it's cheap and convenient to run linting and formatting automatically within a CI system (what is CI?) every time a commit is pushed.

#### An easy solution: No merging if linting fails

To get something set up quickly, it's a good start to make "lint" act the same as running unit tests in CI - block merging the proposed changes until there are no linting errors.

In a CI configuration, that might look like:
```
COPY . .
RUN npm run lint
```
This approach stops reviewers from nitpicking style. "It passed the linter" is a perfectly reasonable response to an overly zealous code reviewer.

It also stops reviewers from having to give style feedback at all - if all of the checks for the code review pass, then the commit is stylistically okay.

#### A better solution: Automatically fix lint issues

For better longer-term automation, it's a good idea to set up a "commitback bot" that creates a linted version of the branch automatically if necessary.

In a CI configuration, that might look like:
```
COPY . .
RUN if ! npm run eslint; then \
	npm run eslint --fix && \
	git config user.name 'lint bot' && \
	git config user.email 'lintbot@example.com' && \
	git add -A && \
	git commit -m 'Automatically linted' && \
	git checkout -b $(git branch --show-current)-linted && \
	git push -f origin $(git branch --show-current)-linted; && \
	echo 'lint failed!'; exit 1; \
fi
```
With this configuration, if a developer pushed to the "myfeat" branch but hadn't linted, the CI configuration would fail their pipeline and create a new branch called "myfeat-linted"

A review could continue like normal, and if lint failed the reviewer could simply merge the "myfeat-linted" branch instead of the "myfeat" branch.

## Examples of linters for various programming languages
---
- JavaScript: ESLint
- TypeScript: TypeScript ESLint
- Python: pylint, flake8
- C++: Google's cpplint
- Go: gofmt
- Java: CheckStyle, FindBugs
- Ruby: RuboCop, Pronto
- Java, JavaScript, C#, TypeScript, Kotlin, Ruby, Go, Scala, Flex, Python, PHP, HTML, CSS, XML and VB.NET: SonarQube
- Python, Go, Ruby, JavaScript, Java, Docker, Terraform, SQL, Shell (not open source) DeepSource

## Conclusion
---
In comparison to most other code review automation tools, linters are exceptionally easy to set up. Any team with more than one developer working in the same codebase should almost immediately set up a linter to catch obvious bugs like infinite loops.

Automatic linting comes standard with many code editors,  so it would be wise to teach developers how to preconfigure their editors to use the existing code rules to avoid errors being pushed at all.

In teams working on earlier products, linters can help avoid writing comprehensive unit tests in the early days, which saves a lot of time for experimental products. In teams working in established products, they stop bickering in code reviews and ensure code is easier to maintain and debug.
