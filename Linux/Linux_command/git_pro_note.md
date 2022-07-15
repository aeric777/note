# Git Pro

> 2021.11.22

## ⅠBefore You Getting Start


    Git is a kind of Distributed Version contral system(DVCSs). Besides ,other kind of Version Contral  System is Centralized Version Contral System.
    Git is more like a stream of snapshots which nearly evrey operation is **Local**.
    Git uses SHA-1 hash(`40-character` string composed of `hexadecimal characters`) and stores everything is its datebase by the hash value of its contents.
    Three States:
    **modified, staged and commited**

## ⅡGetting Started

### **git config**
- `[path]/etc/gitconfig` file for all the user in the system
- `~/.gitconfig` or `~/.config/git/config` for a specific user
- `.git/config` file in a Git directory only for  a specific repo
    You can view all of your settings and where they are coming from using:
```
$ git config --list --show-origin
```

#### Prevent asking for code every time 
```
git config --global credential.helper cache
```


#### Your Identity
```
git config --global user.name "[name]"
git config --global user.email "[email]"
```

#### Your Editor
```
git config --global user.editor "[editor](point out the full path on Windows OS)"
```

#### Your default branch name
```
git config --global init.defaultBranch main(used to be master)
```

### Check Your Setting
```
git config --global --list      # check --global configuration
git config --list
```

## Ⅲ**Git Basic**
    you can obtian a git repository in two ways:
1. take a local directory that is not under version contral yet, and then turn it into a git repository.
2. clone an existing repository form elsewhere.

### **Initializing a Repository**

``` bash
git init            # initial a git repo
git add <filename>(--all)
git add LiCENSE     # optional
git commit -m "[commitment]"
```

### **Clone An Existing Repo**
``` bash
git clone <url> [specify name]  # use https or ssh
```

### Recording Changes to the Repository
    Remember that each file in your working directory can be in one of two states: ``tracked` or `untracked`

#### check tht status of your file
```
git status

git status -s   # short
# arent's tracked   with  ??
# has been added    with  A
# has been modified with  M
# modefied and staged and modified again with MM
```

#### Tracking New Files
```
git add
```
    When you `git commit` the file you commit remain the version that just the moment your ran `git add <filename>`.


#### Ignoring File
Example:
```
# ignore all .a files
*.a

# but do track lib.a, even though you're ignoring .a files above
!lib.a

# only ignore the TODO file in the current directory, not subdir/TODO
/TODO

# ignore all files in any directory named build
build/

# ignore doc/notes.txt, but not doc/server/arch.txt
doc/*.txt

# ignore all .pdf files in the doc/ directory and any of its subdirectories
doc/**/*.pdf
```
See [here](https://github.com/github/gitignore) for more example.


#### Viewing Your Staged and Unstaged Changes
    `git diff` by itself show you only changes that are unstaged yet.
    While you can use `git diff --staged ` to view the changes 


### Commit Your Change
``` bash
git commit

git commit -m "[commit message]"

