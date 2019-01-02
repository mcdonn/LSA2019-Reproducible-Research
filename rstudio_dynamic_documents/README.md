# RStudio & Dynamic documents with R Markdown


## Connecting Rstudio and GitHub
We will connect RStudio and GitHub using an SSH key, so that you do not have enter your username and password every time you sign in to your account. We will follow instructions from the book [Happy Git and GitHub for the useR
](http://happygitwithr.com/). We'll specifically look at sections [12.3.1](http://happygitwithr.com/ssh-keys.html#option-1-set-up-from-rstudio), [12.4.1](http://happygitwithr.com/ssh-keys.html#option-1-set-up-from-rstudio), [12.5.3](http://happygitwithr.com/ssh-keys.html#on-github). If we run into issues with your computer, we can look in these sections for answers.


### In RStudio

- Step 1: In RStudio, Go to *Tools > Global Options…> Git/SVN*
- Step 2: Click *Enable version control interface for RStudio projects*
- Step 3: Under `SSH RSA Key`, click *Create RSA Key...* <br/> (It will ask you for a passphrase, but let's skip that for the time being.)
- Step 4: Once the key is created click *View public key*
- Step 5: Copy the key.

### In GitHub

- Step 6: Click on your profile picture in the upper right corner and choose to *Settings* from the dropdown menu
- Step 7: In the pane on the lefthand side click on *SSH and GPG keys*. 
- Step 8: Click *New SSH key* in the upper right corner. 
- Step 9: Provide an informative title for your public key (e.g., computer model-year)
- Step 10: Paste the public key you copied from Rstudio in the *Key* box. 
- Step 11: Finally, click *Add SSH key*.

# Getting started with your own repo

## In GitHub

- Create a new repo in GitHub by clicking on your profile picture in the upper right corner and choose to *Your repositories* from the dropdown menu
- You'll see a list of your repositories. Click on the green *New* button in the upper right corner.
- Give your repository a name (e.g., lsa2019-workshop-practice), make it private (if possible). **Do not click any other boxes.**
- Click the green button *Create repository* at the bottom of the page.
- Under the *Quick setup* heading, copy the URL of your repo. You'll need it for the next steps in RStudio.

## In RStudio
- Open RStudio, and in the upper right corner, click on *Project: (None)* and select *New Project...*
- A pop up will appear and select *Version Control*, then select *git* 
- Paste your GitHub repo URL in the box that says *Repository URL* and choose the directory where you would like the project to be stored locally on your computer. 
- Click on *Create project*.

You now have a new project file, and can `pull`, `commit` and `push` changes to your GitHub repo using the `git` tab in pane in the upper right corner.  

# Exercises 
These exercises contain some sample data from a phonetics study and a typological study. The exercises purposely use rather simple r code. The goal of the exercises is for you to feel comfortable using R Markdown and dynamic documents with `knitr`.

Intead of cloning the repo, I recommend downloading the repo and moving the following files and folders from "rstudio\_dynamic\_documents" folder: 

- besemah\_stress.Rmd
- caus\_appl\_syncretism.Rmd
- bib/
- data/ 

You need to install the following packages: 

`install.packages(tidyverse,knitr,kableExtra,leaflet,wesanderson)`


<center>
### You can rely on [this very handy cheatsheet for R Markdown](https://www.rstudio.com/wp-content/uploads/2016/03/rmarkdown-cheatsheet-2.0.pdf).
</center>

*If you're feeling a bit confused or intimadated by all of this, feel free to take some time to look over [this very gentle introduction to R Markdown](https://rmarkdown.rstudio.com/lesson-1.html)

## [Exercise 1: Besemah Stress](phonetics_paper.Rmd)
This is a very basic example of a dynamic document. First, use the `knit` command to compile the document. Then, read through the document and look out for commented sections in between \<!-- and -->. For each of these, I list different tasks to complete throughout the document. I'll be walking around to help you complete these tasks. 


## [Exercise 2: Typology of causatives and applicatives](typology_paper.Rmd)
This is a very basic example of a slides using `knitr` and R Markdown. Again, first use the `knit` command to compile the document. Then, read through the document and look out for commented sections in between \<!-- and -->. For each of these, I list different tasks to complete throughout the document. I'll be walking around to help you complete these tasks.

## Exercise 3: Experimenting on your own
If you have additional time, you can *either* create slides from the document in **Exercise 1** *or* create a document from the slides in **Exercise 2**. I provide a number of links at the end of exercise 2 for you to get some ideas of how you can do even more with dynamic documents.
