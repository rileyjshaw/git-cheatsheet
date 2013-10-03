git-cheatsheet v0.1
==============
A quick reference, for before your morning coffee.
Beginners are strongly advised to check out some of the [references below](#useful-references), since understanding the system is far more important than memorizing syntax.

Once we get past v1 I'll take the version number out of the title, but for now it's a good reminder that this is a work in progress.

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
git clone <repo url>
```
This downloads the entire repository, adds the 'origin' remote which points to the clone URL, and checks out the initial branch.


Set remote URL. Note that __origin__ is often used for the \<name\> attribute.
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
git add .  #add changed or new, not ignored paths within working tree to staged changes (does not stage 'rm' actions)
git add -u  #add changed or removed paths of already tracked files to staged changes 
git add [--all|-A]  #shortcut for doing both git add . and git add -u
git add *.css  #add all .css files in current directory to tracked files
git add "*.css"  #add all css files in entire project to tracked files
```
Record a snapshot of the staging area via a commit
```bash
git commit -m "<commit message>"
git commit -am "<commit message>"  #useful shorthand which automatically stages all tracked, modified files before the commit
```
_**Note:** Commit messages should be brief, and written in the present tense._
>"Add PWM block for motor 2"

Push all unsynced commits to a remote repository
```bash
git push -u <remote repository name> <local branch name>
#Example: git push -u origin master
```

##Pulling
Merge pull
```bash
git pull <remote repository name> <local branch name>
#Example: git pull origin master
```

git pull actually does the following:
```bash
git fetch
git merge origin/master
#Use git log and you'll see why this isn't ideal
```

Rebase pull
```bash
git pull --rebase
```

##Basic references
Check what has changed since the last commit
```bash
git status
```
```bash
git diff  #Show unstaged line differences since last commit
git diff --staged  #Show staged line differences
```
```
git log
```

#Intermediate actions
##Branching
Create new branch
```bash
git branch <name>
```

List branches
```bash
git branch
```

Switch to a branch
```bash
git checkout <name>
#Or if you're feeling fancy...
git checkout -b <name> #Creates and checks out a branch
```

Merge branches
```bash
git checkout <branch to merge to>
git merge <branch to merge from>
```

Delete branch
```bash
git branch -d cat
```


##Advanced commands
###Staging and commits
__Warning: be *very* careful when amending or resetting. You should *not* use these commands once the commit has already been pushed.__

Unstage a staged file
```bash
Git reset HEAD <file>
```
Blow away all changes to a file since last commit
```bash
git checkout --<file>
```
Add staged files to the last commit
```bash
git commit --amend -m "<New commit message>"
```
Undo last commit (changes into staging)
```bash
git reset --soft HEAD^
```
Undo last commit and all changes
```bash
git reset --hard HEAD^
```
Undo last 2 commits and all changes
```bash
git reset --hard HEAD^^
```

##Terminology
__HEAD__ refers to the latest commit

##<a id="refs"></a>Useful references
```bash
git help <command>
```
[Pro Git](http://git-scm.com/book)
