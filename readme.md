![Banner](images/banner.png)

# Git tips and snippets

> A few git tips and functions snippets

* [Get the list of modified files](#get-the-list-of-modified-files)
  * [Don't show deleted files](#dont-show-deleted-files)
  * [Restrict based on the extension](#restrict-based-on-the-extension)
  * [Skip a folder](#skip-a-folder)
* [Enable verbose mode](#enable-verbose-mode)
* [License](#license)

## Get the list of modified files

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

### Don't show deleted files

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

### Restrict based on the extension

Based on the example here above, `git status -s -uall| findstr /C:"html"` will match any files having the `.html` extension.

```bash
 M resources/template.html
```

### Skip a folder

Still based on the example here above, `git status -s -uall| findstr /C:"/Helpers/" /v` will thus match any files in the `/Helpers/` folder (and subfolder) and invert the selection so, we'll skip any files in that folder.

```bash
 M composer.lock
 M resources/template.html
 D src/Classes/Bulma.php
 D src/Classes/Datatables.php
 M src/Classes/MonologParser.php
 M src/Classes/ViewLogs.php
```

## Enable verbose mode

When running GIT commands like a `git commit`, we don't get so much output.

An example is when we're using hooks: if a `pre-commit` hooks is enabled, the hook will be fired by GIT but ... where is stored that hook? It's not really easy to know since it can be in the `.git/hooks` folder or elsewhere (depends on the core.hooksPath, local or global setting).

So, sometimes, it's useful to get more information. To do this, just create a new DOS environment variable called `GIT_TRACE` and initialize it to `1`.

The next time you'll run a GIT command, more information's will be echoed on the console.

## License

[MIT](LICENSE)
