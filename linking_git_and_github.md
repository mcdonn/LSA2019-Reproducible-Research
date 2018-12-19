
... will be heavily borrowing from Software Carpentry's lessons http://swcarpentry.github.io/git-novice/. The files on GitHub: https://github.com/swcarpentry/git-novice/tree/gh-pages/_episodes

... and also my class stuff: http://www.pitt.edu/~naraehan/ling1340/


[Back to workshop home](README.md)

# Linking Git and GitHub

The materials below have been adapted from the excellent lessons by the Software Carpentry, which they have generously made available through the [CC BY 4.0 license](https://creativecommons.org/licenses/by/4.0/). For each of the sections, we encourage you to visit [Software Carpentry's original lesson page](http://swcarpentry.github.io/git-novice/) for more in-depth content. Our workshop lessons below are based on their lessons 7, 8 and 9. 

1. [Remotes in GitHub](#remotes-in-github)
1. [Collaborating](#collaborating)
1. [Conflicts](#conflicts)
1. [Hands-on Group Work](#hands-on-group-work)



## Remotes in GitHub


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

Now that I have the repository living online, I can have collaborators.  But what happens when multiple people work on the same repo? Let's find out. First, I will add Brad as a collaborator of my "language" repo. I go to the GitHub repo, click the settings button on the right, then select Collaborators, and enter Brad's username.


Brad will then get an email message. He can also access the invitation via https://github.com/notifications. Upon accepting it, he will have full access (aka "push" access) to the repo. He then clones the repo to his laptop and goes to work... He adds a new file 'japanese.txt', which he pushes to GitHub repo.  

That means the GitHub repo is more up-to-date than my own local repo on my laptop! What to do? The key is **pull**. Now that the remote repo can be ahead of my local copy, I need to have `pull` as an important first step of my workflow. 

```bash
$ git pull origin master
remote: Counting objects: 4, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 0), reused 3 (delta 0)
Unpacking objects: 100% (3/3), done.
From https://github.com/naraehan/languages
 * branch            master     -> FETCH_HEAD
Updating 9272da5..29aba7c
Fast-forward
 japanese.txt | 1 +
 1 file changed, 1 insertion(+)
 create mode 100644 japanese.txt
```

Now the three repositories (Na-Rae's local, Brad’s local, and Na-Rae’s on GitHub) are back in sync.


> ### A Basic Collaborative Workflow
>
> In practice, it is good to be sure that you have an updated version of the
> repository you are collaborating on, so you should `git pull` before making
> our changes. The basic collaborative workflow would be:
>
> * update your local repo with `git pull origin master`,
> * make your changes and stage them with `git add`,
> * commit your changes with `git commit -m`, and
> * upload the changes to GitHub with `git push origin master`
>
> It is better to make many commits with smaller changes rather than
> of one commit with massive changes: small commits are easier to
> read and review.



## Conflicts


As soon as people can work in parallel, they'll likely step on each other's
toes.  Version control helps us manage these conflicts by giving us tools to
resolve overlapping changes.

To see how we can resolve conflicts, we must first create one.  The file
`zulu.txt` currently looks like this in both partners' copies of our `languages`
repository:

```bash
$ cat zulu.txt
belongs to the Bantu language family
spoken in South Africa
word order: SVO
has about 10 million speakers
```

Suppose Brad and I are working on the same file. Brad adds the line "a close relative of Xhosa", while I add "one of South Africa's official languages". After adding and committing, I try to push:

```bash
$ git push origin master
To https://github.com/naraehan/languages.git
 ! [rejected]        master -> master (non-fast-forward)
error: failed to push some refs to 'https://github.com/naraehan/languages.git'
hint: Updates were rejected because the tip of your current branch is behind
hint: its remote counterpart. Merge the remote changes (e.g. 'git pull')
hint: before pushing again.
hint: See the 'Note about fast-forwards' in 'git push --help' for details.
```

What happened? Turns out Brad had pushed his change in the meantime, therefore my local copy is in conflict. An illustration:

<img src="http://swcarpentry.github.io/git-novice/fig/conflict.svg" width=450px>

Git rejects the push because it detects that the remote repository has new updates that have not been incorporated into the local branch. What we have to do is pull the changes from GitHub, merge them into the copy we’re currently working in, and then push that. Let’s start by pulling:

```bash
$ git pull origin master
remote: Counting objects: 5, done.
remote: Compressing objects: 100% (2/2), done.
remote: Total 3 (delta 1), reused 3 (delta 1)
Unpacking objects: 100% (3/3), done.
From https://github.com/naraehan/languages
 * branch            master     -> FETCH_HEAD
Auto-merging mars.txt
CONFLICT (content): Merge conflict in zulu.txt
Automatic merge failed; fix conflicts and then commit the result.
```

The git pull command updates the local repository to include those changes already included in the remote repository. After the changes from remote branch have been fetched, Git detects that changes made to the local copy overlap with those made to the remote repository, and therefore refuses to merge the two versions to stop us from trampling on our previous work. The conflict is marked in in the affected file:

```bash
$ cat zulu.txt
belongs to the Bantu language family
spoken in South Africa
word order: SVO
has about 10 million speakers
<<<<<<< HEAD
one of South Africa's official languages
=======
a close relative of Xhosa
>>>>>>> dabb4c8c450e8475aee9b14b4383acc99f42af1d
```

Our change is preceded by `<<<<<<< HEAD`. Git has then inserted `=======` as a separator between the conflicting changes and marked the end of the content downloaded from GitHub with `>>>>>>>`. (The string of letters and digits after that marker identifies the commit we’ve just downloaded.)

It is now up to us to edit this file to remove these markers and reconcile the changes. We can do anything we want: keep the change made in the local repository, keep the change made in the remote repository, write something new to replace both, or get rid of the change entirely. For our `zulu.txt`, edit the file to keep both lines, so the file looks like:


```bash
$ cat zulu.txt
belongs to the Bantu language family
spoken in South Africa
word order: SVO
has about 10 million speakers
one of South Africa's official languages
a close relative of Xhosa
```

To finish merging, I add `zulu.txt` to the changes being made by the merge and then commit:

```bash
$ git add zulu.txt
$ git status
On branch master
All conflicts fixed but you are still merging.
  (use "git commit" to conclude merge)

Changes to be committed:

	modified:   mars.txt
```

It's ready to commit:

```bash
$ git commit -m "Merge changes from GitHub"
[master 2abf2b1] Merge changes from GitHub
```

Now I can push the changes to GitHub: 


```bash
$ git push origin master
Counting objects: 10, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (6/6), done.
Writing objects: 100% (6/6), 697 bytes, done.
Total 6 (delta 2), reused 0 (delta 0)
To https://github.com/naraehan/languages.git
   dabb4c8..2abf2b1  master -> master
```


Git’s ability to resolve conflicts is very useful, but conflict resolution costs time and effort, and can introduce errors if conflicts are not resolved correctly. If you find yourself resolving a lot of conflicts in a project, consider these technical approaches to reducing them:

* Pull from upstream more frequently, especially before starting new work
* Use topic branches to segregate work, merging to master when complete
* Make smaller more atomic commits
* Where logically appropriate, break large files into smaller ones so that it is less likely that two authors will alter the same file simultaneously

Conflicts can also be minimized with project management strategies:

* Clarify who is responsible for what areas with your collaborators
* Discuss what order tasks should be carried out in with your collaborators so that tasks expected to change the same lines won’t be worked on simultaneously
* If the conflicts are stylistic churn (e.g. tabs vs. spaces), establish a project convention that is governing. 



## Hands-on Group Work 

Time to practice! Let's work together as a group on this GitHub repository: https://github.com/mcdonn/lsa2019-languages-exercise.  




