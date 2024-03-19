# Git and Github notes

## Intro

Very important to fully get down. I do not yet have a full grasp on this yet, but will be working
towards that. Here is a cheat sheet and the basic stuff I have.

### Distinction

Its important to note the distinction between git and github. Git is a version control software
used to locally track the changes. It has a hidden `.git` file that contains version control info (your commits and pushes) Need to learn a 
bit more about this, but that is the working info for now. Github lets you create a remote
repository that you can push your local changes to. This allows for colloboration or an online back up.

## Local to Remote

If we first create the project locally, we go to the root dir of our project and run the following

`cd root_project`

`git init`

This creates a hidden `.git` dir that will store all version control info for project.

You can check it out! In the same directory:

list all hidden files or directorities:

`ls -lah` 

switch to said hidden file (in this case .git):

`cd .git`

Do the `ls` command to see what you can check out! `config` file is a good place to check out.

The other options:

``` bash
COMMIT_EDITMSG  HEAD       branches  description  index  logs     refs
FETCH_HEAD      ORIG_HEAD  config    hooks        info   objects
```

Actually going through this stuff will demystify whats going on behind the scenes. Use the `cat` command to read out some of these files and see if there's anything you can understand.

## Adding files

`git add [file_path]`

Add files for staging which can then be committed.

## Check status

`git status` 

This tells you which files are staged to be committed or if there are unstaged changes.
Will also tell you which branch you are on.

`git commit -m "commit message"`

Commit the changes so that they are ready to be pushed to the remote project.

### change branch name

I like to change branch name from master to main after init

`git branch -m master main`

The format is `-m <original> <new>`

## Set up remote repo

Create remote repo on github website and then go back to local project terminal at root proj dir.

Then you run the following to add a remote depo:
`git remote add origin <remote-url>`

Use the ssh version and make sure to set up ssh key for that. 
I have notes for the ssh keys, make sure to reference that. **Git no longer allows for regular password entry, SSH keys are essential**

# Pull all branches 

This is only if you need to access a different remote branch.

fetch all branches:

`git fetch --all`


list all branches:

`git branch -a` 

now switch to it:

`git checkout <branch-name>`

## Push to remote

`git push origin <branch-name>` 

Now we can push this to the remote project and others can access it or now we have a safe place to keep it.

Can set an upstream branch so all you need to write is git push origin.

`git push upstream <branch-name>`

now pushes to <branch-name> only need to be:

`git push origin`

## Work flow after initial set up

- Work Iteratively, add changes in a way that makes sense for documentation and version control

- Handling Branches / Merging 
	
	- new branches: `git checkout -b <branch-name>`
	
	- switch branches: `git checkout <branch-name>`
	
	- merge branches: `git merge <branch-name`

- Keep commit history descriptive


# Pull all branches

`git fetch --all` 

`git branch -a` // list all branches

//now switch to it

`git checkout <branch-name>`
