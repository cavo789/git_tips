# Update a branch (merge request)

You've a `dev` and a `myFeature` branches and you want to update the `myFeature` branch with the latest changes done in branch `dev`.

In a DOS Prompt Session, make sure you're in branch `myFeature` (run `git branch` or `git status` to confirm this).

Then, run these commands:

* `git pull` to make sure that your current branch is up-to-date (don't trust `git status`, it's always a good idea to run `git pull` even if `git status` has said *up-to-date*),
* `git merge origin/dev` so changes in `dev` branch are merge in the current (`myFeature`) branch,
* You'll probably have a lot of conflicts, 
   * `git status` so you can see the list of **Unmerged paths** (= conflict)
   * Now, you need to solve them; for instance,
      * Start vscode,
      * Show the `Source Control` pane (<kbd>CTRL</kbd>-<kbd>SHIFT</kbd>-<kbd>G</kbd> followed by <kbd>G</kbd> once more),
      * Select the list of files with conflicts and solve them one by one or all at once: right click on the file and accept all incoming changes.
      * This done, select the list of files once more, right click and commit changes.
