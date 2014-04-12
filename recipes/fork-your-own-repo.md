# Fork your own repo on GitHub
**Source: [Jason Krol](http://kroltech.com/2014/01/quick-tip-how-to-fork-your-own-repo-in-github/)**

## Variables

+ `<username>`: your GitHub username
+ `<newrepo>`: a blank repo that you want to fill with your project
+ `<oldrepo>`: the repo that you want to fork

## Steps

```.bash
git clone https://github.com/<username>/<newrepo>.git
git remote add upstream https://github.com/<username>/<oldrepo>.git
git pull upstream master
git push -u origin master
```

## Notes
If you want to pull in new changes from `<newrepo>`, run:

```.bash
git pull upstream master
```
