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

