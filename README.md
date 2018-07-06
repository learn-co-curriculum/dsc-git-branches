# Collaboration Using `Git`

## Problem Statement

Two golden practices in collaborating with `git` are:

1. Keep the `master` _branch_ working at all times
2. Keep lines of work (_branches_) separate from each other

Collaboration with `git` relies on _branches_. They allow our "golden
practices". Let's explore `git` _branches_ and we'll come back to review why
these golden practices are so helpful.

## Objectives

1. Define what a `git` branch is
2. Explain branching and committing changes
3. Explain switching branches with `git checkout`
4. Explain merging branches
6. Explain the motivation of the "golden practices"

## Define What a `git` Branch is

A `git` branch is a means to diverge from the main line of development, and be
able to continue to do work without messing with the main line known as
`master`.  The master `git` branch is our default branch. One of the
recommended ways to use `git` is to make sure that the master branch is always
"clean" with working code, so that if you ever need to add a bug fix, or start
a new feature, you can work off a working branch. If there's broken code in the
`master` branch, you wouldn't be able to safely deploy.

## Explain Branching and Committing Changes

Best practices suggest that any new set of changes related to fixing a bug,
creating a feature, or even messing around with experimental code in a
"sandbox", should be started on a new branch.  In order to start a new branch,
in the terminal type `git branch <branch name>` to create the newly defined
branch. In the case of a branch relating to writing a new feature, you could
name the branch `add-rainbow-background`. The master branch remains unchanged
and clean. This creates a new branch which can be seen in the branch list by
typing `git branch` in the terminal.

## Explain Switching Branches with `git checkout`

In order to start making changes on your new branch, you need to "checkout" or move into the
`add-rainbow-background` branch, so that `git` knows that all commits made apply to
only that unit of work or branch. You can move between branches with
`git checkout <branch name>`.

> **Protip**: You can create and checkout a new branch in one command using:
> `git checkout -b new-branch-name`.
That will both create the branch `new-branch-name` and move into it by checking
it out.

You can always move between branches with `git checkout <branch name>`. If you
are currently on `add-rainbow-background`, you can move back to master with
`git checkout master`. If the last branch that you switch from was master, you
can also type `git checkout -` in order to move back to the previous branch.
Then to get back to `add-rainbow-background` you can switch it again using `git
checkout add-rainbow-background`.

If you have changes that are not yet committed, when you switch between
branches, the untracked changes will follow you to the next branch. These
changes must be committed with `git commit -m "<my commit message>"` while
still on the feature or bug branch the changes belong to. When the changes on
your feature or bug branch are committed, you'll notice that when you are on
master or another branch with a different branch, the commit with those changes
will not be present. The master branch only has the code from the most recent
commit relative to the master branch or branch. The code from our
`add-rainbow-background` is tucked away in that branch, waiting patiently in
isolation from the rest of your code in `master` until the feature is
considered complete.

The final step of completing the `add-rainbow-background` work sprint is to
merging that branch into the master branch.

## Explain Merging Branches

Now that you have some additions to the code that you'd like to combine back
with the master set of code, the goal is to bring the branch of commits that
occurred on the `add-rainbow-background` branch into the `master`. By merging
the branch, `master` will have all of the commits from the
`add-rainbow-background` branch as though those events occurred on the `master`
branch.

When merging a branch with `git merge`, it's important to be currently working
on your target branch, the branch you want to move into. The first step for our
`add-rainbow-background` merge is to checkout `master` because that is where
you want the commits to end up.

When performing `git merge -m "merge in feature add rainbow-background"` you
can add a message and complete the commit in one action.

Now the branches have been merged. If you type `git log`, you'll see the
commits from the `add-rainbow-background` branch on your master branch.

## Explain Merging Remote Branches with `git fetch` and `git pull`

Your local branches can attach to remote branches that live on the internet,
generally on GitHub, that your team members might contribute to and you can
download locally. Whenever you want to update your local copy with all the
branches that might have been added to the GitHub remote, you can type `git
fetch -a`.

When we `fetch` with `git`, we are asking to copy all changes on the remote to
our local `git` repository, but not actually integrate any. If there are
changes to any branches such as master, you'll see new commits were found. The
branch `origin/master` is the version of `master` on GitHub. Even if `git`
fetched a new commit from `origin/master`, it did not merge it into the local
master.

After you fetch, you have access to the remote code but you still have to merge
it. How do you merge a change fetched from `origin/master` into your current
master? From within your local master branch, type `git merge origin/master`,
referring to the branch's full path, `remote/branch`, or `origin/master`.

The commits fetched via `git fetch` will be merged from the `origin/master`
branch into our local `master` branch. Type `git log` to reveal that the new
changes. These changes will be integrated into your local copy of `master` as
well.

When you fetch, `git` may also output: `* [new branch]`. Similarly, `git`
fetched a new branch and if you want to check it out or merge it you can, using
`git checkout` or `git merge`.

When checking out a remote branch fetched, `git` will create a local branch to
track that remote and switch to that branch. You can now do work, push it back
up to GitHub, and another developer can fetch those changes down, too.

`git fetch` is a pretty low-level `git` command that doesn't get used that much
because it always requires two steps. First `git fetch` and then `git merge` to
actually integrate those changes into your working branch. Generally, if you
are in `master` you want to immediately `fetch` and `merge` any changes to the
remote master.

If you want to both fetch and merge, which is what you want to do most of the
time, just type `git pull`. `git pull` is literally the combination of both
`git fetch` and `git merge`. When you `git pull` the following things will
occur:

1. You will `git fetch` all remote changes, including those on the current
   branch, existing branches, and new branches.
2. Any changes that are on a remote branch which is being tracked by your local
   branch, that is to say, if you are on `master` and there is a change to
   `origin/master`, those changes will be automatically merged.

## Explain The Motivation Of The "Golden Practices"

As developers we try to make sure that everyone has a clean place to start
from: be that for writing a new feature or fixing a bug. Branching lets us keep
`master` working at all times. If an emergency bug comes up, we know we have a
solid foundation to build from. Feature branches also help us look at `git
log` and see what the intention of a feature was.

## Conclusion

`Git` is a complex tool, and these tools are just scratching the surface for
collaborating with people. These workflows are just being introduced to
you--and it may be challenging for the time being. You'll have lots of time to
practice them and get used to what each command does. Don't try to cram it it
all in at once; instead just start to get an understanding of what is at your
disposal.

![XKCD Git](http://imgs.xkcd.com/comics/git.png)

_Do not do as stick man suggests!_

<p class='util--hide'>View <a href='https://learn.co/lessons/git-collaboration-readme'>Git Collaboration</a> on Learn.co and start learning to code for free.</p>

[vi]: https://www.youtube.com/watch?v=_NUO4JEtkDw
