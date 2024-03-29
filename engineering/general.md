# Technical Standards

## I. Code authoring

The overall summary of this section could be referred to as “Engineer for Change”. Business rules change, customers expectations change, requirements change, maintainers change, technologies change … write your applications with this at the center of your mind.

To do that, we have compiled a list of philosophies and approaches to higher level programmatic thinking to lend itself to better long-term code quality. You will find all these ideas in standard computer science theory or popular technical books written by prolific leaders in our industry.

### A. Write code for the maintainers, not for the computers

Computers can understand and execute the ugliest of code as long as it’s syntactically correct. This does not apply to humans. Because of this, the largest reason for standards in code authoring is for the humans that own/read/maintain the code you write.

Know that the original author of code is almost never the final maintainer of the code, so don’t write code for yourself. Write code for the future engineer that has to adopt it after inheriting it *from you*.

#### 1. Writing code is NOT an expression of individuality

Code is community owned, represents PayPal and is explicitly for the customer and company. This means that all code looks like a single person wrote it with the express intent of the customer, as much as possible (don’t take this to a logical extreme).

Conformity has a much higher value than uniqueness when it comes to the scale of PayPal and the reach of its products. If you want to propose a change or a new pattern, raise it to the team and come to a conclusion, **and then document that change**.

#### 2. Cleverness has little long-term value

Let us not confuse clever with smart. Cleverness can easily lead to hard to maintain, difficult to understand and frustrating to debug code as it focuses on the wrong goals: micro-optimizations or ultra succinctness. If there’s a more mundane/boring/verbose way to write code, that’s the preferred, "smart" way.

### B. Design Patterns (Gang of Four)

#### 1. Program to an interface, not an implementation[1]

There are language specific interpretations of this design principle, but I take this a bit more generic. The short of it is focus on how your API is going to be used, not how you have to implement the functionality.

Whether it’s a module, widget, REST API, a model … write code that expresses an interface without the exposure of the implementation. Embrace the idea of public versus private, adhering to conventions and having a small, easy to understand footprint. Don't forget about the principle of least privilege.

#### 2. Composition over inheritance[2]

Classical inheritance (what I call vertical inheritance) has many consequences. Composition (or what I call horizontal inheritance) is much easier to reason-about, debug and maintain. Try to avoid tall vertical inheritance structures as they can be fragile and hard to maintain (fragile base class problem). Focus more on shallow inheritance models, aka composition.

### C. Functional over object-oriented[3]

Many programming languages promote OOP with classes. But, these programming models can have side-effects: implicit state, vertical inheritance, exposure of implementation details, etc. Of course, there are time where OOP is necessary; in those times, use it. This rule is more about preferring functional over OO.

Rather, when possible use a “functional programming” approach, without an adherence on implicit state, using side-effect free functions.  This leads to more declarative, decoupled, explicit, and modular code that will be easier to maintain and can be better performing.

#### 1. Declarative over imperative[4]

Nothing is harder to grok, maintain and debug than imperative code. Rather than thinking in terms of writing procedural statements, write code that describes what it needs to do, not how. That way, each function describes its purpose and encapsulates the implementation of the logic and those hard to read procedural statements.

#### 2. Explicit over implicit

Write code in a way that limits it’s reliance on implicit state (state that "just exists" within the environment), especially when that state is mutable. Explicitness (operate only on what has been explicitly supplied) is always preferred because it’s contained, predictable and side-effect free. Don’t fall into the banana-gorilla problem[5].

### D. Communicate with code

#### 1. Verbosity over terseness

This is where “self-documenting code” comes from. Rarely code requires *no* documentation, but writing in a verbose way reduces the reliance on comments. Nothing’s worse than having to run code just to see what it does.

#### 2. When in doubt, comment

The title pretty much says it all. If there’s any chance that this isn’t easily understood by a passerby, comment on it!

### E. Code Coverage

