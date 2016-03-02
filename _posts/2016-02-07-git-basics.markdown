---
layout: post
title:  "Git Basics"
date:   2016-02-07 18:22:12
categories: git
---

#### Contents

{:.no_toc}
* 
{:toc}

## History of Version Control

[http://ericsink.com/vcbe/html/history_of_version_control.html](http://ericsink.com/vcbe/html/history_of_version_control.html)

## Configuring Git

Specifity overwrites the config.

### System-level configuration

```bash
git config --system
# Stored in /etc/config or c:\Program Files(x86)\Git\etc\gitconfig
```

### User-level configuration

```bash
git config --global
# Stored in ~/.gitconfig or c:\Users\<NAME>\.gitconfig
```

### Respository-level configuration

```bash
git config
# Stored in .git/config in each repo
```

### Useful Commands

```bash
git config --global --list
git config --global user.name "Pere Pages"
git config --global user.email "hello@pearpages.com"
git config --unset core.autocrlf
```

## Working locally

```bash
git init
```

### Add files

```bash
# only modified
 git add -u
 
 # modified and new
 git add --all
 git add -A
 
 git commit -m "files changed"
 
 git log
 
 # comparing with the last cmomit
 git diff dd68210..a234c4 
 
 # The lataest commit is called HEAD
 git diff HEAD
 # the prior the latest one
 git diff HEAD~1 
 # before the prior of the latest one
 git diff HEAD~2
```
 
### Undoing Changes
 
```bash
 # Undoing one file
 git checkout README.txt
 
 # Undoing all changes in the files but not removing the staged or discarding
 git chekcout .
 
 # All changes back to the HEAD (the last commit) losing the staged and therefore discarding
 git reset --hard 
 
 # Goes back to one commit before the last one (HEAD) but keeps the staged files
 git reset soft HEAD~1
```
 
### Discarding changes
 
```bash
# what are we going to discard?
git clean -n 

# discard changes
git clean -f

# discard all changes to the last commit (HEAD)
git reset --hard
```

### .gitignore

Ignoring files and folders

```bash
node_modules
logs
*.tmp
```

## Working Remotely

### Adding a remote origin

```bash
git remote add origin https://github.com/user/repo.git
# Set a new remote

git remote -v
# Verify new remote
```

### Cloning

```bash
git clone https://github.com/pearpages/guess-the-number

# See the log in one line
git log --oneline
```

### Log 

```bash
# Count lines
git log | wc -l

git log --oneline --graph

git shortlog -sne
```

### Viewing Commits

```bash
git show HEAD
git show HEAD~1

git log --oneline
git show 5642626

git remote
git remote -v
```

### Git Protocols

- http
- https
- git
- ssh
- file

```
[remote "origin"]
url = https://github.com/pearpages/ionic-ticketing-tool.git
fetch = +refs/heads/*:refs/remotes/origin/*
[branch "master"]
remote = origin
merge = refs/heads/master
```

```bash
git branch

# display remote branches
git branch -r

git tag
```

### Fetching from a remote

```bash
git remote -v
git remote add origin https://github.com/pearpages/ionic-ticketing-tool.git
git fetch
# If there's more than one remote repository
get fetch origin

# checking the log of the remote master
git log origin/master

git merge origin/master
```

### Pulling from a remote

```bash
git fetch
git merge origin/master
```

is the same than doing 

```bash
git pull origin master
```

### Pushing to a remote

```bash
git push origin master
```

### Creating and verifying tags

```bash
git tag v1.0

# signed tag
git tag -s v2.0 

# check signature of tag
git tag -v v2.0
```

### Pushing Tags to a Remote

Tagging gives us stable points

```bash
git push --tags
```

## Branching, Merging and Rebasing

### Visualizing Branches

```bash
git log --graph --oneline --all --decorate

# We can create alias in git
git config --global alias.lga "log --graph --oneline --all --decorate"
```

### Creating Branches

```bash
git branch feature1
git checkout feature1

# create branch keeping not staged files
git branch -b feature1
```

### Differences betwee branches and tags

Tags always stay on the same commit

### Renaming and deleting branches

```bash
# renaming is the same than moving
git branch -m fix1 bug1234
```

```bash
# deleting the branch
git branch -d bug1234
```

### Recovering deleted commits

You can use this technique, the reflog one, until 30 days of the commit. Than you lose the changes.

```bash
git reflog
git branch bug1234 5a78c8b
```

### Stashing Changes

```bash
git stash
git stash list
git stash apply
# it's the same than apply but gets rid of it in the list
git stash pop

git stash drop
git stash branch feature2
```

### Merging Branches

**kdiff3** is a merging tool that can be used.

```bash
git merge feature1
git branch -d feature1

git merge feature2_additional
git diff --cached
git commit -m "merged"
```

### Rebasing

```bash
git rebase master
```

### Cherry picking changes

Apply only a specific commit

```bash
git cherry-pick 6fa4324
```

### Creating a remote branch

We can do it just pushing the changes

### Deleting a remote branch

```bash
git push origin :my-branch-to-delete
```

## Useful snippets

### Undo working copy modifications of one file in Git

```bash
# You can do it without the -- , but if the filename looks like a branch or tag (or other revision identifier), it may get confused, so using -- is best.
git checkout v1.2.3 -- my-file.js         # tag v1.2.3
git checkout stable -- my-file.js         # stable branch
git checkout origin/master -- my-file.js  # upstream master
git checkout HEAD -- my-file.js           # the version from the most recent commit
git checkout HEAD^ -- my-file.js          # the version before the most recent commit
```