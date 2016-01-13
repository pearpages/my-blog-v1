## History of Version Control
[http://ericsink.com/vcbe/html/history_of_version_control.html](http://ericsink.com/vcbe/html/history_of_version_control.html)

## Configuring Git

Specifity overwrites the config.

### System-level configuration
```
git config --system
# Stored in /etc/config or c:\Program Files(x86)\Git\etc\gitconfig
```

### User-level configuration

```
git config --global
# Stored in ~/.gitconfig or c:\Users\<NAME>\.gitconfig
```

### Respository-level configuration

```
git config
# Stored in .git/config in each repo
```

### Useful Commands

```
git config --global --list
git config --global user.name "Pere Pages"
git config --global user.email "hello@pearpages.com"
git config --unset core.autocrlf
```

## Working locally

```
git init
```

### Add files

 ```
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
 
 ```
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
 
```
# what are we going to discard?
git clean -n 

# discard changes
git clean -f

# discard all changes to the last commit (HEAD)
git reset --hard
```

### .gitignore

Ignoring files and folders

```
node_modules
logs
*.tmp
```

## Working Remotely

### Cloning

```
git clone https://github.com/pearpages/guess-the-number

# See the log in one line
git log --oneline
```

### Log 

```
# Count lines
git log | wc -l

git log --oneline --graph

git shortlog -sne
```

### Viewing Commits

```
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

```
git branch

# display remote branches
git branch -r

git tag
```

### Fetching from a remote

```
git remove -v
git remote add origin https://github.com/pearpages/ionic-ticketing-tool.git
git fetch
# If there's more than one remote repository
get fetch origin

# checking the log of the remote master
git log origin/master

git merge origin/master
```

### Pulling from a remote

```
git fetch
git merge origin/master
```

is the same than doing 

```
git pull origin master
```

### Pushing to a remote

```
git push origin master
```

### Creating and verifying tags

```
git tag v1.0

# signed tag
git tag -s v2.0 

# check signature of tag
git tag -v v2.0
```

### Pushing Tags to a Remote

Tagging gives us stable points

```
git push --tags
```

## Branching, Merging and Rebasing

### Visualizing Branches

```
git log --graph --oneline --all --decorate

# We can create alias in git
git config --global alias.lga "log --graph --oneline --all --decorate"
```

### Creating Branches

```
git branch feature1
git checkout feature1

# create branch keeping not staged files
git branch -b feature1
```

### Differences betwee branches and tags

Tags always stay on the same commit

### Renaming and deleting branches

```
# renaming is the same than moving
git branch -m fix1 bug1234
```

```
# deleting the branch
git branch -d bug1234
```

### Recovering deleted commits

You can use this technique, the reflog one, until 30 days of the commit. Than you lose the changes.

```
git reflog
git branch bug1234 5a78c8b
```

### Stashing Changes

