Developing for YUI will lead you to deal with `git` quite often. The purpose of this page is to list several `git` gotchas as well as offer tips for using `git` with YUI. If you run into any "gotchas" please feel free to add to the list!

Gotchas
======= 

## Branching 

Without an explicit <start point>, `git branch` and `git checkout -b` default to HEAD - which is the branch you are currently on (not necessarily `master`).
So for :

`$ git checkout topic-branch-one`

`$ git checkout -b topic-branch-two`

--> `topic-branch-two` would be created off of `topic-branch-one`, not `master`. 

To specify which branch you would include another argument like:

`$ git checkout topic-branch-one`

`$ git checkout -b topic-branch-three master`

--> `topic-branch-three` branched from `master` instead of `topic-branch-one`



Git Tips
========

##Fundamentals
 
* A branch is a parallel set of commits from an existing commit.

* `git branch foo <commit>` starts this branch, `foo`, from <commit>

* Everything else is just different ways to specify <commit> (as with most things in git). 

    `git branch foo` starts `foo` from whichever commit you're on currently (aka HEAD - normally the tip of your checked out branch).

    `git branch foo upstream/bar` starts `foo` from the commit referenced by upstream/bar, which is the tip of the `bar` branch, on the remote called 'upstream'.

    `git branch foo bar` starts `foo` from the commit referenced by `bar`, which is the tip of your local `bar` branch (which may or may not be different from the upstream/bar commit. In fact your bar may have nothing to do with upstream/bar)

* And sugar on top of `git branch` + `git checkout`

    `git checkout -b foo` is the same as `git branch foo; git checkout foo;`
    `git checkout -b foo upstream/bar` is the same as `git branch foo upstream/bar; git checkout foo;`

## Shell Helpers
YUI Engineer Derek Gathright created a simple shell script to help YUI developers stay up-to-date with all the various branches in YUI. [yui-sync.sh ](https://gist.github.com/4660453)

You should include in your `.bash_profile` (or equiv) a script like [this one](http://www.railstips.org/blog/archives/2009/02/02/bedazzle-your-bash-prompt-with-git-info/) that displays the current git branch whenever you are inside a repo. 

