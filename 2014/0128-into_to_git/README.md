Introduction to Git and GitHub
==============================
[Keith Hughitt](khughitt@umd.edu)
2014/01/19

Overview
--------

The goal of this tutorial is to familiarize the user with the basics of [Git](http://git-scm.com/)
and [GitHub](https://github.com/).

Of course, there are already numerous tutorials which do this and do a much
better job than I could hope to do, e.g.:

- [Git - gittutorial Documentation](http://git-scm.com/docs/gittutorial)
- [Try Git: Code School](http://try.github.io/levels/1/challenges/1)
- [Set Up Git · GitHub Help](https://help.github.com/articles/set-up-git)
- [GitHub For Beginners: Don't Get Scared, Get Started](http://readwrite.com/2013/09/30/understanding-github-a-journey-for-beginners-part-1)

I would encourage people to check these out as well.

Here I am just going to try and cover enough to get people started and 
hopefully interested enough to try it out and learn more.

## Intro to version control systems (VCS)

Version control systems (VCS) are software tools used to track changes to a
collection of files and directories and to aide in collaborative development.
VCS is most widely used in the context of software development for tracking
changes to code, but it can also be used to track changes to other types of
work such as manuscripts, data, etc.

Some popular examples include:

- Concurrent Versions System (CVS)
- Subversion (SVN)
- Git
- Bazaar
- Mercurial

Although the big picture is generally the same for each of these, and using
any of them is going to be better than using none, there are some differences
in the philosophy and function of each.

CSV and SVN were developed first, and are *centralized* version control
systems. This means that there is a master codebase, and client hosts which
"checkout" pieces of this code to make changes.

Newer VCS, including the later three listed above, follow a different approach
called *distributed* VCS (dVCS). In this model there is no central repository
-- all clients have an entire copy of the repository.

Both approaches have their advantages and disadvantages. The focus in this
tutorial, however, is on one of the dVCS: git.

## Why is VCS useful?

Some of the main uses for VCS include:

- Tracking changes (imagine not having an undo button in Word...)
- Backing up code (Mirroring on GitHub, etc.)
- Experimentation (branches)
- Collaboration

Git Basics
----------

## Installation

Download and install Git from
[git-scm.com](http://git-scm.com/book/en/Getting-Started-Installing-Git).

## Five most useful git commands to know

This is 99% of what you need to know to use Git:

1. git init
2. git status
3. git commit
4. git push
5. git pull

## 1. Creating a new repo (git init)

To create a new git repository, simply enter the root directory which you want
to make a repo and run `git init`:

```bash
$ mkdir test
$ cd test 
$ git init
Initialized empty Git repository in /home/username/test/.git/
$
```

## 2. Checking a repo's status (git status)

It's always a good idea before making a commit to check the status of a repo
before making any changes using `git status`:

```bash
$ touch newfile
$ echo 'Hello World' > newfile 
$ git status
On branch master

Initial commit

Untracked files:
  (use "git add <file>..." to include in what will be committed)

    newfile

nothing added to commit but untracked files present (use "git add" to track)
$ git add .
$ git status
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

    new file:   newfile
$
```

## 3. Saving changes (git commit)

Once you have done something interesting, `commit` it!

```bash
$ git commit -m 'Important change #1'
[master (root-commit) 9c5205a] Important change #1
 1 file changed, 1 insertion(+)
 create mode 100644 newfile
$ 

Only the changes that you have stages (using `git add`) will be included in
the commit. To include all changes made to files in the repo, you can use
`git commit -am`.
```

## 4. Pushing your changes to a remote repo (git push)

Once you have committed some changes, you may want to sync them with a remote
repository such as GitHub. This is done using the `git push` command.

```bash
$ git push -u origin master
Counting objects: 3, done.
Writing objects: 100% (3/3), 232 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To git@github.com:khughitt/test-repo.git
 * [new branch]      master -> master
Branch master set up to track remote branch master from origin.
$
```

Note that for this to work, you must first create a remote repo and add a
reference to it. We will come back to this part later...

## 5. Pulling changes made to a remote repo

Once you start to collaborate with other people, you will need a way to sync
your repo when other people have made changes to the shared repo.

This is done using the `git pull` command.

```bash
$ git pull
remote: Counting objects: 4, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 0 (delta 0)
Unpacking objects: 100% (3/3), done.
From github.com:khughitt/test-repo
   9c5205a..1336440  master     -> origin/master
Updating 9c5205a..1336440
Fast-forward
 README.md | 3 +++
 1 file changed, 3 insertions(+)
 create mode 100644 README.md
$ 

```

GitHub Basics
-------------

## Overview

[GitHub](https://github.com) is a free online mirroring service for git 
repositories. It hosts mostly open source code, although you can also pay to 
have "private" repositories.

## Why use GitHub?

- Backup your code
- Share your code
- Collaboration
- Online code viewing/editing
- Browsable [commit history](https://github.com/pydata/pandas/commits/master)
- Integrates with [other services](http://developer.github.com/v3/repos/hooks/)
- Renders [Markdown](http://daringfireball.net/projects/markdown/)
- Host websites (e.g. [umd-byob.github.io](umd-byob.github.io))
- Host [HTML5 presentations](http://khughitt.github.io/slidify-byob-intro/#1)
- Host R packages ([install_github](http://www.inside-r.org/packages/cran/devtools/docs/install_github))
- Host Python packages ([pip](http://www.pip-installer.org/en/latest/logic.html#vcs-support))
- Repo [statistics](https://github.com/pydata/pandas/graphs/contributors)

Single-user Workflow
--------------------

For small projects or scripts that you would like to track and/or share on
GitHub, the process is very simple:

1. [Create a repo](https://github.com/new) on GitHub
2. Follow steps to clone repo and [add repo as an upstream
   remote](http://gitready.com/intermediate/2009/02/12/easily-fetching-upstream-changes.html)
3. Hackity-hack (keep it [atomic](http://www.freshconsulting.com/atomic-commits/))
4. `git commit`
5. `git push`
6. Repeat steps 3-5.

It is also not a bad idea to add a
[README.md](https://github.com/umd-byob/presentations/blob/master/README.md) to
the repo with some notes to yourself or others (same as README.txt.)

Multi-user Workflow
-------------------

The process for collaborating with other users on a project using Git and
GitHub is similar to the single-user workflow described above, with a couple
additional steps along the way.

## Setting up the master and forked repos

1. [Create a repo](https://github.com/new) on GitHub (do this once)
2. [Fork](https://help.github.com/articles/fork-a-repo) the master
   repo (each user does this)
3. Follow steps to clone the forked repo and [add repo as an upstream
   remote](http://gitready.com/intermediate/2009/02/12/easily-fetching-upstream-changes.html)
   (each user does this)

## Making changes

Next, once a repo has been created and each user has their own fork of that
repo, the process each user follows to make changes is the same:

1. If master repo has changed, used `git pull` to merge changes into fork.
2. Make changes
3. `git commit`
4. `git push`
5. Submit a [pull request](https://help.github.com/articles/using-pull-requests)

## Accepting changes

Once a pull request (PR) has been submitted, it will [appear on the master
repo](https://github.com/pydata/pandas/pulls). The PR will list all of the
commits made, files changes, and any information the user submitting the PR
provided about the PR.

If this all looks good, then any user who has privileges to the master repo can
"accept" the PR, and the changes will
([usually](https://help.github.com/articles/merging-a-pull-request)) be 
automatically merged into the master repo.

## Other multi-user workflows

There are [other workflows](https://www.atlassian.com/git/workflows) that can
be used for collaboration on GitHub -- the above just illustrates one of these
which I am partial to.

For larger efforts, you can also [create teams on
GitHub](https://help.github.com/articles/how-do-i-set-up-a-team) so that an
entire team owns or manages a repo instead of a single user.

Beyond just code...
-------------------

One of the nice things about Git and GitHub is that you are not limited to
using it for just code. Some other useful things it can be used for include:

- Documents
    - [Notes](https://github.com/khughitt/notes/blob/master/courses/Coursera-Network_Analysis_in_Systems_Biology/03-Topological_Models_and_Network_Evolution.md)
    - [Knitr output](https://github.com/khughitt/network-layouts)
    - [Science manuscripts](https://github.com/sunpy/sunpy-0.4-paper)
- Websites
    - [BYOB](umd-byob.github.io)
    - [Slidify](http://khughitt.github.io/slidify-byob-intro/)

Continuing the journey
----------------------

In case you are still not convinced about this whole Git/GitHub thing, it turns
out that there are other people discussing the same and related ideas, many of
whom are much more knowledgeable than myself.

Here are a few interesting articles and tutorials I picked out that from around
the web:

- [Git for Scientists: A Tutorial](http://nyuccl.org/pages/GitTutorial/)
- [GitHub and Git in the Life Sciences](GitHub and Git in the Life Sciences)
- [Making Reproducible Research Enjoyable](http://yihui.name/en/2012/06/enjoyable-reproducible-research/)
- [Electronic lab notebook - The stupidest thing...](http://kbroman.wordpress.com/2013/08/20/electronic-lab-notebook/)
- [Git can facilitate greater reproducibility and increased transparency in science](http://www.scfbm.org/content/8/1/7)
- [GitHub for Academics: the open-source way to host, create and curate knowledge](http://blogs.lse.ac.uk/impactofsocialsciences/2013/06/04/github-for-academics/)
- [Version control for scientific research](http://blogs.biomedcentral.com/bmcblog/2013/02/28/version-control-for-scientific-research/)

References
----------
- https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet
- https://help.github.com/articles/github-flavored-markdown
