## Introduction

no new functionality to get
uses standard git functionality (branching / merging)
shell macros to new functions


- branches are cheap
- merging is easy


## Getting started

### Overview of the commands

	git flow

	usage: git flow <subcommand>

	Available subcommands are:
	   init      Initialize a new git repo with support for the branching model.
	   feature   Manage your feature branches.
	   release   Manage your release branches.
	   hotfix    Manage your hotfix branches.
	   support   Manage your support branches.
	   version   Shows version information.

	Try 'git flow <subcommand> help' for details.

### Starting a feature

We start by creating a new feature called ```documenation_101```.
What will happen is that a new feature branch will be created called ```feature/documenation_101``` based on the development branch.
Remember, we never commit code on the ```master``` branch directly. Everything that goes into this ```master``` banch is done through git-flow commands, never direct commits.

Git flow will also switch to this branch and you can start working on this feature.

	git flow feature start documenation_101
	Switched to a new branch 'feature/documenation_101'

	Summary of actions:
	- A new branch 'feature/documenation_101' was created, based on 'develop'
	- You are now on branch 'feature/documenation_101'

	Now, start committing on your feature. When done, use:

	     git flow feature finish documenation_101

### Optional pushing the feature to remote

If this is a feature where multiple people will be working on you can push it to the remove

	git push -u origin feature/documenation_101

	Counting objects: 5, done.
	Delta compression using up to 4 threads.
	Compressing objects: 100% (3/3), done.
	Writing objects: 100% (3/3), 938 bytes, done.
	Total 3 (delta 1), reused 0 (delta 0)
	To git@github.com:ddewaele/GitFlowDemo.git
	 * [new branch]      feature/documenation_101 -> feature/documenation_101
	Branch feature/documenation_101 set up to track remote branch feature/documenation_101 from origin.

### Finishing a feature

When you try to finish a feature with unstages changes you will get an error:

	git flow feature finish documenation_101
	fatal: Working tree contains unstaged changes. Aborting.

So make sure you check everything in 

When everything has been checked in your feature will be merged into ```develop```.


	git flow feature finish documenation_101
	Switched to branch 'develop'
	Merge made by recursive.
	 README.md |   67 ++++++++++++++++++++++++++++++++++++++++++++++++++++++++++--
	 1 files changed, 64 insertions(+), 3 deletions(-)
	warning: not deleting branch 'feature/documenation_101' that is not yet merged to
	         'refs/remotes/origin/feature/documenation_101', even though it is merged to HEAD.
	error: The branch 'feature/documenation_101' is not fully merged.
	If you are sure you want to delete it, run 'git branch -D feature/documenation_101'.

	Summary of actions:
	- The feature branch 'feature/documenation_101' was merged into 'develop'
	- Feature branch 'feature/documenation_101' has been removed
	- You are now on branch 'develop'

When the feature was finished completely the following thing happens :


	Davys-MacBook-Air:GitFlowDemo ddewaele$ git flow feature finish documenation_102
	Switched to branch 'develop'
	Your branch is ahead of 'origin/develop' by 3 commits.
	Updating de4ff1f..da3f9e2
	Fast-forward
	 README.md |   28 ++++++++++++++++++++++++++++
	 1 files changed, 28 insertions(+), 0 deletions(-)
	Deleted branch feature/documenation_102 (was da3f9e2).

	Summary of actions:
	- The feature branch 'feature/documenation_102' was merged into 'develop'
	- Feature branch 'feature/documenation_102' has been removed
	- You are now on branch 'develop'




## Questions

When starting a feature. does it matter on what branch we're on when we execute the command ?