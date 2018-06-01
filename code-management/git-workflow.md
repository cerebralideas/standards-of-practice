# Git Workflow Suggestions and Tips

## I. Getting started

Before getting started you should ensure you have a functioning environment by following the steps outlined in the [Environment Set-Up](https://github.paypal.com/CXP-Web-R/standards-of-practice/blob/master/onboarding/setting-up-your-environment.md) documentation. Now it's time to discuss some guidelines and workflow processes that will hopefully make your daily life a little easier.

## II. Workflow

At this point we are ready to get into the code. Here are some general guidelines to get you started.

## Cloning a Repo:

1. Go the the repo you want to work with. For example -
 `https://github.paypal.com/ConsumerWeb-R/moneynodeweb`
2. In the upper-right hand corner click the **fork** button
3. You should now be in your copy of the repo and the url should look like - `https://github.paypal.com/{user id}/moneynodeweb`
   * click the **Clone or download** button
   * **make sure you are cloning with SSH** and click the small clipboard icon to the right of the text box. Once the codebase is on your machine, please follow our standard [Git Practices](https://github.paypal.com/CXP-Web-R/standards-of-practice/blob/master/engineering/general.md) to contribute to any of our projects.
4. Let's clone our new repo locally
   * open up a terminal by pressing Command + Space and typing *terminal*
   * create a directory to store your code in, this will be the root directory and you will have a folder for each repo in it
   * type - `git clone git@github.paypal.com:{user id}/moneynodeweb.git`
   * now change into your new folder: `cd moneynodeweb`
   * we need to add a new remote called upstream for our new repo, which we can do by typing: `git remote add upstream git@github.paypal.com:ConsumerWeb-R/moneynodeweb.git`
   * pull in the meta data from our new upstream: `git fetch upstream`
   * make our local branch [track upstream](https://git-scm.com/book/id/v2/Git-Branching-Remote-Branches): `git branch --set-upstream-to=upstream/{branch}` where branch is your current working branch

Let's review what we have just accomplished.

1. we have created our own fork of a repo
2. cloned it to our local machine
3. configured our local machine to track the upstream version of our working branch

At this point we are ready to talk a little bit about how we manage our changes with Git.

### Git workflow using `pull/merge`

* Commands
  * pull
  * merge

* Each morning update local develop with `git pull` from your local develop branch.
* In order to update a working branch with the latest code, switch to the working branch with `git checkout {working branch}` and then merge your updated develop into the working branch with `git merge develop`.

This workflow is easier for developers who are less familiar with the specifics of how git works and are just looking for a process to keep their code up to date. A drawback to this process is that squashing commits becomes significantly harder after performing a merge.

### Git workflow using `pull/rebase`

##### Some more info on [rebasing](https://stackoverflow.com/documentation/git/355/rebasing#t=201707312113476986383)

* Commands
  * pull
  * rebase

  * This work style starts off much like the `merge` process updating local develop with `git pull` from your local develop branch.
  * again, switch to your working branch `git checkout {working branch}` except this time you'll use `git rebase develop` to update your branch.

**NOTE:**

If you encounter conflicts while rebasing you will have to `force push` your changes, due to the fact that you have re-written gits history. Before you do this you **_must_** ensure you have `default = nothing` set as your push preference in your `~/.gitconfig`. If you don't and you do something wrong, very bad things can happen!

The main difference here is that using *rebase* to keep your branch up to date will keep it free of merge commits that cause issues with squashing commits.
