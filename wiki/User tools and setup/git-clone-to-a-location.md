
# User tools & setup > `git clone` to a location

## `git clone` usage

By default, `git` repositories are cloned into the current directory (usually `~/home`). You can specify the intended location for a repository using:

```shell
git clone <repository-url> <destination-folder>
```

## Considerations

- If this directory already exists, it must be **empty**, otherwise you will get an error.

- If this directory does **not** exist, creates a new directory at the specific path.

> [!TIP]\
> You can clone a repository's **contents** into the current directory by using `git clone <repo-url> .` \
> Since this clones all content into the current location, it is important to change directories (using `cd`) into the correct directory first, lest files explode everywhere.  
> 
> See: [`cd manpage`][cd], [`git`][git]

[cd]: https://man.archlinux.org/man/cd.n
[git]: https://git-scm.com/about

<!-- EOF -->
