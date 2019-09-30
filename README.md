
# Collaborating with Git Branches

## Introduction

So far we've primarily presented Git as a version control system. Not only is Git a good version control system, it is also a marvelous tool for collaboration and team development. In fact, it was originally designed by Linus Torvalds for coordinating development for the Linux kernel. A primary mechanism through which Git collaboration can effectively be organized is the concept of branches. 

Two golden practices in collaborating with `git` are:

1. Keep the `master` _branch_ functional at all times
2. Keep lines of work (_branches_) separate from each other

Let's explore `git` _branches_ and we'll come back to review why these golden practices are so helpful.

## Objectives

You will be able to:

* Define what a `git` branch is
* Explain branching and committing changes
* Explain switching branches with `git checkout`
* Explain merging branches
* Preview merging remote branches with `git fetch` and `git pull`
* Explain the motivation of the "golden practices"

## Define What a git Branch is

A `git` branch is a means to separate a new set of commits or edits from
another branch. Typically we create a new branch off of `master`. If all
developers we collaborate with honor Golden Practice 1, we can trust that
`master` will be a safe starting point.

When we branch, we're creating a separate parallel universe. We can experiment
there without any adverse effects to the `master` branch. It's a contained sandbox where mistakes can be
made or ideas can incubate.

It's an idea that a lot of fiction has presented in the last 50 years.

|Parallel Universe|Source|
|-----------------|------|
|Mirror Dimension | Dr. Strange (2016)|
|Darkest Timeline | "Community" / "Inspector Spacetime" |
|The entire premise of..| "Dr. Who" |
|Mirror, Mirror (Evil Kirk / Spock) | Star Trek|
|_Plot Against America_ | Philip Roth|
|The entire plot of...| "Primer" (2004)|

If you understand multiple-timeline fiction, you get the idea of branches.

![Annie Edison Says Farewhen to the Inspector](https://media.giphy.com/media/aorHd4Tl6qIDK/giphy.gif)

By doing work in branches, collaborators can work without messing with
the main timeline, known as `master`. OK, so how can we _actually_ leverage this
reality-shattering idea?

## Explain Branching and Committing Changes

Let's suppose a `master` branch with 2 commits:

<img src="images/Image_187_GIT Branch.png">


Best practices suggest that any new set of changes related to fixing a bug,
creating a feature, or even messing around with experimental code in a
"sandbox", should be started on a new branch.

In order to start a new branch, in the terminal type: `git branch <branch name>`
to create the newly defined branch.

This creates a new branch which can be seen in the branch list by typing `git
branch` in the terminal.

In the case of a branch relating to writing a new feature, you could name the
branch `add-preprocessing-and-normalization`. Thus: `git branch add-preprocessing-and-normalization`.
This will take the entire commit history of the branch you're on (usually
`master`) and make it the same history as on the `add-preprocessing-and-normalization`
branch.

At this moment `master` and `add-preprocessing-and-normalization` **are the same branches /
realities** etc.  As you add more commits on the feature branch you're changing
_only_ the `add-preprocessing-and-normalization` reality. The `master` branch **will not be
changed**. Let's talk about adding those commits.

## Explain Switching Branches with git checkout

In order to start making changes on your new branch, you need to "check it
out." After checking a branch out, your commits will be added to that branch's
history. You move between branches with `git checkout <branch name>`.

> **PROTIP**: You can create and checkout a new branch in one command using:
> `git checkout -b new-branch-name`.  That will both create the branch
> `new-branch-name` and move into it by checking it out.

If you are currently on `add-preprocessing-and-normalization`, you can move back to `master`
with `git checkout master`. You can also type `git checkout -` in order to move
back to the previous branch.

When you add commits to a branch, you can see the history of the commits by
typing `git log --graph`. The `git log` command displays the history of commits
for the branch you're on.  The `--graph` "flag" tells `git` to make it pretty,
like a timeline. You can use "Space" to page down the history of commits. Use
`q` to exit.

Let's suppose we added two new commits to our new branch. We could visualize it
as:

<img src="images/Image_188_GIT Branch.png">

