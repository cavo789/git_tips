# Git hooks folder

By default, the `hooks` folder is located in the `.git` folder but this can be changed with the [core.hooksPath](https://git-scm.com/docs/git-config#Documentation/git-config.txt-corehooksPath) setting.

The following command will set the hooks folder for ALL PROJECTS to the `c:\repos\central_hooks` folder. This way, in only one instruction, you'll use the same set of hooks for all your repositories.

```bash
git config --global core.hooksPath c:/repos/central_hooks
```

Then inside of `c:\repos\central_hooks` you'll need to add a `/hooks` sub-folder and moved all of your own hooks there.

Note: you can also change hooks repos by repos using the command below:

```bash
git config core.hooksPath c:/repos/central_hooks
```
