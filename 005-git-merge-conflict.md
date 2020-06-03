# Git Merge Conflict

As a developer I want to manage code conflicts so that I know how to manage my code effectively.

## Exercise 

In case there were any changes from the upstream that are not reflected in your local and origin reset your repo. \
* note do this with caution on other projects as it will destroy git history.

```
$ git reset --hard upstream
$ git push origin --all -f
```

### Step One: Fetch all branches 
The git fetch command downloads commits, files, and refs from a remote repository into your local repo. \
You use fetch to see what the rest of your team is working on and to ensure you have all the latest locally. 
```
$ git fetch --all 
```

### Step Two: Review all branches 
Git branch -a will show you all your local and remote branches.
```
$ git branch -a
```

### Step Three: Check out the remote feature branch
To work on our changes locally, check out the remote branch `JIRA-005-merge-conflict`. Then checkout the branch `JIRA-005-merge-conflict-two`

```
$ git checkout -b JIRA-005-merge-conflict-example upstream/JIRA-005-merge-conflict-example
$ git checkout -b JIRA-005-merge-conflict-example-two upstream/JIRA-005-merge-conflict-example-two
```

### Step Four: Rebase your two branches. 
Since it will be common that other developers on your team will be working on the same code we always want to rebase from the latest. 
In this case we will use the two branches provided in this repo. `JIRA-005-merge-conflict-example` and `JIRA-005-merge-conflict-example-two`. 
```
$ git rebase JIRA-005-merge-conflict-example
```

You should see something along the lines
 
 ```
 [allierays/what-is-git-demo (JIRA-005-merge-conflict|REBASE 1/1)]$ git status
 rebase in progress; onto cc06a94
 You are currently rebasing branch 'JIRA-005-merge-conflict' on 'cc06a94'.
   (fix conflicts and then run "git rebase --continue")
   (use "git rebase --skip" to skip this patch)
   (use "git rebase --abort" to check out the original branch)
 
 Unmerged paths:
   (use "git reset HEAD <file>..." to unstage)
   (use "git add <file>..." to mark resolution)
 
 	both modified:   005b-git-merge-conflict.md
 
 Changes not staged for commit:
   (use "git add <file>..." to update what will be committed)
   (use "git checkout -- <file>..." to discard changes in working directory)
 
 	modified:   005-git-merge-conflict.md
 
 no changes added to commit (use "git add" and/or "git commit -a")
 
 ```

### Step Five: Review your merge conflicts 
```
<<<<<<< HEAD
The purpose of this file is only to demonstrate a git merge conflict. On branch JIRA-005-merge-conflict-example this file was updated.
=======
The purpose of this file is only to demonstrate a git merge conflict. On branch JIRA-005-merge-conflict-example-two this file was also updated.
>>>>>>> JIRA-005: Merge conflict exercise part two.

```
You can think of the HEAD as the "current branch". When you switch branches with git checkout. \
The HEAD revision changes to point to the tip of the new branch.

### Step Six: Fix your conflicts
Review what changes you need to make. Git will only ever know that changes occurred. \
It is up to the developer to determine what needs to stay or be removed. \
For the purposes of this demo we are going to say the commit from ` JIRA-005: Merge conflict exercise part two.` \
Is the most current code changes that we want to keep. \ 

Therefore, remove everything between `<<<<<<< HEAD and =======`.  Also remove the git message `>>>>>>> JIRA-005: Merge conflict exercise part two.` \
Go back to your terminal and type 
```
$ git status
```
Notice there are changes to the 005b-git-merge-conflict.md file.\
Add and commit these changes. 
```
$ git add . 
$ git commit -m"JIRA-005: Resolving merge conflict for merge file."
$ git rebase --continue
```

Try to rebase again 
```
$ git rebase JIRA-005-merge-conflict-two
```

You should see a message along the lines of 
```
[allierays/what-is-git-demo (JIRA-005-merge-conflict)]$ git rebase origin/JIRA-005-merge-conflict-two
Current branch JIRA-005-merge-conflict is up to date.   
```


### Step Seven: Create a PR
Go to your github repo \
and click create a PR. \
Review your code changes \
Review the base branch is AllieRays:master \
Create a PR \
Review [github's documentation about pull requests](https://help.github.com/en/github/collaborating-with-issues-and-pull-requests/creating-a-pull-request-from-a-fork) if you need more help with creating a PR.




## Other Troubleshooting techniques.

If you are having trouble with merge conflicts you can always reset your local to your upstream. \
For example. 

```
git checkout master 
git reset --hard upstream/master

git checkout -b  JIRA-005-merge-conflict origin/JIRA-005-merge-conflict
git reset --hard upstream/JIRA-005-merge-conflict
git push origin JIRA-005-merge-conflict origin -f

git checkout -b  JIRA-005-merge-conflict-two origin/JIRA-005-merge-conflict-two
git reset --hard upstream/JIRA-005-merge-conflict-two
git push origin JIRA-005-merge-conflict-two origin -f
```