Code coverage gives a good grasp of all the code paths executed via tests in a unit of code. Code coverage tools, and metrics around them, helps identify untested code paths, making sure all primary paths of code are covered.

But, there is a dark-side to code coverage, and that's writing nearly worthless tests just to inflate your numbers. Some encourage the enforcement an arbitrary number or a continuously increasing number. More times than not, this can cause developers to just write tests that have very little value to get their code checked-in.

## II. Automation

### A. Static code analysis

Nothing’s worse than having to argue over syntactic variations (tabs v. spaces). Leverage static code analysis tools, like syntax “linters” or type checkers, to ensure the *correctness* of your program while building, pushing, CI … and let them enforce the law of the land.

The more developers can focus on the substantive critiques of code the better, so use these tools to avoid the minute syntax arguments.

### B. Testing

Automated testing removes the need to manually review your application’s functionality after a change. Humans are bad at repetition, so don’t make them do it.

#### 1. Unit ("small") tests

Unit tests address small pieces of code and should not require any external data or functionality and be entirely self contained and quick to run. If you have to bootstrap your whole app or start up a server to run your unit tests, something's wrong.

Unit tests should be fast and simple requiring just the unit itself to successfully test.

#### 2. Functional (sometimes "medium" sized) tests

These tests perform a high level verification of some (usually exposed) functionality than unit/small tests. As an example a functional test may verify the method that accepts incoming requests with the expected parameters, maps them accordingly and outputs the appropriate database query. This single test may involve 3, 4 or 5 separate units of code.

The point is to test the composition of units, but should still be testable without starting up your entire environment.

#### 3. System / End to End (also known as "large") tests

These tests perform a more complex flow or touch a variety of different services / domains. And example of this may be on boarding a PayPal user, setting up the user with a bank account and verifying they can send money.

This usually requires an entire stage system being started with the required external services up and running. These tests are usually fewer than unit tests as they are slow and cumbersome.

### C. Automate everything

Automate anything that can be automated. Spend the time to build the necessary tools and utilities upfront. In the long term, you want to be focused on writing what's unique about your task, not what's common.

#### 1. Immediate feedback is best

Favor immediate feedback for automation, especially for the code analysis tools. Don’t let issues slip passed all the way to CI before being caught.

The best is immediate feedback from IDEs or CLI watchers that alarm when something’s caught.

## III. Versioning and Maintenance

### A. Git Practices

#### 1. Unidirectional Flow

To reduce complication is collaborating with a team of developers, the best practice is to have a unidirectional flow of code modifications.

#### 2. Communicate through commits messages

A commit message is recommended to be verbose and informative. Use an unqualified commit, , to be allowed to create a commit title and commit body.

Establish a formulae for constructing this commit message. Don’t just allow gibberish in commit messages.

#### 3. Reduce the amount of commits, noise

A clean git log is incredibly beneficial to investigative research for issues. With this in mind, use the tools Git allows to amend previous commits or squash past commits. A commit represents a logical chuck of functionality.

A git log should never show commit messages of “Oops, typo O_o” or “git is hard!!!!!” littered throughout your history.

#### 4. NEVER rewrite public or another’s history

Rewriting history is a powerful tools for keeping a well maintained git log. But, “with great power comes great responsibility”, so never, ever rewrite public history or another’s history.

Once code is in the dedicated, main branch, or shared with another developer to build upon, it cannot be rewritten. This is law!

### B. Documentation

