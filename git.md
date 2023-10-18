# Git Cheat Sheet

## HEAD: What's a head or detached Head
Read this [article](https://www.cloudbees.com/blog/git-detached-head).

The purpose of HEAD is to keep track of the current point in a Git repo. In other words, HEAD answers the question, “Where am I right now?  
You can find out with
```
$ git log
``
or
$ cat .git/HEAD
```
Most of the time, HEAD points to a branch name. HEAD is synonymous with “the last commit in the current branch.”

But after running git checkout <previous commit>, HEAD is pointing directly to this commit instead of a branch.  
This is the detached HEAD state.

In this state, you can make experimental changes, effectively creating an alternate history, the next commit will be right on top of <previous commit> on a new time line. 
```
$ git log –oneline
```
### Keep the new time line or discard it
To discard it:
```
$ git checkout <branch-name> 
or on newer git
$ git switch <branch-name> 
```
To keep it the make a new branch ot of it
```
$ git branch alt-history (create new local branch)
$ git checkout alt-history (point HEAD to it)
```

## What's Origin

Origin is just a alias for the remote git url.  
We set it up when:
```
$ git remote add origin git@github.com:vuejsprojects/my-electron-app.git
```
We can check it out with:
```
$ cat .git/config
[remote "origin"]
        url = git@github.com:vuejsprojects/my-electron-app.git
        fetch = +refs/heads/*:refs/remotes/origin/*
[branch "main"]
        remote = origin
        merge = refs/heads/main
[branch "dragndrop"]
        remote = origin
        merge = refs/heads/dragndrop
```

## Create a branch

```
$ git branch
```

Creating a repo creates automatically a **master** branch we often want to rename it.
```
$ git init
$ git log
fatal: your current branch 'master' does not have any commits yet

```

### To rename a branch
```
$ git branch -M new-branch-name
```

### List branches
```
$ git branch -l
or
$ git branch
```
### To list remotes as well
```
$ git branch -a
```

## Switch branches
```
$ git checkout <branch-name> 
or on newer git
$ git switch <branch-name> 
```

## Push Branch To Remote

In order to push a Git branch to remote, you need to execute the “git push” command and specify the remote as well as the branch name to be pushed.
```
$ git push <remote> <branch>
```
For example, if you need to push a branch named “feature” to the “origin” remote, you would execute the following query
```
$ git push origin feature
```

If your upstream branch (i.e. remote branch) is not already created, you will need to create it by running the “git push” command with the “-u” option for upstream.
```
git push -u origin feature
```

Push Branch to Another Branch

In some cases, you may want to push your changes to another branch on the remote repository.
```
$ git push <remote> <local_branch>:<remote_name>
```

The remote can be a different repo.
### List repo
To list the remote repos
```
$ git remote -v

origin  https://github.com/user/repo.git (fetch)
origin  https://github.com/user/repo.git (push)
custom  https://github.com/user/custom.git (fetch)
custom  https://github.com/user/custom.git (push)
```

## Delete branch
### Locally
Git will not let you delete the branch you are currently on so you must make sure to checkout a branch that you are NOT deleting.  
For example: git checkout main

Delete a branch with git branch -d <branch>.
```
$ git branch -d fix/authentication
```

### Remotely
The command to delete a branch remotely: git push <remote> --delete <branch>
```
$ git push origin --delete fix/authentication
```

To synchronize your branch list
```
$ git fetch -p
```
The -p flag means "prune". After fetching, branches which no longer exist on the remote will be deleted.

## Delete a commit

Assuming you are sitting on that commit, then this command will wack it...
```
$ git reset --hard HEAD~1
```
The HEAD~1 means the commit before head.

Or, you could look at the output of git log, find the commit id of the commit you want to back up to, and then do this:
```
$ git reset --hard <sha1-commit-id>
```
If you already pushed it, you will need to do a force push to get rid of it.
```
$ git push origin HEAD --force
```



