# Git
## General info:
 - what is `master` ?
 - what is `origin` ?
 - what is `HEAD` ?
 - What is `branch` ?
 - What is `SHA` ?
 
---
# By Workflow

### Cycle 1:
- Clone
- add / modify / delete
- commit push

### Cycle 2:
- Clone
- Switch to Branch
- Create Branch
- Modify
- commit
- push

### Cycle 3:
- Pull
- Switch to Branch
- Merge branch
- Fix Merge Conflicts
- Update branch
- Do pull request

--- 
# By Topics
## Part 1: (check status with each step)
1. new repo `git init`
2. add files `git add .`
3. commit changes `git commit`
4. add remote server `git remote add origin url`
5. push to server `git push -u origin master`

## Part 2:
1. clone repo `git clone`
2. create branch `git checkout -b <branchName>`
2. change files 
3. delete files
4. commit `git commit -am"CommitMsg"`
5. modify then amend `git commit --amend`
4. push branch to server `git push -u origin <branchName>`

## Part 3:
1. pull latest changes `git pull`
2. Merge 2 branches `git merge`
3. 
---
# Additional Notes:

## Fixing Merge Conflict:
1. Edit the file which has a conflict -> `add` -> `commit`
2. `git pull -X theirs` (to auto-merge and use remote version of the file)
3. during failed merge use: `git checkout --theirs or --ours <fileName>`

---
## Available GUI Tools
1. Atlassian Sourcetree
2. VS Code
3. Git fork
4. Git Kraken
5. TortoiseGit