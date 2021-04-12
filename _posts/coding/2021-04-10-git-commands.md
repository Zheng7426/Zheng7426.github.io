---
layout: post
title: "Some common Git commands"
date: 2021-04-10 00:00:00 -0000
categories: coding 
---

### Basic Workflow of Git

* Working Directory

* Staging Area

* Repository

<br>

### git diff
Difference of what has been changed in the tracked files of working directory but not added to the staging area. 

<br>

### git log
Commit history.

<br>

### git add filename1 filename2 || git add .
Adding multiple files in one line.

<br>

### git show HEAD
The most recent commit info.

<br>

### git checkout HEAD filename || git checkout -- filename
Discard changes made to the working directory.

<br>

### git reset HEAD filename || git reset -- filename
Unstage a file but the changes in the working directory are preserved.

<br>

### git reset commit_SHA
Revert to a previous commit version, the commit history beyond that point would be gone. To obtain commit_SHA, use <code>git log</code>.

<br>

### git checkout -b new-branch-name
Create a new branch and immediately switch to that branch.

<br>

### git remote -v
Check the remote repository linked to the local working directory.













