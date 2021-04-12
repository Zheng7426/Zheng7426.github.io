---
layout: post
title: "Some common Git commands"
date: 2021-04-10 00:00:00 -0000
categories: coding 
---

## Basic Workflow Elements of Git

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


<br>

## Github Workflow in details

Git is a version control tool, while Github is a hosting platform where you can store, publish, and download repositories. Here are some notes derived from the official [Github Workflow](https://guides.github.com/introduction/flow/) guidance:

1. Create a branch

A branch is where you can experiment with new features and functionalities to your project. Whatever changes you make on a branch would not directly affect the `main branch`. After you are satisfied with your local changes, you can create a pull request to merge it with the `main` branch, so that other collaborators can review it. Any content in the `main` branch would be regarded as ready to deploy.  

2. Add commits

After you make changes on your local working directory, you may use `git add` command to move the changes onto the staging area, waiting to be commited with some descriptions(commit message). As you work on adding a new feature or fixing a bug, this process is tracked and can be reverted if needed. Thus, every commit ought to be focused on one thing and separated from other commits. 

3. Open a Pull Request

If you want to initiate discussion about your commits with other collaborators, you may open a pull request for them to accept. They would have a chance to see what changes you made and provide feedbacks to you in case there needs to be some modifications in your code. 

4. Discuss and review

After the pull request was opened, your collaborators would be notified about the changes you want to merge. For example, once I have finished translation for one chapter of a very good book about JavaScript, I could upload the content of the chapter and then waiting for it to be reviewed. There might be some discussions about a specific wording in the chapter, and some modifications would be made after the collaborators and I reached agreement. After that, I would make some changes and then commit again. 

5. Deployment

Some teams have staging environment, testing environment and production environment. You can deploy from a branch for final testing before the pull request is merged to the `main` branch. You can also skip the testing and deploy to the production environment directly, it depends on your needs. 

6. Merge

Once your code has been reviewed and verified, you can merge it to the `main` branch. This would leave a record for other people to understand why such changes have been made. 

















