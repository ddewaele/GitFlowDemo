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

### Starting a release

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





## Questions

When starting a feature. does it matter on what branch we're on when we execute the command ?