---
authors:
  - name: "Uchechukwu Obasi"
date: 2021-02-21
linktitle: How To Avoid Force Pushing During Pull Request.
type:
  - post
  - posts
title: How To Avoid Force Pushing During Pull Request.
weight: 1
categories:
  - version control
  - technical
  - open source
images:
  - "/images/blog/git-push-force-not-how-it-works.jpg"
featuredImage: "/images/blog/git-push-force-not-how-it-works.jpg"
---

**In this blogpost, I will be sharing an alternative you can follow to avoid force pushing to your desired branch most especially if you opened a pull request undergoing review on GitHub.**

Force pushing isn't always the best- you rewrite commit history which isn't a good thing. Although in some severe cases, you're left with no other option than to force push your changes to remote. When you perform more complex operations, for example, squash commits, reset or rebase your branch, you must force an update to the remote branch. These operations imply rewriting the commit history of the branch.

In the case of creating pull request, these are the processes I recommend you follow as an alternative to force pushing.

# Checkout to your default branch

Let's assume your default branch to be Master. You should be able to checkout to Master by doing:

```
git checkout master
```

# Fetch from upstream

If you have write access to the upstream branch or you were added to the repository, then you can do:

```
git fetch --prune
```

This will fetch all the latest remote branch refs. It will then delete remote refs that are no longer in use on the remote repository.
This is highly desirable when working in a team workflow in which remote branches are deleted after merge to master.

If you don't have direct access to upstream or you forked from upstream, then you need to set your upstream first:

```
git remote add upstream https://github.com/ORIGINAL_OWNER/ORIGINAL_REPOSITORY.git
```

After that, do `git fetch --prune upstream`.

> **Note:**`git fetch` will fetch all of your branches set to track remote ones, but not merge any changes. `git pull` will update and merge any remote changes of the current branch you're working on. This would be the one you use to update a local branch.

# Git pull

This is very straightforward, just do:

```
git pull
```

If you're working on a forked repo, then you need to suffix the upstream url and the desired branch you want to pull from.

```
git pull upstream master
```

Remember, "master" could be anything depending on what you choose as your desired branch.

# Checkout to a new or existing branch

To checkout to a new branch, do `git checkout -b BRANCH_NAME`. In the case where you already have a branch you're working on, do `git checkout BRANCH_NAME`.

# Merge updates

> **Note:** In the case where you hapen to checkout to a new branch, then you should skip this section since your new branch would contain all the latest changes from master.

```
git merge master
```

# Resolve merge conflicts

If there are conflicts, resolve them. You can use either the [command line](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/resolving-a-merge-conflict-using-the-command-line) or your [favorite IDE](https://medium.com/better-programming/how-to-resolve-git-conflicts-faster-and-more-easily-in-your-favorite-ide-9d2984283a79)

# Push

Once you're done, do `git push origin BRANCH_NAME`.

Thanks for reading!
