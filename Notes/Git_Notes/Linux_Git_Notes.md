# ***Important Notes***

## LINUX / GIT BASH COMMANDS

### DELETE FILE
`rm -rf fileName`

### MAKE DIRECTORY
`mkdir folderName`

### CHANGE DIRECTORY
`cd foldername`

### OPEN FILE IN VI EDITOR
`vi filename.txt`
* `:wq` to save and quit
* `:w` to save
* `i `to insert mode for typing
* esc to control mode

### READ FILE
`cat filename.txt`

### SEE GIT FOLDERS FILES WHICH ARE HIDDEN
`ls .git`

## ***GIT COMMANDS***

### BASIC COMMANDS 
```
git status
git help config
git add filename.txt
git commit -m "Message"
```

### TO UNSTAGE (UNADD) A STAGED(ADDED) FILE
`git add filename.txt` &nbsp;&nbsp;&nbsp;&nbsp; Stages the file for commit

`git restore --staged names.txt`   


### GIT HISTORY
`git log`


### DELETING A FILE 
`rm -rf filename`
##### Now file gets deleted, but not tracked. Make it tracked/staged by:
`git add filename.txt`     OR    `git add .`    (`.` means all changes)


### STASHING
* All changes made is moved to backstage but not committed. Later we can bring it back

    `git stash`


* TO BRING BACK THE STASHED ONES, USE THIS

    `git stash pop`


* ELSE IF TO DELETE/DISCARD THIS STASHED ONE, USE THIS

    `git stash clear`


### LINKING REMOTE REPO TO THIS LOCAL REPO
`git remote add origin https://github.com/mygitaccountname/my-test-repo.git`

remote means dealing with url, add means adding a new url, origin is the name of the url like contact name in phone


### SHOW ALL URLS ATTACHED TO THIS FOLDER
`git remote -v`

> Output:
> 
> origin  `https://github.com/mygitaccountname/my-test-repo.git` (fetch)
> origin  `https://github.com/mygitaccountname/my-test-repo.git` (push)


### PUSHING TO REMOTE REPO
`git push origin master`

to which repo url?-> origin,  &nbsp;&nbsp; to which branch?-->master   



### EXPLANATION FOR DIFFERENT GIT HIDDEN FILES AND FOLDERS
 HEAD --> HEAD is a pointer to a branch (current branch) which says all the new commits added will be
done on head ie to current branch


### GIT BRANCH
`git branch branchname`
`git checkout branchname`


### HOW TO GET SOMEONE ELSE PROJECT TO YOUR ACCOUNT ---> FORK
> select fork in github, select your account

### CLONNING EXISTING REPO
`git clone <url>`

### UPSTREAM IS THE NAME OF ORIGINAL REPO
`git remote add upstream <url of the original forked repo>`
> DO git remote -v to check this

### REMOVING A COMMIT IN PULL REQUEST
`git restore <id>`
`git add .`
`git stash`

Now Force Push changes
`git push origin branchname -f`


### GETTING LATEST CODE PULL FROM UPSTREAM
`git checkout main`
`git fetch --all --prune`

all means all branches, prune means even the deleted ones
git reset --hard upstream/main

OR

fetch and reset can be done with single command PULL
`git pull upstream main`

### HOW TO MAKE MUTLIPLE COMMITS TO SINGLE COMMIT
* Reset the bottom commit id above which has say 4 comits
* now 4 commits above it get unstaged
* add and commit it using single commit

OR

* USING REBASE TO SQUASH AND PICK
`git rebase -i <commit id whose above commits are considered>`

i means interactive. Now it gives a menu

>pick 64d4s546gss49 commit message 1
> 
>s d454545d545457 commit message 2
>
>s 5464d645s46ds4d8 commit message 3
>
>pick dsfs445654545f commit message 4
> 
Here second and third one we changed to squash. So it will be 
committed along with top pick one
so total 2 commits
commit 1 has 1,2,3,
commit 2 has 4
* NOW PRESS esc + :x enter
* Now it allows to enter commit message enter it
* i for insert mode, enter message, esc + :x


