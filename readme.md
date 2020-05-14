﻿<!--
  This file has been generated by the concat-md.ps1 script.
  Don't modify this file manually (you'll loose your changes)
  but run the tool once more
-->

<!-- Last refresh date: 2020-05-14 09:32:23 -->

<!-- below, content of ./index.md -->

# Git tips and snippets

![Banner](./images/banner.jpg)

> A few git tips and functions snippets

<!-- table-of-contents - start -->
* [Tips](#tips)
  * [Git config](#git-config)
  * [Git init](#git-init)
  * [Git hooks folder](#git-hooks-folder)
  * [Enable verbose mode](#enable-verbose-mode)
  * [Get the list of modified files](#get-the-list-of-modified-files)
    * [Don't show deleted files](#dont-show-deleted-files)
    * [Restrict based on the extension](#restrict-based-on-the-extension)
    * [Skip a folder](#skip-a-folder)
  * [Retrieve the email of a Github user](#retrieve-the-email-of-a-github-user)
  * [Search users on github based on location](#search-users-on-github-based-on-location)
* [Tools](#tools)
  * [Check status](#check-status)
  * [Deploy online](#deploy-online)
  * [Easy access to your stars](#easy-access-to-your-stars)
  * [Display the origin of repos](#display-the-origin-of-repos)
  * [Git pull](#git-pull)
  * [Get history of changes, cross repos](#get-history-of-changes-cross-repos)
* [License](#license)
<!-- table-of-contents - end -->

<!-- below, content of ./010-tips/readme.md -->

## Tips

<!-- below, content of ./010-tips/git-config/readme.md -->

### Git config

To view all your global parameters, the command below allows you to display them in the editor of your choice:

```bash
git config --global --edit
```

<!-- below, content of ./010-tips/git-core-template/readme.md -->

### Git init

When creating a new repo with `git init`, a template is used. The current version is located on `C:\Program Files\Git\mingw64\share\git-core\templates`.

By updating there f.i. the `pre-commit` script, you'll thus automatically get your customized version each time you create a new repo on your disk.

On Linux, the path is `/usr/share/git-core/templates`.

Note: you can change this settings by setting [`init.templateDir`](https://git-scm.com/docs/git-config#Documentation/git-config.txt-inittemplateDir) to your own template folder.

<!-- below, content of ./010-tips/git-hooksPath/readme.md -->

### Git hooks folder

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

<!-- below, content of ./010-tips/git-verbose/readme.md -->

### Enable verbose mode

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

<!-- below, content of ./010-tips/list-modified-files/readme.md -->

### Get the list of modified files

Get a list of modified files not yet staged:

```bash
git status -s -uall
```

By using `-uall` we ask to list of files and not f.i. just a folder name when you've created a new one and put files in it. We wish all filenames so `-uall` will display it.

The result will be something like this:

```bash
 M composer.json
 M composer.lock
 M resources/template.html
 D src/Classes/Bulma.php
 D src/Classes/Datatables.php
 M src/Classes/MonologParser.php
 M src/Classes/ViewLogs.php
?? src/Helpers/Bulma.php
?? src/Helpers/Datatables.php
?? src/Helpers/Download.php
?? src/Helpers/Strings.php
?? src/Helpers/Xml.php
```

#### Don't show deleted files

If you don't want deleted files to be mentioned, under DOS, you can use the `findstr` pipe like this:

```bash
git status -s -uall| findstr /C:" D " /B /v
```

`/C:` is for search for a litteral value (not a regex but well a string) so `/C:" D "` will target all lines having, exactly, `D` (space D space) in his content
`/B` is for restricting the search to the start of the string (like  `^` in a regex expression)
`/v` is for excluding that selection.

So `/C:" D " /B` will match these lines from the above example:

```bash
 D src/Classes/Bulma.php
 D src/Classes/Datatables.php
```

And because we've used the `/v` parameter, we will exclude the selection so `git status -s -uall| findstr /C:" D " /B /v` will return this:

```bash
 M composer.json
 M composer.lock
 M resources/template.html
 D src/Classes/Bulma.php
 D src/Classes/Datatables.php
 M src/Classes/MonologParser.php
 M src/Classes/ViewLogs.php
?? src/Helpers/Bulma.php
?? src/Helpers/Datatables.php
?? src/Helpers/Download.php
?? src/Helpers/Strings.php
?? src/Helpers/Xml.php
```

#### Restrict based on the extension

Based on the example here above, `git status -s -uall| findstr /C:"html"` will match any files having the `.html` extension.

```bash
 M resources/template.html
```

#### Skip a folder

Still based on the example here above, `git status -s -uall| findstr /C:"/Helpers/" /v` will thus match any files in the `/Helpers/` folder (and subfolder) and invert the selection so, we'll skip any files in that folder.

```bash
 M composer.lock
 M resources/template.html
 D src/Classes/Bulma.php
 D src/Classes/Datatables.php
 M src/Classes/MonologParser.php
 M src/Classes/ViewLogs.php
```

<!-- below, content of ./010-tips/retrieve-users-email/readme.md -->

### Retrieve the email of a Github user

Let's say you want to retrieve the email of the `Nestor789` email.

Just go to the following URL `https://api.github.com/users/Nestor789/events/public` and search for the `email` keyword.

So, simply replace `Nestor789` in the URL above by the name of the user for whom you wish to retrieve the information.

<!-- below, content of ./010-tips/search-users-based-on-location/readme.md -->

### Search users on github based on location

The URL `https://github.com/search?q=+location:Racour&type=Users` will display the list of users for the city of `Racour` so just replace the city name to the one of your choice.

<!-- below, content of ./020-tools/readme.md -->

## Tools

<!-- below, content of ./020-tools/check-repos-status/readme.md -->

### Check status

> Check if repositories have been changed

Scan all repositories on your hard disk under a root folder like `C:\Christophe\Repositories` and displays those that have been modified locally.

[https://github.com/cavo789/tools_git_scripts/blob/master/update_repos/git_check_status.bat](https://github.com/cavo789/tools_git_scripts/blob/master/update_repos/git_check_status.bat)

<!-- below, content of ./020-tools/deploy-online/readme.md -->

### Deploy online

Get the newer version of a repository and update a website by just running /deploy.php?sat=MyVeryLongKey from an URL.

[https://github.com/cavo789/tools_git_scripts/tree/master/deploy](https://github.com/cavo789/tools_git_scripts/tree/master/deploy)

<!-- below, content of ./020-tools/favorites/readme.md -->

### Easy access to your stars

[Astral](https://astralapp.com/) is a free interface that displays the list of repositories you've starred.

The interface is easy to use and has a nice search tool so it becomes really simple to retrieve a liked repo.

<!-- below, content of ./020-tools/get-origin/readme.md -->

### Display the origin of repos

> Display the origin of repositories

Scan all repositories on your hard disk under a root folder like `C:\Christophe\Repositories` and display the origin of each repos so you can easily see which are stored on github or elsewhere like gitlab or bitbucket.

[https://github.com/cavo789/tools_git_scripts/blob/master/update_repos/git_get_origin.bat](https://github.com/cavo789/tools_git_scripts/blob/master/update_repos/git_get_origin.bat)

<!-- below, content of ./020-tools/git-pull/readme.md -->

### Git pull

> Check if local copy of repositories needs to be refreshed. This can be done only when no local changes have been made.

Scan all repositories on your hard disk under a root folder like `C:\Christophe\Repositories` and check the status of each repository. If a newer version is available online and if your local copy is unchanged, the repo will be updated automatically (a `git pull` will be made on the repo).

[https://github.com/cavo789/tools_git_scripts/blob/master/update_repos/git_pull.bat](https://github.com/cavo789/tools_git_scripts/blob/master/update_repos/git_pull.bat)

<!-- below, content of ./020-tools/git-standup/readme.md -->

### Get history of changes, cross repos

> [https://github.com/kamranahmedse/git-standup](https://github.com/kamranahmedse/git-standup)

This tool allow to retrieve the list of commits made the last days (there are a big number of parameters like the xxx last days, since or before a given date, ...) and generate a nice output where we can see changes done by someone.

Easy to copy/paste f.i. for a Standup meeting.

![Git Standup](./020-tools/git-standup/images/git_standup.gif)

<!-- below, content of ./999-license/readme.md -->

## License

[MIT](./../LICENSE)
