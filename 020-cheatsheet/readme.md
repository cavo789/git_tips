# Git cheatsheet

## Clone a specific branch files: 

`git clone --branch <branch-name> <url-repo>`

## Rename a local branch and push then

* `<oldname>` is the current name of the branch, the one you wish rename and
* `<newname>` the new name to give

1. `git branch <oldname>`
2. `git branch -m <newname>`
3. `git branch` <-- you should see the new name
4. `git push origin :<oldname>`
5. `git push origin <newname>:refs/heads/<oldname>`
6. `git push origin HEAD:<newname>` <-- now the branch is also online
