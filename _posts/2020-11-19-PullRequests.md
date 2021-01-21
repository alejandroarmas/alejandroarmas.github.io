---
layout: article
title: Code Review Github Workflow with Pull Requests 
author:
  Alejandro Armas
tags: Programming
aside:
    toc: true
---

#### Git

Git is a version control system that can center about a centralized repository called a **remote** that lives on some server and a set of distrubuted repositories, often on the local machines of each contributer, which retrieve and ammend changes from the remote. 

Each repository contains snapshots of file content states and directory organization which you can reference to at any point if you wanted to revert changes or work on something experimental.

#### Github

Builds upon this distrubuted version control system and adds many features. 

## Project Management on Github

Each repository on Github comes with features to enable developers to coordinate, track and update their joint projects seemlessly. This is the way to go if you are collaborating on a small team project or even with a network of strangers on open source software. 

### Issues

Consider a feature that users would like implemented, then they would submit an issue into your github repository. Often `issues` could include potential bugs that users encounter. 

### Project Board

<p style="text-align:center;">
    <img src="/assets/images/Git/projectBoard.png" width="75%" height="75%" alt="projectBoard"/>
    <br>
    <em>Figure 1. Example Project Board.
    </em>
</p>

In the `Projects` tab, contributers would be able to add cards to a repritoire of organized to-do's called a project board. Additionally, a card can be added directly from `issues` we just discussed above using `+ Add Cards`.

<p style="text-align:center;">
    <img src="/assets/images/Git/addingIssueToProject.png" width="50%" height="50%" alt="addingIssue"/>
    <br>
    <em>Figure 2. Adding an Issue to Project.
    </em>
</p>

### Working on changes

#### Pull Data from Remote Repository 

Let's see which remote repositories we are configured to. 

```bash
git remote -v
    origin  https://github.com/alejandroarmas/python_algorithms (fetch)
    origin  https://github.com/alejandroarmas/python_algorithms (push)
```

We can see we are connected to a remote repository "origin", which is typically the default shortname that is used in leau of the url of the remote i.e. [https://github.com/alejandroarmas/python_algorithms](https://github.com/alejandroarmas/python_algorithms).  

We use `git fetch` if we want to download any references not present in our local repository, that exist in the remote since the last time we fetched, and `git merge` if we want to merge a reference with our current branch of the repository. 


We can perform the fetch and merge succincly with a single pull. This is possible only if a branch is set to track a remote branch, which is usually already done by default when you clone a remote repository.

```bash
git pull origin main
```

to stay up to date and avoid merge conflicts down the line.



#### What is a branch

Since git stores data as a series of commits, objects that point to directory snapshots and staged file at those snapshots, a **branch** is simply a pointer to a specific commit. When you switch branches, you are merely changing your current `HEAD` pointer, taking you to a different snapshot of your project and decompressing the files to reflect that snapshot. 

#### Create a branch

By convention we create a branch with a namescheme detailing what changes are going to be made. Since the issue suggested implementing the mergesort algorithm for our `Sort` class, we are going to switch to a difference  branch with the `checkout` command and use the `-b` flag to indicate we would like to also create a new branch in the process. 

```bash
git checkout -b mergesort
```

This is the same as these two commands:

```bash
git branch mergesort
git checkout mergesort
```

We can even check what branches exist with this command.
```bash
git branch
    main
    *mergesort
```

#### Do work... 

Let's say we wanted to implement the mergesort algorithm in two files `sort.py` and `test_sort.py`.

Once you are satisfied with your code, and it is *well tested*, then you may continue:

If you have created a new file, or modified an existing file which is already being tracked, using the `git add FILENAME` command will begin tracking that file and/or stage that file's current stage for the next commit.

```bash
git add datastructures/sort.py tests/datastructures/test_sort.py 
git commit -m "implemented mergesort and created mergesort test"
```

Now you have successfully committed your experimental changes onto the `mergesort` branch.

#### Pushing topic branch to Remote Repository

Now you are ready to share your experimental branch with others on the remote. Simply: 

```bash 
git push origin mergesort
```

To create a branch 

#### Submitting a Pull Request

<p style="text-align:center;">
    <img src="/assets/images/Git/createPullRequest.png" alt="createPullRequest"/>
    <br>
    <em>Figure 3. Creating a Pull Request. 
    </em>
</p>

Now you are at the point where you are requesting another user to pull in your changes into their repository. We are going to assume you are and someone else both have write access to the same repository and you want to perform a pull request between two branches in the same repository.

You will need to submit a **pull request** in order to merge the `origin/main` and experimental `origin/mergesort` branches on the remote repository. This is done to ensure another set of fresh eyes is approving of your changes before changes are made.

Notice we use the phrase `Resolves #1`. The syntax `KEYWORD #ISSUE-NUMBER` in the pull request description is what Github uses in order to link an issue to a pull request in the same repository.

<p style="text-align:center;">
    <img src="/assets/images/Git/pullRequestDifference.png" width="75%" height="75%" alt="pullRequestDifference"/>
    <br>
    <em>Figure 4. Pull Request Differences.
    </em>
</p>

Now the pull request is able to be reviewed and merged by somebody else. They are able to see exactly what has been changed. They can provide feedback if the changes are not sufficient and you improve your pull request on said feedback and commit more changes to your experimental branch.

When all is clear they can merge the commit, automatically closing the issue and pull request. 


Now you can delete the experimental branch on the remote using the github web GUI and the local branch using the following commands:

```bash
git checkout main  # You can't delete a branch you are checked out in. So switch.  
git branch -d mergesort 
```

You will notice that on the card within `Project Board` "**To do**" has now moved to "**Done**". This is automated only if you configure it by clicking `+` in the "**Done**" column. 





