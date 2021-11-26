# Git Tutorial

A quick Git tutorial and cheatsheet

# Introduction

Connecting to github requires generation of SSH keys. 

```
# Email needs to be same as the login of your github account
ssh-keygen -t rs -b 4096 -C "<email>"
```

- The above command generates a key in the current directory.
- Move the keys to the /home/<user>/.ssh directory
- add the private key to the registry using the following command

```bash
ssh-add <private-key>
```
- add the public key to the github account

## Workflow - Git changes in local

* Write code
* Stage changes (git add)
* Commit changes (git commit)
* Push changes (git push)
* Create a PR

## Commands

Install git with the instructions provided on the URL

```
git --version
```

### Creating a new repo from the command line

```
git init
git add README.md
git commit -m "First Commit"
git remote add origin <origin-name>
git push -u origin master
```
### Cloning, adding a file and pushing changes

```
git clone <repo-url>
git add README.md
git commit -m "First Commit"
git remote add origin <origin-name>
git push -u origin master
```

### Status of the branch

```
git status
```

### Tracking a file

* Untracked file - newly added file which git does not know about
* Modified file - added file which has been modified

```
# Adds only one file untracked/modified
git add <file-name>

# Add all files which are untracked/modified
git add .
```

### Committing a file

```
git commit -m <description of commit>
```

### Pushing a file

```
# This command only commits the file changes
git commit -m <description of commit>

# This command adds and commits the changes
git commit -am <description of commit>


```

### List out all remote repositories

```
git remote -v
```

### Creating a new branch

```
git checkout -b <branch-name>
```

### Switching between branches

```
git checkout <branch-name>
```

### Changes made since the last commit

```
git diff
```

### Showing the diff between master and feature branch

```
git diff <branch-name>
```

### Merge changes of another branch with current branch

```
git merge <branch-name>
```


### Stash changes - If you change branches without committing changes
you will need to stash changes

```
git merge <branch-name>
```

### Resetting to what was already committed and pushed

```

#Resets the specific file
git reset <filename>

#Resets all the files
git reset --hard 

#Resetting your last commit
#Tilda here means 1 behind head
git reset HEAD~1

# resetting it to be a previous commit
git reset --hard <SHA>
```

### Viewing all the commits in reversed chronological order

```
# Displays all information
git log

# Displays only one line information
git log --oneline
```

# Advanced Git Features

## Interactive rebasing

### When is it used?

* Change a commits message
* Delete commits
* Reorder commits
* Combine multiple commits into one
* edit/split an existing commit into mutiple new commits

#### Note

* Do not use interactive rebase on commits you have already pushed
to a shared remote repository.

* To be used only for cleaning up a local commit history before merging it
into shared team branch.

#### Steps to be done for interactive rebase

* How far do you go back to consolidate commits?

```
git rebase -i HEAD~<no-behind>
```
#### Change the commit message

* Executing the above command should open up an editor
* If you need to update a commit, mark "pick" as "reword". Close the editor
* This should open an another editor to change the comment, save and close

#### Changing the commit message

* Executing the above command should open up an editor
* If you need to update a commit, mark "pick" as "reword". Close the editor
* This should open an another editor to change the comment, save and close

#### Squashing several commits

* Follow the same steps as above except that we rename "pick" to "squash"


#### Cherry Picking

Allows individual commits to be integrated

```
git cherry-pick <SHA>
```

#### Reflog

What happens when you want to move back a few commits and *delete* the commit.
After deleting you realize you have some vital changes which you want to 
retrieve back

##### To create the case

Move back the commits on a particular branch

```
git checkout <branch-name>
git reset --hard <SHA>
```

After the above command you will notice that the pointer
has moved back a few commits. The changes no longer show up
when the following command is executed

```
git log
```

Assume there are some important changes you want to get back. Execute
the following command to understand which changes you want back

```
# Display all the logs
git reflog
```

There are 2 ways to reset it

```
git reset --hard <revision-SHA>
```

or 

```
# create a branch
git branch <branch-name> <revision-SHA>
```

##### To recover a deleted branch.

* Delete a branch by mistake
* Recover the branch

```
git reflog
git branch <same-branch-name-as-deleted> <release-SHA>
```

#### Submodules

Consider a git repository on your local machine, let us say you want to add another submodule to this parent rep from another repo.


##### Case 1: Adding a module
```
git submodule add <url>
```
This should add a .gitmodules folder in the parent project and an entry into the .git/config folder.

```
git status
```
Performing a git status basically shows that there are files to be staged. We go ahead
and commit the files

##### Case 2: Cloing and updating a sub module

Instead of using the submodule commands let us say we clone another repo
into a parent repo, and assume that the project by itself which you are cloning
has submodules, in that case the "git clone" will result in empty directories.
This should clone automatically all the submodules.

```
git submodule update --init --recursive
```

You can use the above or you can use clone with the following command

```
git clone --recurse-submodules <url>
```


#### Search and Find

Filtering commit history can be odne by the following criteria


##### Examples

```
#by Date  --before / --after
git log --after=<date> --before=<date>

#by message
git log | grep "<string>"

#by author
git log --author=""

#by file -- <filename>
git log -- <filename>

#by branch <branch-name>
git log <branch-name>
```

# References

* https://www.youtube.com/watch?v=RGOj5yH7evk
* https://askubuntu.com/questions/730754/how-do-i-show-the-git-branch-with-colours-in-bash-prompt