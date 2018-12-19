
... will be heavily borrowing from Software Carpentry's lessons http://swcarpentry.github.io/git-novice/. The files on GitHub: https://github.com/swcarpentry/git-novice/tree/gh-pages/_episodes

... and also my class stuff: http://www.pitt.edu/~naraehan/ling1340/


[Back to workshop home](README.md)

# Linking Git and GitHub

The materials below have been adapted from the excellent lessons by the Software Carpentry, which they have generously made available through the [CC BY 4.0 license](https://creativecommons.org/licenses/by/4.0/). For each of the sections, we encourage you to visit [Software Carpentry's original lesson page](http://swcarpentry.github.io/git-novice/) for more in-depth content. Our workshop lessons below are based on their lessons 7, 8 and 9. 

1. [Remotes in GitHub](#remotes-in-github)
1. [Collaborating](#collaborating)
1. [Conflicts](#conflicts)



## Remotes in GitHub
http://swcarpentry.github.io/git-novice/07-github/index.html
... the screenshots are terrible


Version control really comes into its own when we begin to collaborate with
other people.  We already have most of the machinery we need to do this; the
only thing missing is to copy changes from one repository to another.

Systems like Git allow us to move work between any two repositories.  In
practice, though, it's easiest to use one copy as a central hub, and to keep it
on the web rather than on someone's laptop.  Most programmers use hosting
services like [GitHub](https://github.com) to hold those master copies. 

Let's start by sharing the changes we've made to our current project with the
world.  Log in to GitHub, then click on the icon in the top right corner to
create a new repository:

<img src="img/github_repo1.png" width=240px>

Name your repository "languages", and then click "Create Repository".  As soon as the repository is created, GitHub displays a page with a URL and some information on how to configure your local repository. 

The next step is to connect the two repositories. We do this by making the GitHub repository a **remote** for the local repository. The home page of the repository on GitHub includes the address of the GitHub repo. Click on the clipboard icon to copy it:

<img src="img/github_repo2.png">


Then, return to your "languages" directory in command line, and execute:  

```bash
$ git remote add origin https://github.com/naraehan/languages.git
``` 

Make sure to use the URL for your repository rather than Na-Rae’s: the only difference should be your username instead of `naraehan`. We can check that the command has worked by running `git remote -v`:


```bash
$ git remote -v
origin https://github.com/naraehan/languages.git (push)
origin https://github.com/naraehan/languages.git (fetch)
```

The name `origin` is a typical local nickname for your remote repository. 

Once the nickname `origin` is set up, this command will push the changes from our local repository to the repository on GitHub:

```bash
$ git push origin master
```

That "pushes" the changes in your local repo out to the GitHub repo, thereby syncing them up. This "pushing" step is typically the very last step of Git/GitHub workflow, which now looks like:

   1. `git status` (shows clean state)
   1. ... edit some files ... 
   1. `git status`, `git diff`, etc. (to confirm changes)
   1. `git add x y z` 
   1. `git status`, `git diff`, etc. (to confirm changes)
   1. `git commit -m "a message"`
   1. `git push origin master` 

Go ahead add another Zulu language fact to `zulu.txt`: it has about 10 million speakers. You should follow the workflow above. 



## Collaborating
http://swcarpentry.github.io/git-novice/08-collab/index.html
... probably should do a collaboration demo with a real github repo


## Conflicts
http://swcarpentry.github.io/git-novice/09-conflict/index.html

