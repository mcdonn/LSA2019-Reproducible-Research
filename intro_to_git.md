[Back to workshop home](README.md)

# Introduction to Git


... will be heavily borrowing from Software Carpentry's lessons http://swcarpentry.github.io/git-novice/. The files on GitHub: https://github.com/swcarpentry/git-novice/tree/gh-pages/_episodes

... and also my class stuff: http://www.pitt.edu/~naraehan/ling1340/


## Setting up Git
http://swcarpentry.github.io/git-novice/02-setup/index.html

List your global config:
```bash
$ git config --global --list
user.name=Na-Rae Han
user.email=naraehan@gmail.com
core.editor=nano
core.autocrlf=input
core.safecrlf=false
```

Set your name and email:

```bash
$ git config --global user.name "Noam Chomsky"
$ git config --global user.email "chomsky@mit.edu"
```



To get help: 
```bash
$ git config -h
```

## Creating a Repository
http://swcarpentry.github.io/git-novice/03-create/index.html

## Tracking Changes
http://swcarpentry.github.io/git-novice/04-changes/index.html

## Exploring History 
http://swcarpentry.github.io/git-novice/05-history/index.html


## Ignoring Things
http://swcarpentry.github.io/git-novice/06-ignore/index.html
