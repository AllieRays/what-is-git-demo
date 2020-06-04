# Git Merge Conflict

As a developer I want to manage code conflicts so that I know how to manage my code effectively.

## Exercise 

Prerequisites: Make sure you do Exercise two: https://github.com/AllieRays/what-is-git-demo/blob/master/002-fork-a-repo.md \
Check that you have both your origin and upstream remote git repositiories. \
It should look similar to:
```
[allierays/what-is-git-demo (master)]$ git remote -v
origin	git@github.com:[your-github-name]/what-is-git-demo.git (fetch)
origin	git@github.com:[your-github-name]/what-is-git-demo.git (push)
upstream	git@github.com:AllieRays/what-is-git-demo.git (fetch)
upstream	git@github.com:AllieRays/what-is-git-demo.git (push)
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
To work on our changes locally, check out the remote branch `JIRA-005-merge-conflict-example`. Then checkout the branch `JJIRA-005-merge-conflict-example-two`

```
$ git checkout -b JIRA-005-merge-conflict-example origin/JIRA-005-merge-conflict-example
$ git checkout -b JIRA-005-merge-conflict-example-two origin/JIRA-005-merge-conflict-example-two
```

### Step Four: Rebase your two branches. 
Since it will be common that other developers on your team will be working on the same code we always want to rebase from the latest. \
In this case we will use the two branches provided in this repo. `JIRA-005-merge-conflict-example` and `JIRA-005-merge-conflict-example-two`. \
Double check you are on the JIRA-005-merge-conflict-example-two branch
```
$ git branch 
```
This should return `JIRA-005-merge-conflict-example-two` \
Then rebase the first branch.

```
$ git rebase JIRA-005-merge-conflict-example
```

You should see something along the lines
 
 ```
 First, rewinding head to replay your work on top of it...
Applying: JIRA-005: Example number two of a merge conflict.

Using index info to reconstruct a base tree...
M	005b-git-merge-conflict.md
Falling back to patching base and 3-way merge...

Auto-merging 005b-git-merge-conflict.md

CONFLICT (content): Merge conflict in 005b-git-merge-conflict.md
error: Failed to merge in the changes.
Patch failed at 0001 JIRA-005: Example number two of a merge conflict.
hint: Use 'git am --show-current-patch' to see the failed patch

Resolve all conflicts manually, mark them as resolved with
"git add/rm <conflicted_files>", then run "git rebase --continue".
You can instead skip this commit: run "git rebase --skip".
To abort and get back to the state before "git rebase", run "git rebase --abort".

 ```

### Step Five: Review your merge conflicts 
```
<<<<<<< HEAD
The purpose of this file is only to demonstrate a git merge conflict. On branch JIRA-005-merge-conflict-example this file was updated.
=======
The purpose of this file is only to demonstrate a git merge conflict. On branch JIRA-005-merge-conflict-example-two this file was also updated.
>>>>>>> JIRA-005: Example number two of a merge conflict.

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
Add these changes, continue your rebase and force push to your origin.
```
$ git add . 
$ git rebase --continue
$ git push origin -f
```

Try to rebase again 
```
$ git rebase JIRA-005-merge-conflict-example-two
```

You should see a message along the lines of 
```
[allierays/what-is-git-demo (JIRA-005-merge-conflict)]$ git rebase origin/JIRA-005-merge-conflict-two
Current branch JIRA-005-merge-conflict-example-two is up to date.
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
$ git fetch --all
$ git checkout master 
$ git reset --hard upstream/master
$ git push origin 
```
