![Banner](./images/banner.png)

# Git tips and snippets

> A few git tips and functions snippets

<!-- table-of-contents - start -->
* [Tips](#tips)
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
* [License](#license)
<!-- table-of-contents - end -->

## Tips

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

`/C:` is for search for a litteral value (not a regex but well a string) so `/C:" D "` will target all lines having, exactly, ` D ` (space D space) in his content
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

### Retrieve the email of a Github user

Let's say you want to retrieve the email of the `Nestor789` email.

Just go to the following URL `https://api.github.com/users/Nestor789/events/public` and search for the `email` keyword.

So, simply replace `Nestor789` in the URL above by the name of the user for whom you wish to retrieve the information.

### Search users on github based on location

The URL `https://github.com/search?q=+location:Racour&type=Users` will display the list of users for the city of `Racour` so just replace the city name to the one of your choice.

## Tools

### Check status

> Check if repositories have been changed

Scan all repositories on your hard disk under a root folder like `C:\Christophe\Repositories` and displays those that have been modified locally.

[https://github.com/cavo789/tools_git_scripts/blob/master/update_repos/git_check_status.bat](https://github.com/cavo789/tools_git_scripts/blob/master/update_repos/git_check_status.bat)

### Deploy online

Get the newer version of a repository and update a website by just running /deploy.php?sat=MyVeryLongKey from an URL.

[https://github.com/cavo789/tools_git_scripts/tree/master/deploy](https://github.com/cavo789/tools_git_scripts/tree/master/deploy)

### Easy access to your stars

[Astral](https://astralapp.com/) is a free interface that displays the list of repositories you've starred.

The interface is easy to use and has a nice search tool so it becomes really simple to retrieve a liked repo.

### Display the origin of repos

> Display the origin of repositories

Scan all repositories on your hard disk under a root folder like `C:\Christophe\Repositories` and display the origin of each repos so you can easily see which are stored on github or elsewhere like gitlab or bitbucket.

[https://github.com/cavo789/tools_git_scripts/blob/master/update_repos/git_get_origin.bat](https://github.com/cavo789/tools_git_scripts/blob/master/update_repos/git_get_origin.bat)

### Git pull

> Check if local copy of repositories needs to be refreshed. This can be done only when no local changes have been made.

Scan all repositories on your hard disk under a root folder like `C:\Christophe\Repositories` and check the status of each repository. If a newer version is available online and if your local copy is unchanged, the repo will be updated automatically (a `git pull` will be made on the repo).

[https://github.com/cavo789/tools_git_scripts/blob/master/update_repos/git_pull.bat](https://github.com/cavo789/tools_git_scripts/blob/master/update_repos/git_pull.bat)

## License

[MIT](LICENSE)
