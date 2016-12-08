# Contributing to Consumer Web

Contributing to code bases should be a structured, disciplined act. Not only should all code being added to the codebase look like it was written by the same dev, but all git commits and PRs should also look like the same person contributed. Standardization is critical when multiple teams of multiple individuals are all contributing to the same codebase.

## Summary

- All code should follow our coding conventions ... needs link.
- Pull requests should be submitted for a discreet task. Please do not submit pull requests with multiple different changes.
- Any new code should be accompanied by test cases.
- All existing test cases must pass.

## Pull Request Checklist

1. Read the project's Wiki for style, convention and understanding of the code base.
2. Follow existing patterns, styles and conventions
3. Did you account for accessbility?
4. Did you add the appropriate documentation concerning your changes?
5. Rebase into as few commits as possible, *BUT NEVER REWRITE PUBLIC HISTORY!*
6. Solicit feedback from multiple project leads; don't ask for immediate merge
7. Add screenshots or screen recordings if applicable
8. Two "thumbs up" are required from prominent contributors for a merge

## Commit Message Guidelines

We have very precise rules over how our git commit messages can be formatted.  This leads to more
readable messages that are easy to follow when looking through the **project history**.

Each commit should be written in this manner using `git commit` command without the `-m` flag (you enter into the Vi editor).

**Please note that Jira IDs should not be used in titles. They have zero meaning and have to be looked up to have any value. Adding them in the body of the commit or PR is good.**

If a single dev is working on a feature or fix then committing is easy. Just have one initial commit, and then `git commit --amend` that commit over and over. As long as your the only dev working on it, this is perfectly fine. Or, you can commit a hundred times, but before you create a PR for it, rebase them all into 1 (`git rebase -i {SHA just before your first}`).

If you have multiple devs working on the same branch, then each dev keeps their own commits to a minimum (no `oops, fixed typo` commits), but don't rewrite another's commits. Then, once the whole PR is done, you can squash all the remaining commits into one (not squashing any public commits).


### Commit Message Format

```
type(scope): subject

body
```

Each commit message consists of two parts: a **header** and a **body**.  The header has a special
format that includes a **type**, a **scope** and a **subject**:

- **Type** - Must be one of the following: **feat** (feature), **fix**, **docs**, **test**, **tech** ([chore, refactor](https://github.com/angular/angular.js/blob/master/CONTRIBUTING.md#type)).
- **Scope** - The scope should specify what UI feature or part of the codebase your change touches. i.e. `SendMoney/CurrencyConversion`,
`Wallet/AddCard`, `Activity`, `Home/AcctBalance`, etc...
- **Subject** - A succinct description of the change.
- **Body** - The motivation for the change (WHY) and contrast this with previous behavior. Helpful context goes here.


### Example
```
fix(buttons/primary): fixed incorrect color assignment

The wrong color (Pay Blue) was used which did not provide enough contrast for a11y. The new color of accessible blue is now used.
  ```

Immediately, the **type** – fix – tells me that this commit is a bugfix, the **scope** is the "buttons/primary, and the **subject** states that it relates to style / color changes. The **body** helps people understand why this change was made and what was changed.

## Creating a PR

When a PR is made the commit text is turned into the PR title and comment. If there is more than one commit to a PR – which is fine, but we'd like to avoid it – then you have to manually alter the PR title and comment to encompass all the commits.

The final PR text should be written like this:

**Title**: type(scope): subject

**Comment**: body

PRs should also be scoped to a focused group of code, a flow or feature, so PRs that fix or address unrelated things should be avoided. We'd rather have smaller, more focused PRs than fewer, large sweeping PRs. This helps in using git logs to debug issues after the fact. A commit of `changed all the things` doesn't help when you are trying to find what commit to revert while a live site is crashing.

### Providing links for verification

Since almost all of our work is tracked with either Rally or Jira, a link to the respective story or defect is necessary. This allows all that review the PR to verify the work done according to the requirements and expectations.

### Screenshots of UI related work

If the work relates to the UI layer, then screenshots of the work is necessary. If it's a defect, then a before and after is recommended. This allows the reviewer to verify the code changes against what they see in the screenshot.

## References

[Here are the definitions for type, scope, subject and body](https://github.paypal.com/ConsumerWeb-R/walletexpnodeweb/blob/develop/CONTRIBUTING.md#commit-message-format). Here are example PRs that you can use as a reference:

- https://github.paypal.com/ConsumerWeb-R/walletexpnodeweb/pull/7857
- https://github.paypal.com/ConsumerWeb-R/walletexpnodeweb/pull/7768
- https://github.paypal.com/ConsumerWeb-R/walletexpnodeweb/pull/7824
