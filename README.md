# Understanding GIT 
The purpose of these exercises is to get hands on experience for common git commands and methodology.   

### Commit Messages Guidelines
Always include the issue number in your commit message. Ex: "JIRA-104: Moved install profile to be under /profiles rather than /profiles/custom." \
Optionally include additional information in your commit message if your commit makes multiple changes to the codebase.
Example: JIRA-104: Moved install profile to be under /profiles rather than /profiles/custom. \
Added the module security_review Added new install profile configuration option "feature-set"

#### Pull Request Guidelines
Always include a link to the issue  in the PR comments Always review your PR for merge conflicts and fix those. \
Cleaning up your Git repo
```
$ git fetch -p origin     prune your local "cache" of remote branches firs
$ git branch -D <branch name>    Deleting a local branch - optional
$ git push origin --delete <branch name>    push delete changes back up remote  - optional
```

#### Common git commands
```
git command    definition
git remote show origin     shows the origin of the git repo. 
git fetch     updates your remote-tracking branches
git pull    pulls remote changes
git add -p    add each change individually to a single commit
git rebase --interactive HEAD~2    merge your commits together
git clean -fd    remove untracked files and directories
git stash    save and remove local changes but do not commit them
git stash pop    return saved change
sgit fetch
Git add -p lets you add your commits in small batches. By committing one change at a time, you can exclude changes that do not pertain to your commit message. This is helpful when other developers are reviewing your commit messages. Important to note that git add -p will only add changes to files, not add new files. You will still have to use git add for new files. git add -p.
 When you use git add -p you will see the options
 Stage this hunk [y,n,q,a,d,/,e,?]?
 These options in more detail.
y -    stage this hunk
n -    do not stage this hunk
q -    quit; do not stage this hunk or any of the remaining ones
a -    stage this hunk and all later hunks in the file
d -    do not stage this hunk or any of the later hunks in the file
/ -    search for a hunk matching the given regex
j -    leave this hunk undecided, see next undecided hunk
J -    do not stage this hunk or any of the later hunks in the file
k -    leave this hunk undecided, see next undecided hunk
s -    leave this hunk undecided, see next hunk
e -    manually edit the current hunk
? -    print help
```



## More Documentation 
https://www.atlassian.com/git/tutorials/making-a-pull-request
https://www.atlassian.com/git/tutorials/comparing-workflows/forking-workflow
https://www.atlassian.com/git/tutorials/using-branches
https://backlog.com/git-tutorial/
