git-cheatsheet
==============
A quick reference for before your morning coffee.
Beginners are strongly advised to check out some of the [references below](#useful-references); memorizing syntax can only get you so far.

##Setting up a workstation
Install Git by following [these steps](http://git-scm.com/book/en/Getting-Started-Installing-Git), then:
```bash
git config --global user.name "Your Name"
git config --global user.email youremail@domain.com
git config --global color.ui true
```
##Setting up a local repository
```bash
cd /path/to/repository
git init
```
##Using GitHub (or other remote repositories)
Clone an existing repository
```bash
git clone <repo url> [<folder name>]
```
This downloads the entire repository into its own subfolder, adds the 'origin' remote which points to the clone URL, and checks out the initial branch. Subfolder name defaults to the repo name.

A _remote URL_ points to wherever your code is stored. For the default remote, __origin__ is often used for \<name\>.

Set remote URL.
```bash
git remote add <name> <address>
#Example: git remote add origin https://github.com/rileyjshaw/git-cheatsheet.git
```
Update remote URL
```bash
git remote set-url <name> <NEWURL>
```
Show remote repositories
```bash
git remote -v
```
Remove remote
```bash
git remote rm <name>
```
#Basic actions
Add file to staging area (preparing for a commit)
```bash
git add <list of files>
git add .  #stage changed or new files in working tree (does not stage 'rm' actions)
git add -u  #stage changed or removed files (does not stage untracked files)
git add [--all|-A]  #shortcut for doing both git add . and git add -u
git add *.css  #add all .css files in current directory to tracked files
git add "*.css"  #add all css files in entire project to tracked files
```

Remove a file from staging area
```bash
git rm <list of files>  #untracks *and removes* files
git rm <list of files> -cached  #untracks files but doesn't remove them. Usually want to add these to .gitignore
```

Record a snapshot of the staging area via a commit
```bash
git commit -m "<commit message>"
git commit -am "<commit message>"  #useful shorthand to automatically stage all tracked, modified files before the commit
```
_**Note:** Commit messages should be brief, and written in the present tense._
>"Add PWM block for motor 2"

Push all unsynced commits to a remote repository
```bash
git push [-u] <remote repository name> <local branch name>
#Example: git push -u origin master
```
`-u` sets the upstream repository to the specified remote. After this, you can run `git push`, `git fetch` etc without having to specify remote and branch names.

##Pulling
```bash
git pull [<remote repository name> <local branch name>]
#Example: git pull origin master
```
As long as you've set an upstream branch, you can type `git pull` without the additional arguments.

`git pull` actually does the following:
```bash
git fetch
git merge origin/master
#Use git log and you'll see why this isn't always ideal
```
Using `git pull` can clutter your history with merges; for continuous changes where you just want your branch to reflect the upstream branch, add `--rebase` to keep your logs sane.

```bash
git pull --rebase [<remote repository name> <local branch name>]
```
This way, merges in your history will represent points where divergent branches were intentionally merged.

##Basic references
```bash
git status  #Check what has changed since the last commit
git diff  #Show unstaged line differences since last commit
git diff --staged  #Show staged line differences
git diff <file name>  #Show changes in a specific file since last commit
git diff <commit id> <commit id>  #Show changes between two commits
git log  #Show repository history
git blame <file name>  #Show what revision and author last modified each line of a file
```

#Intermediate actions
##Branching
###Create a new branch
```bash
git branch <name>
```

###List branches
```bash
git branch [-a]
```
`-a` will list both local and remote branches


###Switch to a branch
```bash
git checkout <name>
#Or if you're feeling fancy...
git checkout -b <name> #Creates and checks out a branch
```

###Merge branches
```bash
git checkout <branch to merge to>
git merge <branch to merge from>
```

###Delete a branch locally
```bash
git branch -d <branch name>
```

###Delete a branch locally and remotely
```bash
git push origin –delete <branch name>
```

##Stashing
```bash
git stash  #stashes uncommitted work away (modified tracked files & staged changes)
git stash pop  #pops the latest stashed state and reapplys the changes
git stash list  #shows list of stashes
```
There's more to stashing than this, but I reserve `git stash` for quickly hiding the dirty parts of a branch (if I want to change branches without committing changes, for example). I prefer to treat the stash as a stack with ideal size 0 or 1.

##Tagging
Tagging can be super useful if you're working on a repository with [semantic versioning](http://semver.org/):
```bash
git tag [-a] <tag name> [-m <annotation>]
git push --tags
#Example: git tag -a v1.0.0 -m 'First major release build'
```
Adding the `-a` and `-m` options allows you to add annotations to the tag

#Advanced commands
##Staging and commits
__Warning: be *very* careful when amending or resetting. Generally, you should *not* use these commands if the commit has already been pushed.__

###Unstage a staged file
```bash
Git reset HEAD <file>
```

###Blow away all changes to a file since the last commit
```bash
git checkout --<file>
```

###Add staged files to the last commit
```bash
git commit --amend -m "<New commit message>"
```

###Undo last commit (changes into staging)
```bash
git reset --soft HEAD^
```

###Undo last commit and all changes
```bash
git reset --hard HEAD^
```

###Undo last 2 commits and all changes
```bash
git reset --hard HEAD^^
```

#Terminology
 - __master__ : default branch
 - __origin__ : conventional name for the default upstream repo
 - __HEAD__ : latest (or currently checked-out) commit
 - _[More...](http://stackoverflow.com/questions/7076164/terminology-used-by-git)_


#<a id="refs"></a>Useful references
 - From terminal: `git help <command>` (alternatively, check out the [git(1) Manual Page](https://www.kernel.org/pub/software/scm/git/docs/))
 - [Git Reference](http://gitref.org/)
 - [Everyday Git](https://www.kernel.org/pub/software/scm/git/docs/everyday.html)
 - [Pro Git](http://git-scm.com/book)
 - Codeschool courses: [1](https://www.codeschool.com/courses/try-git), [2](https://www.codeschool.com/courses/git-real), and [3](https://www.codeschool.com/courses/git-real-2)
