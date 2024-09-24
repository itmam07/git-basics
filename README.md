# GIT CHEAT SHEET

<p align="center">Itmam Alam - 24.09.2024</p>

## INSTALLATION

To install git on your PC go to https://git-scm.com and choose your OS. For Windows, after opening the installer just click on all default settings and start the installation.

## SETUP

Open your terminal and try to see if git was installed correctly:

    $ git -v
    
You should get something like: *git version 2.43.0.windows.1*

#### Config

Now we want to set some config data:

    $ git config --global user.name “firstname lastname”
    $ git config --global user.email “email”

So git knows who you are.

#### Optionally

Git repos where (and sometime still are) initially created with a "master" branch. We don't want that sh*t so 

    $ git config --global init.defaultBranch main

This ensures that when you initialize a new git repo on your PC, it has a "main" and not a "master" branch. You will see that in the next section.

# Basics

## Cloning a repo
Cloning a repo means to get a git repository from the web, such as github.com or something. Often when working with different people, you want to work together in the same project. So one creates the repo, which you have to "copy" to your own pc by cloning it.

    $ git clone [url] | [ssh]
    $ git clone git@github.com:itmam07/pos.git
    $ git clone https://github.com/itmam07/pos.git

 

## Creating a repo

For your own projects (SYP, POS) you have to create a git repo. This allows you to for example maintain a clean code history since git tracks all changes to the code over time. It is also ~~a~~ **the** way to collaborate with others regarding software dev.

### Over GitHub*

*or any other code hosting provider like GitLab

Go to the folder where you want to make a new git repo.

    $ cd my-project

Then initialize git

    $ git init
    
> git init:
> This creates a hidden .git folder in your project folder. All
> information that git needs is in that folder. You yourself have to do
> nothing with this folder so forget it.

Now you should be able to use git in that folder. You can add files, track them with git for changes, etc.

    $ echo "# my-project" >> README.md     # create a READMEfile
	$ git add README.md   				   # let git know that it should track this file
	$ git commit -m "intial commit"		   # commit changes

But the thing is it is not synced with any repo on your GitHub account. For that we have to set a **remote origin** for your repo.

So after going through the creation process over on github.com you are now left with a repo name. Let's assume that this repo is called *my-project.*

Then go back to the terminal in your folder:

    $ git remote add origin git@github.com:username/my-project.git
    $ git remote add origin https://github.com/username/my-project.git
    $ git push --set-upstream origin main

For the first commit (and after changing branches) you have to set the "**remote origin**" of your repo. This is so git nows on which branch it should push the changes to, e.g. main, dev, feature etc. 

> Note: There is a way to automate this whole thing:
> $ git config --global --add --bool push.autoSetupRemote true
> after that you don't have to do that --set-upstream thing anymore

In this case the main branch. We will come to branching later. After this first push git nows where to push changes to automatically, so you only have to write **$ git push**.

## STAGING

Staging is the process to tell git to track changes on a specific file. In git there are two stages:

#### Untracked
The file is currently not tracked, and won't be added to the next commit, that means those changes are currently only on your computer. 

> This state always occurs when you create a new file for example hello.txt.

#### Staged
These files are tracked by git and they will be included in the next commit. To get a file  tracked by git use the following command:

    $ git add [file_name]
    $ git add hello.txt

#### Status

You can always view the current status of each file in your folder by simply typing:

    $ git status

**For me, this is THE most important command for git.** It always shows you what you have to stage.

#### Unstaging

Often times you decide that a specific staged file is not necessary for this commit. To unstage this file:

    $ git restore --staged [file]
    $ git restore --staged hello.txt

When you execute $ git status now, you will see that hello.txt is untracked again.

There is another way to unstage, but i don't recommend it since it is meant for another reason (changing commit history) and can potentially cause a **lot** of trouble.

    $ git reset [file]
    $ git reset hello.txt
