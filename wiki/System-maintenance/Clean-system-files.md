
# System maintenance > Clean system files

## Overview

`pacman` and `yay` store different versions of packages and their dependencies in cache folders. Unused files, dependencies, and logs accumulate over time and should periodically be cleared to keep the system's disk space tidy.

- [Clear `pacman` cache](#clear-pacman-cache)
- [Clear `yay` cache](#clear-yay-cache)
- [Clear `systemd` journal](#clear-systemd-journal)
- [Remove orphan dependencies](#remove-orphan-dependencies)

---

## Clear `pacman` cache

Every 1-2 months, remove old packages from the `pacman` cache with:

```sh
 $ paccache -r
```

This command retains the 3 most recent versions while clearing the cache at `/var/cache/pacman/pkg`. This is a system-wide cache that can be accessed by helpers such as `yay`.

- `paccache -r` - Clears cache while retaining last 3 versions.

- `paccache -ru` - Clears uninstalled packages and retains the last 3 versions.

- `paccache -ruk0` - CLears all versions of uninstalled packages.

- `pacman -Sc` - Clears all uninstalled packages and unused `pacman sync` databases. Not recommended for network-shared caches.

> [!NOTE]\
> It is not recommended to delete all past versions unless disk space is really needed. Keeping previous versions prevents redundant downloads when downgrading or reinstalling packages.
>
> See: [`paccache manpage`][paccache], [Pacman wiki: Cleaning the package cache][pacman-cache]

[paccache]:https://man.archlinux.org/man/paccache.8
[pacman-cache]: https://wiki.archlinux.org/title/Pacman#Cleaning_the_package_cache

---

## Clear `yay` cache
`yay` maintains a separate user-specific cache for AUR packages and their build files. 

1. Clear all cached AUR packages, the `pacman` cache, and untracked files:

    ```sh
     $ yay -Sc
    ```

2. `yay` will confirm which files of the cache it should remove. Enter `Y` or `N` at the terminal prompts to keep or remove the packages.
    - By default (no input), it keeps all locally installed packages. 

<details open="false"> 
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
     $ journalctl --vacuum-time=4weeks
    ```

It is recommended to keep a minimum of 4 weeks of logs. By default, the journal can only contain up to 4 GB of information.

> [!NOTE]\
> See: [`systemd journal`][journal]

[journal]: https://wiki.archlinux.org/title/Systemd/Journal

<!------------------------------------------>

## Remove orphan dependencies

**Orphans** are dependencies that are no longer needed by any program. 

These accumulate when packages are only partially removed during uninstallation, or the new version no longer requires a dependency it originally used.

1. To list orphans and recursively remove them after user confirmation, enter:
    ```sh
     $ sudo pacman -Qdtq | sudo pacman -Rns -
    ```

2. The terminal will display a list of orphans (if any). Enter `Y` to confirm removal of the listed orphans.

   - If the terminal outputs `error: argument '-' specified with empty stdin`,  there are no orphans to remove.

    [remove-orphans]: ./images/remove-orphans.png
    ![Terminal output listing an orphan after running sudo pacman -Qdtq | sudo pacman -Rns -][remove-orphans]

3. To keep any orphan dependencies, specify them with this command prior to removal:

    ```sh
     $ sudo pacman -D --asexplicit <pkg>
    ```

---

Here is a breakdown of the individual commands used:
| Command      | Description         | 
| ------------ | ------------------- |
| `sudo pacman -Qdtq` | Lists all orphan dependencies. |
| `sudo pacman -Rns <pkg>` | Removes the specified orphan. |
| `sudo pacman -D --asexplicit <pkg>` | Excludes the specified orphan from removal. |

> [!NOTE]\
> See: [Pacman Tips and Tricks: Orphans][orphans]

[orphans]: https://wiki.archlinux.org/title/Pacman/Tips_and_tricks#Removing_unused_packages_\(orphans\

<!-- EOF -->