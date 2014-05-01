## Introduction

= no new functionality to Git
= uses standard git functionality (branching / merging)
= shell macros to new functions

Key assumptions:

- branches are cheap
- merging is easy

## Some scenarios

- You and your team are developpping features.
- You finish features (meaning they are merged into the development branch)
- At some point you need to create a feature out of this.
- You'll typically close this feature very soon after creating itm because all features will have been merged into development
- Ater finishing the release it is merged to master and tagged.

Suppose you want to develop a feature for a future release.


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


When you published your feature but haven't kept in sync with the remove you'll get the following error:

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

In order to avoid this always ensure that it has been synced with the remote by doing 

	git flow feature publish documenation_101


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


### Pushing your changes

By default, if you do a ```git push``` your tags will not be pushed.

	git push
	Counting objects: 1, done.
	Writing objects: 100% (1/1), 219 bytes, done.
	Total 1 (delta 0), reused 0 (delta 0)
	To git@github.com:ddewaele/GitFlowDemo.git
	   621cbfd..727e7fa  master -> master

This means that when you have finished a release, in order to push your tags you'll need to use the ```--tags``` flag like this:

	git push --tags

	Counting objects: 1, done.
	Writing objects: 100% (1/1), 158 bytes, done.
	Total 1 (delta 0), reused 0 (delta 0)
	To git@github.com:ddewaele/GitFlowDemo.git
	 * [new tag]         1.2 -> 1.2


## Releases

### Starting releases

	git flow release start 1.5

Response :

	Switched to a new branch 'release/1.5'

	Summary of actions:
	- A new branch 'release/1.5' was created, based on 'develop'
	- You are now on branch 'release/1.5'

	Follow-up actions:
	- Bump the version number now!
	- Start committing last-minute fixes in preparing your release
	- When done, run:

### Finishing a release

     git flow release finish '1.5'

Resposne :

	Davys-MacBook-Air:GitFlowDemo ddewaele$ git status
	# On branch release/1.5
	nothing to commit (working directory clean)
	Davys-MacBook-Air:GitFlowDemo ddewaele$ git flow release finish '1.5'
	Switched to branch 'master'
	Merge made by recursive.
	 README.md |   40 +++++++++++++++++++++++++++++++++++++++-
	 1 files changed, 39 insertions(+), 1 deletions(-)
	Deleted branch release/1.5 (was d7d9362).

	Summary of actions:
	- Latest objects have been fetched from 'origin'
	- Release branch has been merged into 'master'
	- The release was tagged '1.5'
	- Release branch has been back-merged into 'develop'
	- Release branch 'release/1.5' has been deleted



### Viewing your changes

When executing the following command:

	git log --graph --all --oneline

you should get this outcome:

	*   727e7fa Merge branch 'release/1.2'
	|\  
	| * ca0d6d4 updated docs
	| * da3f9e2 working on docs
	| *   de4ff1f Merge branch 'feature/documenation_101' into develop
	| |\  
	| | * 2445053 updated docs
	| | * 194b096 working on docs
	| |/  
	| *   d5a1fb7 Merge branch 'feature/add_primary_business_logic' into develop
	| |\  
	| | *   c9388e4 Merge pull request #1 from ddewaeletest/feature/add_primary_business_logic
	| | |\  
	| | | * 7dff3b6 ddewaeletest also working
	| | |/  
	| | * 94b6673 working on business logic feature
	| |/  
	| *   9006548 Merge branch 'release/1.1' into develop
	| |\  
	* | \   621cbfd Merge branch 'release/1.1'
	|\ \ \  
	| | |/  
	| |/|   
	| * | f70b2ed bumping version
	| |/  
	| * e3cc5bb initializing project
	* |   1469103 Merge branch 'release/1.0'
	|\ \  
	| |/  
	| * b1cae29 readme
	|/  
	* 53388f8 Initial commit



## Questions

When starting a feature. does it matter on what branch we're on when we execute the command ?
Feature branches (or sometimes called topic branches) are used to develop new features for the upcoming or a distant future release.
So how do you handle multiple releases being developed in parallel (so different features being developped for different releases that haven't gone into production yet).


The key moment to branch off a new release branch from develop is when develop (almost) reflects the desired state of the new release. At least all features that are targeted for the release-to-be-built must be merged in to develop at this point in time. All features targeted at future releases may not—they must wait until after the release branch is branched off.


So until the release branch is branched off all features targeted future releases are un-finished. They are not merged to dev.
(if they were moved to dev to would go into the next release.)

Suppose we are developing our product, our first release is going to be v1.0
We are developping features and finishing them on the develop branch.
At this point there is no release yet. 
Obviously we are already thinking about v2.0 and there's this feature that we would already like to get started on

So at what point do we decide when we need to start a release ?

- When we are almost feature-complete for v1.0 
- When we want to start working on features for v2.0 ?


## Deleting remote branches

If you're working on a feature branch by yourself it might not always be necessary to publish it, but when multiple people need to work on a feature it is required.

Gitflow by default does not delete remote feature branches when they are finished. 

There seems to be 2 ways of doing it :

- git push origin :feature/new
- git flow feature finish with -F.


### Starting a release with un-merged features (documenten directly in release 1.6)

Imagine sitting on the following feature (un-finished)

	git status
	# On branch feature/documenation_108

And then you start a new release

	git flow release start 1.6

Gitflow will switch to a new branch based on develop.

	Switched to a new branch 'release/1.6'

	Summary of actions:
	- A new branch 'release/1.6' was created, based on 'develop'
	- You are now on branch 'release/1.6'

	Follow-up actions:
	- Bump the version number now!
	- Start committing last-minute fixes in preparing your release
	- When done, run:

	     git flow release finish '1.6'

Is it at this point still possible to bring in the feature ?


## After release has started, no way to pull in stuff from develop

It needs to be very clear that once you started on a release, any features that were open (and were not part of develop) will not be part of this release.


## Multiple releases

Git flow doesn't support multiple releases.

	git flow release start 1.7

	There is an existing release branch (1.6). Finish that one first.


## What if we have conflicts

	git flow release finish 1.6 
	
	Switched to branch 'master'
	Merge made by recursive.
	 README.md       |   29 +++++++++++++++++++++++++++++
	 file-for-1.6.md |    1 +
	 2 files changed, 30 insertions(+), 0 deletions(-)
	 create mode 100644 file-for-1.6.md
	Switched to branch 'develop'
	Auto-merging README.md
	CONFLICT (content): Merge conflict in README.md
	Automatic merge failed; fix conflicts and then commit the result.
	There were merge conflicts.

## References



