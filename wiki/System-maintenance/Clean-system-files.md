
# System maintenance > Clean system files

## Overview

`pacman` and `yay` store different versions of packages and their dependencies in cache folders. Unused files, dependencies, and logs accumulate over time and should periodically be cleared to keep the system's disk space tidy.

- [Clear `pacman` cache](#clear-pacman-cache)
- [Clear `yay` cache](#clear-yay-cache)
- [Clear `systemd` journal](#clear-systemd-journal)
- [Remove orphan dependencies](#remove-orphan-dependencies)

---

## Clear `pacman` cache

1. Remove old packages from the `pacman` cache while retaining the 3 most recent versions: 
    ```sh
    paccache -r
    ```

By default, `pacman` stores package files in the `/var/cache/pacman/pkg` cache. This is a system-wide cache that can be accessed by helpers such as `yay`.

> [!NOTE]\
> It is not recommended to delete all past versions unless disk space is really needed. Keeping previous versions prevents redundant downloads when downgrading or reinstalling packages.

| Terminal command  | Description             | 
| ----------------- | ----------------------- |
| `paccache -r` | Clears the `/var/cache/pacman/pkg` cache of all packages while retaining the last 3 versions. |
| `paccache -ru` | Clears the `pacman` cache of **uninstalled** packages while retaining the last 3 versions. | 
| `paccache -ruk0` | Clears the `pacman` cache of all versions of **uninstalled** packages.
| `pacman -Sc` | Clears the `pacman` cache of all uninstalled packages and unused `pacman sync` databases. This isn't recommended for network-shared caches. |

> [!IMPORTANT]
> It is recommended to clear the `pacman` and `yay` caches every 1-2 months. \
> See: [`paccache manpage`][paccache], [Pacman wiki: Cleaning the package cache][pacman-cache]

[paccache]:https://man.archlinux.org/man/paccache.8
[pacman-cache]: https://wiki.archlinux.org/title/Pacman#Cleaning_the_package_cache


## Clear `yay` cache
`yay` maintains a separate user-specific cache for AUR packages and their build files. 

1. Clear all cached AUR packages, the `pacman` cache, and untracked files by entering:

    ```sh
    yay -Sc
    ```

2. `yay` will confirm which files of the cache it should remove. Enter `Y` or `N` at the terminal prompts to keep or remove the packages.
    - By default (no input), it keeps all locally installed packages. 

<details open>
 <summary>Example <code>yay -Sc</code> output below:
 </summary>
 
 ```sh
 Packages to keep:
  All locally installed packages

 Cache directory: /var/cache/pacman/pkg/
 :: Do you want to remove all other packages from cache? [Y/n] y
 removing old packages from cache...

 Database directory: /var/lib/pacman/
 :: Do you want to remove unused repositories? [Y/n] y
 removing unused sync repositories...
 
 Build directory: /home/kain/.cache/yay
 :: Do you want to remove all other AUR packages from cache? [Y/n] y
 removing AUR packages from cache...
 :: Do you want to remove ALL untracked AUR files? [Y/n] y
 removing untracked AUR files from cache...
 ```
</details>

> [!NOTE]\
> See: [`yay` command library][yay]

[yay]: https://linuxcommandlibrary.com/man/yay

<!------------------------------------------>

## Clear `systemd` journal

`systemd` logs system activity in the journal and is used to troubleshoot issues. Open the journal by entering `journalctl` in a terminal.

1. Clear excess journal logs while retaining the past 6 weeks' logs:

    ```sh
    journalctl --vacuum-time=6weeks
    ```

It is recommended to keep a minimum of **4 weeks** of logs, but the amount can be adjusted to personal preference. By default, the journal can only contain up to 4 GB of information.

> [!NOTE]\
> See: [`systemd journal`][journal]

[journal]: https://wiki.archlinux.org/title/Systemd/Journal

<!------------------------------------------>

## Remove orphan dependencies

**Orphans** are dependencies that are **no longer needed** by any program. These accumulate on the system when packages are uninstalled and only partially removed with `pacman -R <package-name>` (instead of the `-Rs` option) removed, or the new version no longer requires a dependency it originally used.


1. To list orphans and recursively remove them after user confirmation, use this command:
    ```sh
    sudo pacman -Qdtq | sudo pacman -Rns -
    ```

2. After running `sudo pacman -Qdtq | sudo pacman -Rns -`, enter `Y` to confirm removal of the listed orphans.
   - If the terminal outputs `error: argument '-' specified with empty stdin`, this means there are no orphans to remove.

  [remove-orphans]: ./images/remove-orphans.png
  ![Terminal output listing an orphan after running `sudo pacman -Qdtq | sudo pacman -Rns -`][remove-orphans]

3. If there are orphan dependencies that you wish to **keep**, specify beforehand which ones should be excluded from removal with this command:

    ```sh
    sudo pacman -D --asexplicit <pkg>
    ```

Here is a brief breakdown of the individual commands used:
| Command      | Description         | 
| ------------ | ------------------- |
| `sudo pacman -Qdtq` | Lists all orphan dependencies. This is useful for checking if there  are orphans that should be kept. |
| `sudo pacman -Rns <pkg>` | Removes a specified orphan. |
| `sudo pacman -D --asexplicit <pkg>` | Excludes the specified orphan from removal. |

> [!NOTE]\
> See: [Pacman Tips and Tricks: Orphans][orphans]

[orphans]: https://wiki.archlinux.org/title/Pacman/Tips_and_tricks#Removing_unused_packages_\(orphans\

<!-- EOF -->