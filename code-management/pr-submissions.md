## PR Process

### Prior to submitting PR

We encourage early submissions of PRs, but ask that the code builds without issue: passes linting, compiles and doesn't break any existing tests.

### Submitting a PR

Please review the `CONTRIBUTING.md` of the project as well as all Standards of Practice guidelines for this organization. Here are the basics:

1. PRs should be created on the project's `upstream/develop`, or `upstream/master`, if it's a module
2. The PR should be created from a branch off of your local, and _up-to-date_, `develop` (or `master`, if it's a module) branch
3. The branch name should reflect the feature or bug fix that it's addressing
4. A PR should contain a single feature or bug fix and should have as few commits as possible, preferably one commit
5. The PR title and description should adhere to the project's stated guidelines and should have as much information as possible: links to Rally or Jira, screenshots if UI related, description of changes ...
6. Contributors _should not wait_ until the end of sprint to submit PRs. Submissions should be as early as possible. If the code cannot be submitted until late in the sprint, alert the maintainers of the project (and QA) about the PR and its potential late arrival
7. Expect feedback and don't expect quick merges without proper reviews

### PR reviews

PR reviews are critical to maintaining a stable and high-quality code base. Our organization takes PR reviews seriously, but professionally, so expect a lot of feedback.

1. PR reviews can be started before feature development is complete. Just let us know it's still a WIP (Work In Progress)
2. In addition to expecting a clean build, we will review a PR according to our engineering and style guidelines stated in our Standards of Practice
3. We will try to review each PR in a timely manner, but please don't expect immediate turnaround. We purposefully want PRs to be open for a few days to provide engineers time to review. "Quick merges" are discouraged
4. We do not just evaluate the code's correctness, but also design and style. This is to ensure consistency throughout our codebase, and conformity to the established conventions
5. We will also be respectful of every PR's author and will keep the PR feedback professional, constructive and kind

### Merging a PR

1. All PRs, with a few exceptions, require two independent approvals from engineers. Brand new, complex feature development will require a third QA approval prior to merging
2. PRs ready to be merged should meet our "Definition of Done", which can be seen within our Standards of Practice.
3. There is no self-merging or "quick merges"
4. Once a PR is ready to merge, please squash all commits into one commit, if possible (DO NOT REWRITE PUBLIC HISTORY)
5. One of the two reviewing engineers of the team that directly maintains the codebase will merge your code. Please don't ask anyone outside of the direct team to merge your code
