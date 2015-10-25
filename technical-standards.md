# Engineering Technical Standards

## I. Code authoring

The overall summary of this section should be “code for change”. Business rules change, customers expectations change, requirements change, maintainers change, technologies change … write your applications with this at the center of your mind.’

To do that, I’ve compiled a list of philosophies and approaches to higher level programmatic thinking to lend itself to better long-term code quality. You will find all these ideas in standard computer science theory or popular technical books written by prolific leaders in our industry.

### A. Write code for the maintainers, not for the computers

Computers can understand and execute the ugliest of code as long as it’s syntactically correct. This does not apply to humans. Because of this, the largest reason for standards in code authoring is for the human that will eventually own the code you write.

Now that the original author of code is almost *never* the final maintainer of the code, so don’t write code for yourself. Write code for the unfortunate engineer that has to maintain it after inheriting it.

#### 1. Writing code is NOT an expression of individuality

Code is community owned, represents PayPal and is explicitly for the customer. This means that all code should look like a single person wrote it with the express intent of the customer.

Conformity has a much higher value then uniqueness when it comes to the scale of PayPal and the reach of its products. 

#### 2. Cleverness has no value

To extend on the above, cleverness has no value in this organization due to it being hard to maintain, difficult to understand and frustrating to debug. If there’s a more mundane/boring way to write code, *that’s* the preferred way.

### A. Design Patterns (Gang of Four)

#### 1. Program to an interface, not an implementation

Whether it’s a module, widget, REST API, a model … write code that expresses an interface without the exposure of the implementation. Embrace the idea of public versus private.

#### 2. Composition over inheritance

Inheritance (what I call vertical inheritance) has many consequences. Composition (or what I call horizontal inheritance) is much easier to reason-about, debug and maintain.

### B. Functional over object-oriented

#### 1. Declarative over imperative

Nothing is harder to grok, maintain and debug than imperative code. Declarative code is the best way to “follow the bread crumbs”.

#### 2. Explicit over implicit

Write code in a way that limits it’s reliance on implicit state, especially when that state is mutable. Explicit code is always preferred because it’s contained and predictable.

### C. Communicate with code

#### 1. Verbosity over terseness

This is where “self-documenting code” comes from. Which few code requires no documentation, but it reduces the reliance on the comments. Nothing’s worse than having to run code to see what it does.

#### 2. When in doubt, comment

The title pretty much says it all. If there’s any chance that this isn’t understand by a passerby, comment it!


## II. Automation

### A. Linters and style checkers

Nothing’s worse than having to argue over tabs versus spaces. Leverage linters and style checkers while building, pushing, CI … and let that be the law of the land.

### B. Testing

Testing removes the need to manually review your applications functionality. Humans are bad at repetition, so don’t make them do it.

#### 1. Unit tests

Unit tests should test functional units of code and should not require any external data or functionality. It should be entirely self contained.

#### 2. Functional tests

This should test the entire end-to-end flow of your application.

### A. Automate all the things

Automate anything that can be automated. Spend the time to build the necessary tools and utilities.

#### 1. Immediate feedback is best

Favor immediate feedback for automation, especially for the linters and style checkers. Don’t let issues slip passed all the way to CI.


## III. Versioning and Maintenance

### A. Git Practices

#### 1. Unidirectional Flow

To reduce complication is collaborating with a team of developers, the best practice is to have a unidirectional flow of code modifications.

#### 2. Communicate through commits messages

A commit message should be verbose and informative. Use an unqualified commit, `git commit`, to be allowed to create a commit title and commit body.

Establish a formulae for constructing this commit message. Don’t just allow gibberish in commit messages.

#### 3. Reduce the amount of commits, noise

A clean git log is incredibly beneficial to investigative research for issues. With this in mind, use the tools Git allows to amend previous commits or squash past commits. A commit should represent a logical chuck of functionality.

**A git log should never show commit messages of “Oops, typo O_o” or “git is hard!!!!!” littered throughout your history.**

#### 4. NEVER rewrite public or another’s history

Rewriting history is a powerful tools for keeping a well maintained git log. But, “with great power comes great responsibility”, so never, ever rewrite public history or another’s history.

**Once code is in the dedicated, main branch, it cannot be rewritten. This is law!**

### B. Contributing Practices

#### 1. CONTRIBUTING.md

Every project should have a CONTRIBUTING.md  file in its root directory. This is to communicate the standards that are expected if one is to contribute to the codebase. It should spell out as much as possible to leave little to assumption.

#### 2. Code reviews

Code reviews are absolutely crucial to our practices at PayPal. A PR that has been merged should meet the following criteria at the very minimum:

1. Another engineer has signed off after reviewing the code
2. Another has signed off after executing the code on a machine other than the authoring dev

Optimally, the two from above should be done by different people. If possible, #2 should be done by a member of the quality assurance team. It’s also recommended that the machine that is executing the code is a stage/server machine, not a local computer.

**But, the only things that is required are that the above two criteria are met.**

#### 3. NO self-merging and no quick-merging

This should be obvious, but merging your own PR into the main branch is not allowed. The only exception is if your modifying documentation or version bumping the meta information (e.g. package.json).

PRs are to exist in an open state for a few hours at the very least, days are recommended. This gives other engineers time to review your code and allow multiple pairs of eyes to provide feedback. PRs that contain code changes that are opened and merged within minutes are not allowed.

#### 4. Ensure conformity for all PRs

Always run the codebase’s standard test suite, build or task runners prior to creating a PR to ensure that your code passes the established conventions. Reviewing a PR that requires a bunch of nit-picky comments are a waste of time and frustrating.
