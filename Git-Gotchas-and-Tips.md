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



Git Cheat Sheet
===============