[Note: `.md` refers to a “Markdown” file. It’s just a very simple formatted text file. [See Github’s style of Markdown for more details](https://help.github.com/articles/github-flavored-markdown/)]

#### 1. README.md

This file is placed at the root of your project and is intended to introduce a newcomer to the project. It includes the following:

- the proper name of the project
- a summary of it’s purpose
- how to install it
- who maintains it
- links to more documentation

#### 2. CONTRIBUTING.md

We recommend that every project has a CONTRIBUTING.md ([a file that is commonplace in OSS](https://github.com/blog/1184-contributing-guidelines)) file in its root directory. This is to communicate the standards that are expected if one is to contribute to the codebase. It needs to spell out as much as possible and leave little to assumption.

For more examples of a CONTRIBUTING.ms file, see here: [Angular.js](https://github.com/angular/angular/blob/master/CONTRIBUTING.md), [Express.js](https://github.com/strongloop/express/blob/master/Contributing.md). Notice how one is very extensive and the other is very simple. It’s up to you, just document it.

#### 2. Code reviews

It is very important to make sure we review each other’s code before it makes its way into production. Not only does this ensure that mistakes are caught, but we can all become better developers by learning from each other.

Each team needs to have a process by which each developer spends at least an hour a day for posted, code reviews, if there is code to review. The best opportunity is via Github and the concept of pull requests (or PRs).

It’s recommended that code that has been merged into the main branch meet the following criteria at the very minimum*:

1. Another engineer has signed off after reviewing the code
2. Another has signed off after executing the code on a machine other than the authoring developer’s

Optimally, the two from above should be done by different people. If the feature is large and complicated, #2 needs to be done by a member of the quality assurance team on a testing stage. It’s also recommended that the machine that is executing the code is a stage/server machine, not a local computer.

But, the only things that is required are that the above two criteria are met.

\* There are obvious exceptions like documentation changes, comment modifications or something super simple. But, if it’s substantial code, then it should follow the two criteria.

#### 3. NO self-merging and no quick-merging

This should be obvious, but merging your own PR into the main branch is not allowed. The only exception is if your modifying documentation or version bumping the meta information (e.g. the version tag on the package.json).

PRs are to exist in an open state for a few hours at the very least, days are recommended. This gives other engineers time to review code and allow multiple pairs of eyes to provide feedback. PRs that contain code changes that are opened and merged within minutes are not allowed.

#### 4. Ensure conformity for all PRs

Always run the codebase’s standard test suite, build or task runners prior to creating a PR to ensure that your code passes the established conventions. This all needs to be documented in the CONTRIBUTING.md file. This allows the reviewers to focus on the substantive code logic, rather than a bunch of nit-picky comments about syntax or style.

#### 5. Release process

End to end release process needs to be identified and documented, hopefully within the project itself or a linked Wiki. This will enable a smoother push of the code to production without a bunch of assumptions.

#### 6. Open (internal) Source

Are the sources for your components open to all developers outside your team and do you accept contributions? Github’s internal, public repos are preferred to allow external (to the team) collaboration.

### C. Bug Tracking System

An official bug tracking system is necessary for proper product maintenance. The location of the bug tracking system/project should be identified and linked from your project’s README.md and should be open to external submission of tickets.

Your SLA needs to be publicly documented.

### D. Continuous Integration

We recommend having an end to end CI (continuous integration) process/pipeline implemented (ideally “ECI phase-2”) of your application/component. The CI pipeline should include building, deploying and testing all branches/repos under active development or support.

The team working on your component should be responsible for the current  “health” of your CI and should know if your CI pipeline is “green” or “red”.   Your CI pipeline needs to be visible to all users and everyone on the team knows how to get the code coverage and test success metrics.

We recommend releases of any artifacts always be done from the same CI pipeline. This is to ensure that release artifacts actually match what’s been building, deploying and testing day in and day out.

## Footnotes:

1. [Program to an interface](https://www.quora.com/In-a-design-pattern-principle-what-does-Program-to-an-interface-not-an-implementation-mean/answer/Jaryl-Sim)
2. [Composition over inheritance](https://en.wikipedia.org/wiki/Composition_over_inheritance)
3. [When FP? And when OOP?](http://raganwald.com/2013/04/08/functional-vs-OOP.html)
4. [Declarative over imperative](https://www.netguru.co/blog/imperative-vs-declarative)
5. [OOP Quotes](http://harmful.cat-v.org/software/OO_programming/)
