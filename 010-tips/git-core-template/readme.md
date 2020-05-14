# Git init

When creating a new repo with `git init`, a template is used. The current version is located on `C:\Program Files\Git\mingw64\share\git-core\templates`.

By updating there f.i. the `pre-commit` script, you'll thus automatically get your customized version each time you create a new repo on your disk.

On Linux, the path is `/usr/share/git-core/templates`.

Note: you can change this settings by setting [`init.templateDir`](https://git-scm.com/docs/git-config#Documentation/git-config.txt-inittemplateDir) to your own template folder.
