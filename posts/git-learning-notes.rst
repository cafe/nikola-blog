.. title: Git Learning Notes
.. slug: git-learning-notes
.. date: 2016-04-25 16:07:58 UTC+08:00
.. tags: git, github
.. category: tools
.. link: 
.. description: 
.. type: text
.. author: YONG

Git Project
===========

A git project can be thought of as having three parts in Figure
*git-parts*:

-  A **Working Directory**: creating, editing, deleting and organizing
   files
-  A **Staging Directory**: list changes
-  A **Repository**: Git permanently stores changes as different
   *versions*.

.. TEASER_END   
   
.. figure:: /images/git-learning-notes-3parts.png
   :alt: git-parts
   :width: 480

   3 parts of a Git project

Basic
=====

-  ``git init``
-  ``git status``
-  ``git add filename1, filename2, ...``
-  ``git diff filename.txt``
-  ``git commit -m`` “some message”
-  ``git log``

Backtrack
=========

-  ``git show HEAD``: see the most recently made commit
-  ``git checkout HEAD filename``: restore the file in your working
   directory to look exactly as it did when you last made a commit
-  ``git reset HEAD filename``: unstages file changes in the staging
   area. This command is used when you want to exclude a specific file
   before committing (it has been added to staging area though)
-  ``git reset SHA(first 7 characters of the SHA of a previous commit)``:
   reset to a previous commit in your commit history. You will lost the
   gray commits in Figure *git-reset*.

.. figure:: /images/git-learning-notes-reset.png
   :alt: git-reset
   :width: 480

   git reset diagram

Branching
=========

-  ``git branch``: check what branch you are currently on. The branch
   with an asterisk is the branch you’re on
-  ``git branch branchname``: create a branch
-  ``git checkout branchname``: switch to a branch
-  ``git merge branchname``: if u want to merge a branch *fencing*, you
   need to switch to *master* first

   Merge conflict will happen if you made commits on separate branches
   that alter the same line in conflicting ways. After merge, we can fix
   the merge conflict by hand and then ``add`` and ``commit`` again.

-  ``git branch -d branchname`` delete a branch

Remotes, Pulling, and Pushing
=============================

The remote address is referred to as **origin** by git.

-  ``git clone remote_location clone_name``: get your own replica (named
   clone-name) of a remote project
-  ``git remote -v``: see a list of git projects’ remotes
-  ``git fetch``: fetch any new changes at the remote side (it does not
   merge changes from remote into your local repository. It brings those
   changes onto what’s called a remote branch.)
-  ``git merge origin/master`` merge with remote

   The typical workflow for git collaborations:

   #. Fetch and merge changes from the remote
   #. Create a branch to work on a new project feature
   #. Develop the feature on your branch and commit your work
   #. Fetch and merge from the remote again (in case new commits were
      made while you were working)
   #. Push your branch up to the remote for review

-  ``git push origin your-branch-name``: push your branch up to the
   remote, ``origin``.
