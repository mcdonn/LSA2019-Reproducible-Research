# Software Installation Guide

We need three software components: [**git**](#git-and-github), [**R**](#r-and-r-studio) and [**Python 3**](#python-3). The Python component also require two add-ons: **Jupyter Notebook** and **NLTK**. 


### Troubleshooting
If you run into problems, please:
- Email the instructors. Note your OS (Windows? Mac?) and give us a description of how and where you are stuck. Screenshots work wonders. 
- On the workshop day, arrive early at 8:30am. The instructors will be ready to get hands-on with your laptop. 


## git and GitHub 
- Install `git` from [https://git-scm.com/downloads](https://git-scm.com/downloads).
  - We don't need GUI clients: there is no need to install one. 
  - (Windows users only) Choose the 64-bit version unless you know your system can only handle 32-bit. 
  - Default editor: ([Screenshot](img/git_setup1.png)) You don't want to use Vim! Choose your favorite editor in the drop-down menu (Sublime Text, Notepad++, Atom, etc.) if you already have one installed. If you are not sure, pick Nano.  
  - (Windows users only) Line ending conversions: ([Screenshot](img/git_setup2.png)) Choose the "Checkout as-is, commit Unix-style line endings" option. 
  - For all other options, the default setting should work best for most users.   

### Signing up for a GitHub Account
<img src='img/Octocat.png' align=right>

GitHub accounts has different types of accounts. The free account allows you to create public repositories and collaborate with others, but you *cannot* create private repository that only you and your collaborators can view. This requires a paid 'developer' account. However, there's good news for eductors! GitHub offers educators two years free for these developer accounts, you simply need to apply and use your educational (.edu) email address. Follow these steps to sign up for GitHub and apply for the educational discount: 

1. Go to [https://github.com](https://github.com)
	- Create a username, supply an email (best to use .edu email) and password.
	- Choose the Free account and click Continue and then Submit
	- You now have a GitHub account

1. To apply for the educational discount, go to [https://education.github.com/](https://education.github.com/)
	- Click on **Join GitHub Education** in the upper right corner
	- Fill out the questions (select Individual account for question 2) and click Next
	- Then fill out your name, university issued email address, name of school, and a brief description of how you plan to use GitHub.
	- Click Submit request and GitHub will email instructions for the rest of the process.

## Python 3

There are a LOT of Python distributions and therefore many ways to install Python. Two recommended options:

- If you are completely new to Python, you should install Anaconda Python. It includes all necessary Python add-ons. ([OPTION 1](#option-1-install-everything-through-anaconda)) 
- If you already have a working copy of Python 3 on your machine, you can install Jupyter Notebook and NLTK separately via `pip`. Recommended for advanced users. ([OPTION 2](#option-2-already-have-python-add-on-components-separately)) 

###  OPTION 1: Install everything through Anaconda 
<img src='img/anaconda_logo.png' align=right>

Anaconda has the advantage of already including popular scientific libraries such as NLTK. It also includes the Jupyter Notebook interface. 
<!-- (The downside is that it also installs lots of things you might never need.) -->

- Go to Anaconda Python's download page: [http://www.anaconda.com/download/](http://www.anaconda.com/download/) Current version is **5.3.1**. 
- Make sure you download and install the **Python 3.7 version**. Important!
- 64-bit vs. 32-bit: if your system can handle it (most modern systems can), we recommend 64-bit. 
- Double-click the downloaded setup file to start the installation process. Details:
   - The setup file is 600MB; You will need 3GB of space on your hard drive.
   - Ignore away: a question about installing Visual Studio Code, a "Get the cheat sheet" dialog box popping up asking for your email, and a message about signing up for Anaconda Cloud. 
   - The default settings and options should work fine for most of you.   
- Depending on your system, Anaconda may take a while to install. Once it finishes, check your installation: 
   - Find Anaconda Navigator in your start menu (or Applications folder on Mac), launch it
   - Launch Jupyter Notebook
   - Jupyter opens up as a tab in your browser (Safari, Chrome, FireFox, etc.). You should be able to see your personal folders such as `Desktop` and `Documents`. 

### OPTION 2: Already have Python, add on components separately
<img src='img/python_jupyter_nltk.w200.png' align=right>

If you already have a working copy of Python 3 on your machine (perhaps you installed [python.org](https://www.python.org/) version of Python at some point), then you have a choice:

1. Keep your existing Python copy, and install the Anaconda version separately. Both copies of Python will work independently. To go with this option, follow the [Anaconda installation instructions above](#option-1-install-everything-through-anaconda). 
1. Add NLTK and Jupyter Notebook to your existing Python 3. This is a sensible thing to do! Follow the instructions below. It assumes you are familiar with `pip`.  
    - In your console window (`cmd` for Windows, `Terminal` for Mac), use `pip3` to install the two add-on components: 
	- Install NLTK: `pip3 install nltk`
	- Install Jupyter Notebook: `pip3 install jupyter`
    - If it did not work, `pip3` is not in your system's path. Google for solutions or install Anaconda instead. 
    - If installation went fine, verify your setup: 
         - In your console, use the command`jupyter notebook` to launch jupyter. It will open a tab in your default browser. 
	     - On the right-hand side, click on "New", choose "Python 3". Another tab will open up. 
	     - In the top cell, type in `import nltk`, and then hit the play ▶ button on top. 
         - If there is no error message, your installation was successful.
  
## R and R Studio
There are two options for installing R and RStudio. <img src='img/r-logo.png' align=right>

1. If you plan to install Python 3 with Anaconda, you can simply Install R and RStudio using Anaconda Navigator **(Choose Option 1)**. <img src='img/rstudio-logo-flat.png' align=right>

2. However, if you don't plan to install Anaconda, it's quite simple to install R and RStudio  **(Choose Option 2)**. 



### OPTION 1: Install RStudio as a part of Anaconda
Anaconda doesn't install RStudio by default, so you need to install it. Luckily, it's quite simple. 

- In the Anaconda Navigator window, click Install RStudio (1.1.456 version)
- It will take some time to install, there's a progress bar in the lower right corner to show it's working
- You may also be asked to update Anaconda Navigator; it's okay to install and relaunch
- Lauch RStudio and desktop app will open

### OPTION 2: Install R and RStudio 
R and RStudio are downloaded and installed separately. 

1. Download R from [https://cran.r-project.org/](https://cran.r-project.org/) 
	- Select the appropriate version of R for your machine, which takes you to another page
	- **Mac Users:** 
		- Under the heading *Latest Release* download **R-3.5.1.pkg** and run the installer
		-  It is also a good idea to download and install XQuartz ([https://www.xquartz.org/](https://www.xquartz.org/))
	- **Windows Users:** 
		- Under the heading *Subdirectories* select **base**
		- Then, select **Download R 3.5.1 for Windows** and run the installer
1. Download [R Studio](https://www.rstudio.com) from [https://www.rstudio.com/products/rstudio/download/](https://www.rstudio.com/products/rstudio/download/)
	- Select the *free* download and choose the appropriate installer for your machine
	- Run the installers 
	- **Mac Users** simply drag the RStudio.app file into your Applications folder

