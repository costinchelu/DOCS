# VERSION CONTROL (GIT)

### 3 STAGES OF A FILE:
**I ) COMMITED** – data is stored in local database  
**II ) MODIFIED** – when file contents is changed  
**III ) STAGED** – changes are made and about to be commited  

### 3 STAGES OF A GIT PROJECT:

**I ) WORKING DIRECTORY**  
Single copy (checkout) of a version of the project. Files are pulled from GIT database.
Files that are not yet been added to the stage area for commit.

**II ) STAGING AREA (INDEX)**  
Area that sits between working and .git directory. Used for changes so when commit, then only files from the staging area are commited.
Files modified and added to be commited in the next snapshot.

**III ) .GIT DIRECTORY (REPOSITORY)**  
Files in GIT database.
Files recorded as version snapshot.

### CONFIGURATIONS 

`git config --global core.autocrlf true`
 = Configure Git on Windows to properly handle line endings

### COMMANDS

`pwd` = print working directory  
`cd` = change directory  
`cd..` = up to main  
`cd\` = up to main (C:\>)  
`dir` = list files (for Linux: ls)  
`copy con` = new empty file (for Linux: touch)  
`mkdir` = new empty folder  
`clear` = clear screen  
`man git` = git manual  
`git help <instruction>` = get help for a specific instruction  

### CREATING A GITHUB REPOSITORY

Options for creating the repository:  
`add.gitignore` = git will ignore all files with listed extensions that are in the repository (usually large files, or project configurations files). Extensions will be written in the .gitignore file.
Adding a licence (licence files)
Initialise repository with a readme.me file

### INITIALISING A NEW REPOSITORY (ON LOCAL)

`git init` = a new repository is initialised in the current directory  
`echo` *“#github_repo_name”* >> `README.md` = to add the README .me to the project  
`git clone <link>` = clone an online repository on a local drive.   
Links from github can be pasted with shift+insert  
`git add.` = add files to the staging area  
`git add -A` = (A = all) add all files that had been modified or added to the repository (similar with `git add .` )  
`git commit -m` “here description or/and name of the commit is written” = commits and posts a message for the commit  
`git commit -a` = automatically commits changes to files tracked by git  
`git commit --amend` = overwrites last commit with changes made now  
`git revert <hash  of  a  previous  commit>` = revert changes to the commit selected (by hash)  
`git remote show origin` = shows info about connection of the local repository with a remote repository on another computer  
`git remote add origin` *pasted_link_of_the_github_project* = adds the origin github repository to our local repository by creating a link that allows us to push or pull changes between the two  

(local <<--link-->> github)

`git push -u origin master` = to push files of the project to github server on master branch  

On creating a repo, github creates a branch named master. So when the local master branch is up to date with the origin/master branch on github server.

### TAGS

`git tag` = view all the tags in the project history.  
There are two types of tags: lightweight, adnotated.  
`git tag` *“tag_name”* = for creating a light tag  
`git tag -a` *“tag_name”* `-m` *“message”* = for creating an adnotated tag  
`git show` *“tag_name”* = for viewing commit assigned with a tag  

### LOGS

`git status` = shows the state of the project (
M = modified,
A = new file staged
?? = new file untracked )

`git status -s` = silent mode status

When creating a new file we can add it to the tracked file by using the command `git add` *file_name*

A file can be in two states in the same time. For example, we can modify it (in this case, the file becomes “not staged”) and after we add it to be staged, we can modify it again.

`git log` = list commits made until now (to limit displaying all commits we can use git log -5 (for example - in this case only the last 5 commits will be displayed).  
For all, we can scroll screen up & down with J & K keys. To exit press q.

`git log --online` = short log of commits  
`git log –-stat` = detailed view  
`git log -p` = shows differences made in each commit  
`git log --oneline -–decorate` = shows a short presentation of each commit  
`git log --since “2 months”` = shows only commits made in the last 2 months. We can use also “*from*” & “*until*”.  
`git log --graph` = shows commits in a graphical format (useful for branching)  
`git diff` = shows differences in files that are not yet staged  
`git config –list` = check out git configuration  

`cat ~/.gitconfig` = to read the .gitconfig file  

### BRANCHES

`git checkout -b` *new_branch_name* = creates a new branch from current branch and moves the „head” pointer to the new branch (checkout).   
That means - new commits will get on the new branch  
`git checkout` *branch_name* = changes current branch  
`git branch` *new_branch_name* = when we only want to create the new branch (without checking out to it)  
`git branch -d` *branch_name* = deletes branch specified by branch name  
`git rebase` = gets all content and commits from a secondary branch, on top of the master commits.   
This is useful when changes in the secondary branch are very important and we want to take the new route, leaving master behind and also on master new changes are not useful. After the rebase, we have to merge the new branch to master.  
`git rebase master` = is made when we are in the secondary branch then `git merge` *new_branch*

### FORKing

We have access to repositories and can contribute by having our own version of them to work with.   
Later we can request merging changes to the main branch.   
When forking a project on Github, we wil copy project contents to own repo.

To keep the fork up-to-date, we want to add the original repo as a remote to our local repo.   
For that we will get to the page of the original repo and copy the URL to the project:  
`git remote add` *<chosen  name  /  upstream>  < link >*  
`git fetch upstream` = To get the updates from the upstream  

### STASH

`git stash` = will save working directory and index state to a stash area to be kept until we will decide where to put changes  
`git stash pop` = will extract changes from stash to working area  
`git stash list` or `git stash show` = will display the contents of the stash  
`git merge` *branch_name* = this will merge contents of branch_name to master branch  
`git reset` = used only when we don't want to push commits further into git (get back to working directory)  
`git reset --soft` = gets commits back into staging area  
`git reset --hard` = gets them all deleted (only when we don't need changes)  
`git reset --soft HEAD~5` = squashes the last 5 commits to just one. Useful when the last commits practically tries to fix or make one problem and are very similar in nature, and we want to get just one commit to reduce clutter in the log.


