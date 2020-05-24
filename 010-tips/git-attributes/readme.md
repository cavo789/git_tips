# .gitattributes

> [https://git-scm.com/docs/gitattributes](https://git-scm.com/docs/gitattributes)

The `.gitattributes` file will help to keep the same rules for your repository like making sure that all `.js` file are saved with `LF` and not `CRLF`.

It's like the `.editorconfig` file but for your repo: make sure everyone who'll push files to your repository (even you) will respect the rules specified in the `.gitattributes` file.

```sql
<!-- concat-md::include "./files/gitattributes.txt" -->
```

If you're creating a fresh repository, create your `.gitattributes.txt` file and add your rules; it'll be enough.

When the file is added on an existing repository, you'll need to refresh the cache; see [Be a Git ninja: the .gitattributes file]([🙏 Please Add .gitattributes To Your Git Repository](https://dev.to/deadlybyte/please-add-gitattributes-to-your-git-repository-1jld) for more.
