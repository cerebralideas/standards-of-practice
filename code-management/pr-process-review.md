## PR Process

### Prior to submitting PR

We encourage early submissions of PRs, but ask that the code builds without issue: passes linting, compiles and doesn't break any existing tests.

### Submitting a PR

Please review the `CONTRIBUTING.md` of the project as well as all [Standards of Practice guidelines for this organization](https://github.paypal.com/CXP-Web-R/standards-of-practice). Here are the basics:

1. PRs should be created against the project's `upstream/develop` (or `upstream/master`, if it's a module) from your personal fork (aka `origin`)
2. The PR should be created from a branch off of your local, and _up-to-date_, `develop` (or `master`, if it's a module) branch
3. The branch name should reflect the feature or bug fix that it's addressing. E.g. `new-add-card-flow` or `fix-withdrawal-errors`
4. A PR should contain a single feature or bug fix and should have as few commits as possible, preferably one commit
5. The PR title and description should adhere to the project's stated guidelines and should have as much information as possible: links to Rally or Jira, screenshots if UI related, description of changes ...
6. Contributors _should not wait_ until the end of sprint to submit PRs. Submissions should be as early as possible. If the code cannot be submitted until late in the sprint, alert the maintainers of the project (and appropriate QA) about the PR and its potential late arrival
7. **Content Cutoff**: Any PR that contains content needs to be merge'able by the Thursday prior to sprint-end. This is to allow localization to take place in preparation for sprint-end releases. _If there is a chance your PR may not be merge'able by that time, please open a "Content Only PR" that can be merged in separately_
8. Expect feedback and don't expect quick merges without proper reviews

### PR reviews

PR reviews are critical to maintaining a stable and high-quality code base. Our organization takes PR reviews seriously and professionally, so expect feedback (it may be more than you're used to).

1. PR reviews can be started before feature development is complete. Just let us know it's still a WIP (Work In Progress). Most of our projects have a `DO NOT MERGE` or `WIP` labels which can be used if you have write permissions. If not, communicate this in the title of your PR
2. In addition to expecting a clean build, we will review a PR according to our engineering and style guidelines stated in our [Standards of Practice](https://github.paypal.com/CXP-Web-R/standards-of-practice).
3. We will try to review each PR in a timely manner, but please don't expect immediate turnaround. We purposefully want PRs to be open for a few days to provide engineers time to review. "Quick merges" are discouraged
4. We do not just evaluate the code's correctness, but also design and style. This is to ensure consistency throughout our codebase, and conformity to the established conventions
5. We will also be respectful of every PR's author and will keep the PR feedback professional, constructive and kind [1]

### Merging a PR

1. All PRs, with a few exceptions, require two independent approvals from engineers. Brand new, complex feature development will require a third QA approval prior to merging
2. PRs ready to be merged should meet our ["Definition of Done"](https://github.paypal.com/CXP-Web-R/standards-of-practice/blob/master/agile/definition-of-done.md), which can be seen within our Standards of Practice.
3. Self-merging or "quick merges" are not allowed
4. Once a PR is ready to merge, please squash all commits into one commit, if possible (DO NOT REWRITE PUBLIC HISTORY). If you have questions or concerns, please reach out to one of us (see DLs below)
5. One of the two reviewing engineers of the team that directly maintains the codebase will merge your code. (NOTE: Please don't ask anyone outside of the direct team to merge your code)

### DLs for product teams

1. Summary page: DL-PayPal-Coyotes <DL-PayPal-Coyotes@paypal.com>
2. Wallet page: Team Six Core <DL-PayPal-Team-Six-Core@paypalcorp.com>
3. Activity page: DL-PP-Consumer-Wildcards <DL-PP-Consumer-Wildcards@paypal.com>
4. Settings page: Luche Libre <DL-PP-DT-Luche-Libre-Austin@paypalcorp.com>
5. Header-footer service: DL-PayPal-Coyotes <DL-PayPal-Coyotes@paypal.com>

### Footnote

1. [Mindful communications in code reviews](http://amyciavolino.com/assets/MindfulCommunicationInCodeReviews.pdf)