git commit -v   # show the changes you have made
```
    Remember that the commit rcords a snapshot only those file you set up in your `stagin aera`, and anything you didn’t stage is still sitting there being in state of `modified`.


#### Skipping the Staging Area
```
commit -a <filename>  //you don't need add an unstaged file into staging area and then run git commit 
```

#### Remove File

    Difference between `git rm` & `rm`
    use `-f`  flag to force the removal

    To keeping the file on your working tree but remove it from your staging area.
```
git rm --cached <filename>
```

#### Rename File
```
git mv <old file_name> <new file_name>
```

### View The Commit History
```
git log
```
    usefull flag: 
`-[number]` show you limit the number of log entires displaied.
`-p` shows your the details of each patch
`--all`
`--graph`
`--oneline`
`--decorate`
`--name-only`
`--pretty`

### Undoing Things
```
git commit --amend  //reset the last commit
```
```
git restore --staged <filename> //unstage staged file
git restore <filename> //unstage staged file    //discard the change you have made
```

### Working With Remote
```
git remote      //show the current remote
git remote -v     //more  details
git remote show [remote-name]       //show more information about one particular remote
```
    Add remote
```
1. git clone <url>  //automaticlly add a remote origin 
git clone -o [remote name] <url>
2. git remote add [name] <url>  //add remote repository
```
    Fetch remote information 
```
git fetch [remote name]
```
    pull and push with remote
```
git pull [remote] [branch]
git push [remote] [branch]
```
    Rename and removing remote
```
git remote rename [oldname] [newname]
git remote remove [remote name]
```


### Tags
    Listing tags
```
git tag
```
    Creating Tags : `lightweight` or `annotated` tag
    Anotated Tags:
```
git tag -a [tag name] -m "tag message"
```
    Lightweight Tags:
```
git tag [tagname]-Lw
```

#### Add Tags Later
```
git tag -a [tagname]  [hash value] 
```

#### Push Tags To the　Remote 
```
git push [remote name] [tagname]    //push single tag
git push [remote name] --tags       //push all tags
```

#### Deleting Tags
```
git tag -d [tag name]   //delete local tag
git push [remote name] --delete [tagname]   //delete tag on remote server
```

### Git Alias
```
git config --global alias.[short name] 'full command'
```

## Ⅳ**Git Branching**

### Branch Manegement

#### Creating new branch 
```
git branch [mame]
```

#### Switching Branch
```
git checkout [branch]       //Move pointer `HEAD` to a specifeid branch
git checkout -b [branch]    //creat new branch
```
```
//use switch 
git switch [branch]     //same as "git checkout [branch]"
git switch -c [branch]  //same as "git checkout -b [branch]"
git switch -            //new functionality
```

#### Branch Merging
    clea your waoking tree before merge!!!
```
git merge       //git use three merge as below:
1.fast-forward          //don't creat new snapshot
2.'recursive' strategy  //creat new commit(snapshot)
3.conflict resolve      //only when Automatic merge failed
```

```
// show Branch
git branch --merged
git branch --no-merged

//delete Branch
git branch -d [branch name]
git branch -D [branch name]     //force
```


#### **Changing Branch Name**
    Make sure the working tree is clean begfore change the name of your branch (*local mechine & remote*)
```
git branch --move [old name] [new name]     //change name locally
git push --set-upstream [remote name] [branch name] //change to remote
//Note that you can check the current branch with "git branch --all" command 
git push [remote name] --delete [branch name which to be deleted]   //delte useless branch
```
    How to make sure that your working tree is clean when you are in cooperation with colleague

> - Any projects that depend on this one will need to update their code and/or configuration.

> - Update any test-runner configuration files.

> - Adjust build and release scripts.

> - Redirect settings on your repo host for things like the repo’s default branch, merge rules, and other things that match branch names.

> - Update references to the old branch in documentation.

> - Close or merge any pull requests that target the old branch.

### Branching Workflows
#### Long Running Branch
    Keep one stable version on branch master, developping on other branch

#### Topic Branches

### Remote Branches

#### Tracking Branches
    Tracking branches are local branches that have direct relationship to a remote branch.
```
git checkout -b [new branch] [remote]/[tracking branch name]
```
    Change the upstraeam branch you are tracking.
```
1.git push -u [remote]/[branch]
2.git push --set-upstream-to [remote]/[branch]
```
    `git branch -vv` list out all the branch and which branch they are tracking.
    What's more we usually use
```
git fetch --all ; git branch -vv
```

#### Pulling
    `Git fetch` fetch all the commit on the server that you don't have, but won't modify you working area. You need to`git merge` command to bring this change to your working directory.
    While there is another command to achieve the same thing
```
git pull
```
    but sometime this can be confusing.

### Rebasing

#### Basic Rebasing
    Take all the changes that ware committed on one branch and replay them on a different branch.
    **Note that: Don't rebase commit that exit outside your repository and that peopkle may have based work on.**
    **Fllowing this tips:Rebase local changes before pushing to clean up your work, but never rebase anything that you've pushed somewhere else.**
```
git rebase [base branch] [topic branch] //check the topic branch for you and replay it onto the base branch.
git checkout [base branch]
git merge [topic branch]
git branch -d [topic branch]    //make your git history clean enough
```
```
git checkout [side branch]
git rebase [main branch]

git checkout [main branch]
git merge [side branch]
```