To make sure that you don't lose work, you should make sure all your changes
are committed before you switch branches. If you're doing work in
`add-preprocessing-and-normalization` that updates `model.py`, because `master` *also* has
a `model.py` file, `master` could overwrite your changes. Make sure all your
changes are committed before you switch branches.

> **ADVANCED**: `git` has a powerful feature called `stash` which can be used,
> when you're ready to hold changes-in-progress. When you're very comfortable
> with `git`, look into it!

If we then `git checkout master`, and use `git log --graph` again, we will see
that the `master` branch _only_ has the code up to the moment you "branched"
into the `add-preprocessing-and-normalization` timeline, er, branch.

The code from `add-preprocessing-and-normalization` is tucked away in that branch,
waiting patiently in isolation from the rest of your code in `master` until the
feature is considered complete.

The final step of completing the `add-preprocessing-and-normalization` work is to merge that
branch into the `master` branch.

## Explain Merging Branches

Now that you have some additions to the code that you'd like to combine back
with the `master`, the goal is to bring the branch of commits that occurred on
the `add-preprocessing-and-normalization` branch into the `master` branch. By merging the branch,
`master` will have all of the commits from the `add-preprocessing-and-normalization` branch
as though those events occurred on the `master` branch.

When merging a branch with `git merge`, it's important to be currently working
on your target branch, the branch that you want to move the content to of the feature
branch. The first step for our `add-preprocessing-and-normalization` merge is to checkout
`master` because that is where you want the commits to end up.

When performing `git merge -m "merge in feature add-preprocessing-and-normalization"` you
add a message and complete the merge in one action.

Now the branches have been merged. If you type `git log --graph`, you'll see
the commits from the `add-preprocessing-and-normalization` branch on your master branch.

Here's another way to visualize it:

!<img src="images/Image_189_GIT Branch.png">

In this graphic, you might note that a commit happened to `master` _between_
the two commits that made up our feature branch. The amazing thing is `git`
reconciles the `master` timeline, the additional commit, and the commits in
this feature branch. It re-weaves multiple realities together. That is
_seriously_ cool.

When you're done with a branch that's been merged you can delete it with: `git
branch -d branch-to-delete`.

## Preview Merging Remote Branches with git fetch and git pull

Your local branches can merge in changes from _remote_ repository branches
just like they can do for _local_ branches!

To update a list of available branches at a _remote_ we use: `git fetch remote-name`. Note this only updates the list of branches from remote repositories and not the local branches themselves. If you want to update the local branches, you have to merge. To give you a preview of what merging a remote branch workflow
looks like:

```shell
$ git fetch origin 
$ git checkout add-preprocessing-and-normalization 
$ git merge origin/laurens-preprocessing 
```

And now our _local_ `add-preprocessing-and-normalization` has Lauren's ideas woven into it.

Alternatively, as a shorthand, you can `fetch` and then automatically merge the same-named branch
from the _remote_ using `git pull remote-name branch-name-to-merge-in`.

These are complex topics as it brings up the topic of how to reconcile lines of
code where you and another developer might have changed the same thing. This is
called a "merge conflict." We're not going to cover that topic here. Instead we
want you to embrace working in branches, keeping `master` functional, and doing
_local_ merges.

## Explain The Motivation Of The "Golden Practices"

As developers we try to make sure that everyone has a clean place to start
from: be that for writing a new feature or fixing a bug. Branching lets us keep
`master` working at all times. If an emergency bug comes up, we know we have a
solid foundation to build from. Feature branches also help us look at `git
log` and see what the intention of a feature was.

## Summary

Git is a complex tool, and these tools are just scratching the surface for
collaborating with people. These workflows are just being introduced to
you -- and it may be challenging for the time being. You'll have lots of time to
practice them and get used to what each command does. Don't try to cram it
all in at once; instead just start to get an understanding of what is at your
disposal.

![XKCD Git](http://imgs.xkcd.com/comics/git.png)

Image courtesy of [xkcd](https://www.xkcd.com/).

_Do not do as stick man suggests!_
