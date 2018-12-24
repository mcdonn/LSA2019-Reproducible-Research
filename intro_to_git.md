# Introduction to Git

The materials below have been adapted from the excellent lessons by the Software Carpentry, which they have generously made available through the [CC BY 4.0 license](https://creativecommons.org/licenses/by/4.0/). For each of the sections, we encourage you to visit [Software Carpentry's original lesson page](http://swcarpentry.github.io/git-novice/) for more in-depth content. Our workshop lessons below are based on their lessons 2 to 6. 

1.  [Setting Up Git](#setting-up-git)  
1.  [Creating a Repository](#creating-a-repository) 
1.  [Tracking Changes](#tracking-changes) 
1.  [A Commit Workflow](#a-commit-workflow) (2nd half of SWC's Tracking Changes)
1.  [Exploring History](#exploring-history) 
1.  [Ignoring Things](#ignoring-things) 

## Setting Up Git

When we use Git on a new computer for the first time,
we need to configure a few things. Below are a few examples
of configurations we will set as we get started with Git:

*   our name and email address,
*   what our preferred text editor is,
*   and that we want to use these settings globally (i.e. for every project).

On a command line, Git commands are written as `git verb options`,
where `verb` is what we actually want to do and `options` is additional optional information which may be needed for the `verb`. So here is how you would look up your global setting: 

```bash
$ git config --global --list
user.name=Na-Rae Han
user.email=naraehan@gmail.com
core.editor=nano
core.autocrlf=input
core.safecrlf=false
```

Your name and email will need setting up. Commands to set them on your machine:

```bash
$ git config --global user.name "Henry Higgins"
$ git config --global user.email "profhiggins@oxford.edu"
```
Please use your own name and email address instead of Prof. Higgins's. This user name and email will be associated with your subsequent Git activity,
which means that any changes pushed to online git host servers such as 
[GitHub](https://github.com/) 
in a later lesson will include this information.

One additional detail: your default editor. If you followed our installation instruction, it should already be set to `nano` or your own favorite text editor. If that is not the case, reset it as shown below. 

```bash
$ git config --global core.editor "nano"
```

Lastly, if you forget a `git` command, you can access the list of commands by using `-h` and access the Git manual by using `--help`:
```bash
$ git config -h
```


## Creating a Repository


Once Git is configured, we can start using it. First, let's create a directory in `Desktop` folder for our work and then move into that directory:

```bash
$ cd ~/Desktop
$ mkdir languages
$ cd languages
```


Then we tell Git to make `languages` a **repository** -- a place where
Git can store versions of our files:

```bash
$ git init
```


It is important to note that `git init` will create a repository that
includes subdirectories and their files -- there is no need to create
separate repositories nested within the `languages` repository, whether
subdirectories are present from the beginning or added later. Also, note
that the creation of the `languages` directory and its initialization as a
repository are completely separate processes.

If we use `ls` to show the directory's contents,
it appears that nothing has changed:

```bash
$ ls
```

But if we add the `-a` flag to show everything,
we can see that Git has created a hidden directory within `languages` called `.git`:

```bash
$ ls -a
.	..	.git
```

Git uses this special sub-directory to store all the information about the project, 
including all files and sub-directories located within the project's directory.
If we ever delete the `.git` sub-directory,
we will lose the project's history.

We can check that everything is set up correctly
by asking Git to tell us the status of our project:

```bash
$ git status
# On branch master
#
# Initial commit
#
nothing to commit (create/copy files and use "git add" to track)
```



## Tracking Changes

<!-- 
First let's make sure we're still in the right directory.
You should be in the `languages` directory.

```bash
$ pwd
/home/naraehan/Desktop/languages
```
-->


Let's create a file called `zulu.txt` that contains some notes
about the language.
We'll use `nano` to edit the file; you can use your favorite editor.
In particular, this does not have to be the `core.editor` you set globally earlier. But remember, the bash command to create or edit a new file will depend on the editor you choose (it might not be `nano`). 

```bash
$ nano zulu.txt
```

An editor window will open up. Type the text below into the `zulu.txt` file:

```
belongs to the Bantu language family
```

To save and exit `nano`,  hit `Ctrl+X`, and then `y` to save. `zulu.txt` now contains a single line, which we can see by running:

```bash
$ cat zulu.txt
belongs to the Bantu language family
```

If we check the status of our project again, Git tells us that it’s noticed the new file:

```bash
$ git status
On branch master

Initial commit

Untracked files:
   (use "git add <file>..." to include in what will be committed)

	zulu.txt
nothing added to commit but untracked files present (use "git add" to track)
```

The "untracked files" message means that there's a file in the directory
that Git isn't keeping track of.
We can tell Git to track a file using `git add`:

```bash
$ git add zulu.txt
```
and then check that the right thing happened:

```bash
$ git status
On branch master

Initial commit

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)

	new file:   zulu.txt
```

Git now knows that it's supposed to keep track of `zulu.txt`,
but it hasn't recorded these changes as a commit yet.
To get it to do that,
we need to run one more command:

```bash
$ git commit -m "start notes on Zulu language"
[master (root-commit) f22b25e] start notes on Zulu language
 1 file changed, 1 insertion(+)
 create mode 100644 zulu.txt
```

When we run `git commit`,
Git takes everything we have told it to save by using `git add`
and stores a copy permanently inside the special `.git` directory.
This permanent copy is called a **commit** and its short identifier is `f22b25e`.
Your commit may have another identifier.

We use the `-m` flag (for "message")
to record a short, descriptive, and specific comment that will help us remember later on what we did and why.
If we just run `git commit` without the `-m` option,
Git will launch `nano` (or whatever other editor we configured as `core.editor`)
so that we can write a longer message.

If we run `git status` now:

```bash
$ git status
On branch master
nothing to commit, working directory clean
```

it tells us everything is up to date.
If we want to know what we've done recently,
we can ask Git to show us the project's history using `git log`:

```bash
$ git log
commit f22b25e3233b4645dabd0d81e651fe074bd8e73b
Author: Henry Higgins <profhiggins@oxford.edu>
Date:   Thu Aug 22 09:51:46 2018 -0400

    start notes on Zulu language
```

`git log` lists all commits  made to a repository in reverse chronological order.
The listing for each commit includes
the commit's full identifier
(which starts with the same characters as
the short identifier printed by the `git commit` command earlier),
the commit's author,
when it was created, and the log message Git was given when the commit was created.


Now suppose Prof. Higgins adds more information to the file:
<!--
(Again, we'll edit with `nano` and then `cat` the file to show its contents;
you may use a different editor, and don't need to `cat`.)
-->

```bash
$ nano zulu.txt
$ cat zulu.txt
belongs to the Bantu language family
spoken in South Africa
```

When we run `git status` now,
it tells us that a file it already knows about has been modified:

```bash
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   zulu.txt

no changes added to commit (use "git add" and/or "git commit -a")
```
	
The last line is the key phrase:
"no changes added to commit".
We have changed this file,
but we haven't told Git we will want to save those changes
(which we do with `git add`)
nor have we saved them (which we do with `git commit`).
So let's do that now. It is good practice to always review
our changes before saving them. We do this using `git diff`.
This shows us the differences between the current state
of the file and the most recently saved version:

```bash
$ git diff
diff --git a/zulu.txt b/zulu.txt
index df0654a..315bf3a 100644
--- a/zulu.txt
+++ b/zulu.txt
@@ -1 +1,2 @@
 belongs to the Bantu language family
+spoken in South Africa
```

The output is cryptic because
it is actually a series of commands for tools like editors and `patch`
telling them how to reconstruct one file given the other.
If we break it down into pieces:

1.  The first line tells us that Git is producing output similar to the Unix `diff` command
    comparing the old and new versions of the file.
2.  The second line tells exactly which versions of the file
    Git is comparing;
    `df0654a` and `315bf3a` are unique computer-generated labels for those versions.
3.  The third and fourth lines once again show the name of the file being changed.
4.  The remaining lines are the most interesting, they show us the actual differences
    and the lines on which they occur.
    In particular,
    the `+` marker in the first column shows where we added a line.

After reviewing our change, we go for committing:

```bash
$ git commit -m "add region information"
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   zulu.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

Whoops:
Git won't commit because we didn't use `git add` first.
Let's fix that. We add *and then* commit:

```bash
$ git add zulu.txt
$ git commit -m "add region information"
[master 34961b1] add region information
 1 file changed, 1 insertion(+)
```

Git insists that we add files to the set we want to commit
before actually committing anything. This allows us to commit our
changes in stages and capture changes in logical portions rather than
only large batches.
For example, suppose we're adding a few citations to relevant research to our thesis.
We might want to commit those additions,
and the corresponding bibliography entries,
but *not* commit some of our work drafting the conclusion
(which we haven't finished yet).

To allow for this,
Git has a special **staging area**
where it keeps track of things that have been added to
the current **changeset** but not yet committed. 
If you think of Git as taking snapshots of changes over the life of a project,
`git add` specifies *what* will go in a snapshot
(putting things in the staging area),
and `git commit` then *actually takes* the snapshot, and
 makes a permanent record of it (as a commit). An illustration: 

<!-- 
> ### Staging Area
>
> If you think of Git as taking snapshots of changes over the life of a project,
> `git add` specifies *what* will go in a snapshot
> (putting things in the staging area),
> and `git commit` then *actually takes* the snapshot, and
> makes a permanent record of it (as a commit).
> If you don't have anything staged when you type `git commit`,
> Git will prompt you to use `git commit -a` or `git commit --all`,
> which is kind of like gathering *everyone* for the picture!
> However, it's almost always better to
> explicitly add things to the staging area, because you might
> commit changes you forgot you made. 
-->

<img src="http://swcarpentry.github.io/git-novice/fig/git-committing.svg">



## A Commit Workflow

Let's watch as our changes to a file move from our editor
to the staging area and into long-term storage.
First, we'll add another line to the file:

```bash
$ nano zulu.txt
$ cat zulu.txt
belongs to the Bantu language family
spoken in South Africa
word order: SVO
```

Then see what's changed: 
```bash
$ git diff
diff --git a/zulu.txt b/zulu.txt
index 315bf3a..b36abfd 100644
--- a/zulu.txt
+++ b/zulu.txt
@@ -1,2 +1,3 @@
 belongs to the Bantu language family
 spoken in South Africa
+word order: SVO
```

So far, so good:
we've added one line to the end of the file
(shown with a `+` in the first column).
Now let's put that change in the staging area
and see what `git diff` reports:

```bash
$ git add zulu.txt
$ git diff
```

There is no output!
As far as Git can tell,
there's no difference between what it's been asked to save permanently
and what's currently in the directory.
However, if we use the `--staged` flag:

```bash
$ git diff --staged
diff --git a/zulu.txt b/zulu.txt
index 315bf3a..b36abfd 100644
--- a/zulu.txt
+++ b/zulu.txt
@@ -1,2 +1,3 @@
 belongs to the Bantu language family
 spoken in South Africa
+word order: SVO
```

it shows us the difference between
the last committed change
and what's in the staging area.
Let's save our changes:

```bash
$ git commit -m "add word order info"
[master 005937f] add word order info
 1 file changed, 1 insertion(+)
```

check our status:

```bash
$ git status
On branch master
nothing to commit, working directory clean
```

and look at the history of what we've done so far:

```bash
$ git log
commit 005937fbe2a98fb83f0ade869025dc2636b4dad5
Author: Henry Higgins <profhiggins@oxford.edu>
Date:   Thu Aug 22 10:14:07 2018 -0400

    add word order info

commit 34961b159c27df3b475cfe4415d94a6d1fcd064d
Author: Henry Higgins <profhiggins@oxford.edu>
Date:   Thu Aug 22 10:07:21 2018 -0400

    add region information

commit f22b25e3233b4645dabd0d81e651fe074bd8e73b
Author: Henry Higgins <profhiggins@oxford.edu>
Date:   Thu Aug 22 09:51:46 2018 -0400

    start notes on zulu language
```


## Exploring History 

As we saw in the previous lesson, we can refer to commits by their
identifiers.  You can refer to the _most recent commit_ of the working
directory by using the identifier `HEAD`.

We've been adding one line at a time to `zulu.txt`, so it's easy to track our
progress by looking, so let's do that using our `HEAD`s.  Before we start,
let's make a change to `zulu.txt`, adding yet another line which unfortunately contains misinformation:

```bash
$ nano zulu.txt
$ cat zulu.txt
belongs to the Bantu language family
spoken in South Africa
word order: SVO
a close relative of Spanish
```

Now, let's see what we get.

```bash
$ git diff HEAD zulu.txt
diff --git a/zulu.txt b/zulu.txt
index b36abfd..0848c8d 100644
--- a/zulu.txt
+++ b/zulu.txt
@@ -1,3 +1,4 @@
 belongs to the Bantu language family
 spoken in South Africa
 word order: SVO
+a close relative of Spanish
```

which is the same as what you would get if you leave out `HEAD`.  The
real goodness in all this is when you can refer to previous commits.  We do
that by adding `~1` to refer to the commit one before `HEAD`.

```bash
$ git diff HEAD~1 zulu.txt
```

If we want to see the differences between older commits we can use `git diff`
again, but with the notation `HEAD~1`, `HEAD~2`, and so on, to refer to them:


```bash
$ git diff HEAD~2 zulu.txt
diff --git a/zulu.txt b/zulu.txt
index df0654a..b36abfd 100644
--- a/zulu.txt
+++ b/zulu.txt
@@ -1 +1,4 @@
 belongs to the Bantu language family
+spoken in South Africa
+word order: SVO
+a close relative of Spanish
```

We could also use `git show` which shows us what changes we made at an older commit as well as the commit message, rather than the _differences_ between a commit and our working directory that we see by using `git diff`.

```bash
$ git show HEAD~2 zulu.txt
commit 34961b159c27df3b475cfe4415d94a6d1fcd064d
Author: Henry Higgins <profhiggins@oxford.edu>
Date:   Thu Aug 22 10:07:21 2013 -0400

    start notes on zulu

diff --git a/zulu.txt b/zulu.txt
new file mode 100644
index 0000000..df0654a
--- /dev/null
+++ b/zulu.txt
@@ -0,0 +1 @@
+belongs to the Bantu language family
```

In this way,
we can build up a chain of commits.
The most recent end of the chain is referred to as `HEAD`;
we can refer to previous commits using the `~` notation,
so `HEAD~1`
means "the previous commit",
while `HEAD~123` goes back 123 commits from where we are now.

<!-- 
We can also refer to commits using
those long strings of digits and letters
that `git log` displays.
These are unique IDs for the changes,
and "unique" really does mean unique:
every change to any set of files on any computer
has a unique 40-character identifier.
Our first commit was given the ID
`f22b25e3233b4645dabd0d81e651fe074bd8e73b`. Instead of forcing us to type in the full 40 characters, though, Git mercifully lets us use the first few characters: 

```bash
$ git diff f22b25e zulu.txt
diff --git a/zulu.txt b/zulu.txt
index df0654a..93a3e13 100644
--- a/zulu.txt
+++ b/zulu.txt
@@ -1 +1,4 @@
 belongs to the Bantu language family
+spoken in South Africa
+word order: SVO
+a close relative of Spanish
```
-->

All right! So
we can save changes to files and see what we've changed—now how
can we restore older versions of things?
Let's suppose we change our mind about the last update to
`zulu.txt`, about its relation to Spanish, which turns out incorrect. 
Checking `git status` tells us that the file has been changed,
but those changes haven't been staged:

```bash
$ git status
On branch master
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git checkout -- <file>..." to discard changes in working directory)

	modified:   zulu.txt

no changes added to commit (use "git add" and/or "git commit -a")
```

We can put things back the way they were
by simply using `git checkout`:

```bash
$ git checkout HEAD zulu.txt
$ cat zulu.txt
belongs to the Bantu language family
spoken in South Africa
word order: SVO
```

As you might guess from its name,
`git checkout` checks out (i.e., restores) an old version of a file.
In this case,
we're telling Git that we want to recover the version of the file recorded in `HEAD`,
which is the last saved commit.
If we want to go back even further,
we can use a commit identifier instead:

```bash
$ git checkout f22b25e zulu.txt
$ cat zulu.txt
belongs to the Bantu language family
```


```bash
$ git status
# On branch master
Changes to be committed:
  (use "git reset HEAD <file>..." to unstage)
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#
#	modified:   zulu.txt
#
no changes added to commit (use "git add" and/or "git commit -a")
```


Notice that the changes are on the staging area.
Again, we can put things back the way they were
by using `git checkout`:

```bash
$ git checkout HEAD zulu.txt
```



## Ignoring Things


What if we have files that we do not want Git to track for us,
like backup files created by our editor
or intermediate files created during data analysis?
Let's create a few dummy files:

```bash
$ mkdir results
$ touch a.dat b.dat c.dat results/a.out results/b.out
```

and see what Git says:

```bash
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	a.dat
	b.dat
	c.dat
	results/
nothing added to commit but untracked files present (use "git add" to track)
```

Putting these files under version control would be a waste of disk space.
What's worse,
having them all listed could distract us from changes that actually matter,
so let's tell Git to ignore them.

We do this by creating a file in the root directory of our project called `.gitignore`:

```bash
$ nano .gitignore
$ cat .gitignore
*.dat
results/
```

These patterns tell Git to ignore any file whose name ends in `.dat`
and everything in the `results` directory.
(If any of these files were already being tracked,
Git would continue to track them.)

Once we have created this file,
the output of `git status` is much cleaner:

```bash
$ git status
On branch master
Untracked files:
  (use "git add <file>..." to include in what will be committed)

	.gitignore
nothing added to commit but untracked files present (use "git add" to track)
```

The only thing Git notices now is the newly-created `.gitignore` file.
You might think we wouldn't want to track it,
but everyone we're sharing our repository with will probably want to ignore
the same things that we're ignoring.
Let's add and commit `.gitignore`:

```bash
$ git add .gitignore
$ git commit -m "Ignore data files and the results folder."
$ git status
# On branch master
nothing to commit, working directory clean
```

As a matter of fact, the workshop's repository has its own `.gitignore` file, which [is found here](.gitignore). You will see `.ipynb_checkpoints` and other common OS configuration files. 




