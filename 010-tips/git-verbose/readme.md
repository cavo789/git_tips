# Enable verbose mode

When running GIT commands like a `git commit`, we don't get so much output.

An example is when we're using hooks: if a `pre-commit` hooks is enabled, the hook will be fired by GIT but ... where is stored that hook? It's not really easy to know since it can be in the `.git/hooks` folder or elsewhere (depends on the core.hooksPath, local or global setting).

So, sometimes, it's useful to get more information. To do this, just create a new DOS environment variable called `GIT_TRACE` and initialize it to `1`.

The next time you'll run a GIT command, more information's will be echoed on the console.

Below, we can see it: we've a "Here I am!" when committing changes from the `git_tips` repo. Why? We can see it in the trace... There is a `hooks/pre-commit` script in the loop.

```log
C:\Christophe\Repository\git_tips>git commit -m "Add GIT_TRACE tip"
09:10:04.825250 exec-cmd.c:237          trace: resolved executable dir: C:/Program Files/Git/mingw64/bin
09:10:04.830257 git.c:439               trace: built-in: git commit -m 'Add GIT_TRACE tip'
09:10:04.859250 run-command.c:663       trace: run_command: GIT_EDITOR=: GIT_INDEX_FILE=.git/index 'c:/christophe/repository/resources/git_hooks/hooks/pre-commit'
Here I am!
```
