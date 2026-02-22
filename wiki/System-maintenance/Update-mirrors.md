
# System maintenance > Update mirrors

This guide overviews the definitions of mirrors, mirrorlists, possible errors, and how to maintain up-to-date mirrors.

- [Overview](#overview)
- [Re-rank mirrors](#re-rank-mirrors)
- [Common issues: outdated mirrors](#common-issues-outdated-mirrors)
- [FAQs](#faqs)
  
<!---------------------------------------------------------->

## Overview

**Mirrors** are servers located around the world that store copies of software packages. When upgrading packages, your EndeavourOS system utilizes multiple mirrors, which are noted in a `mirrorlist`. 

A well-maintained `mirrorlist` ensures that the `pacman` package manager can access the most up-to-date package files when performing system updates. Outdated mirrors can prevent `pacman` from updating applications, including the system's **core packages**.

To update a `mirrorlist` configuration, users should run commands to **re-rank mirrors**.

> [!IMPORTANT]\
> It is highly recommended to re-rank mirrors at least every 1-2 months.

<!---------------------------------------------------------->

## Re-rank mirrors

Arch packages are updated on a frequent and unscheduled rolling-release basis. Your Arch `mirrorlist` configuration should be updated regularly so your system can access up-to-date package databases.

`mirrorlists` are configured separately for **Arch** mirrors and **Endeavour OS** mirrors. The process is the same, but different commands are used.

### Re-rank Arch mirrors

1. Update the Arch `mirrorlist` by running the command:
   
    ```sh
    reflector-simple
    ```

2. By default, `reflector-simple` selects the **20 fastest** mirrors based on your set location. You can adjust these preferences in the GUI tool.
 
    [reflector-simple-1]: ./images/reflector-simple-1.png
    ![A GUI Preference menu that displays after running `reflector-simple`, displaying settings such as region, filter by options, and amount.][reflector-simple-1]

   - The `reflector-simple` GUI tool allows easy customization of mirror locations, the number of mirrors stored, and ranking priority (latest, fastest, etc.)

3. Hit **OK** to confirm the selection and run the process. It is normal to see warnings as `reflector` tests various mirrors for connectivity speed and age.

4. The system will notify you once the new Arch `mirrorlist` has been generated. **Save** to apply the configuration changes.
   
   [reflector-simple-2]: ./images/reflector-simple-2.png
   ![New mirrorlist output from `reflector-simple` listing 20 U.S. mirrors ranked by speed.][reflector-simple-2]

5. **Refresh the system** to sync the newly obtained mirrors with the Arch package databases:
   
    ```sh
    yay -Syyu
    ```

> [!CAUTION]\
>  Do not run `yay` with root permissions (`sudo`), or it may cause accidental (and potentially fatal) system changes. The AUR helper does not require root permissions to manage packages.

---

### Re-rank EndeavourOS mirrors

**Endeavour OS** has its own distro-unique packages, which are modified/additional versions distinct from Arch packages. These are stored in EOS-specific mirrors.

1. Update the Endeavour OS `mirrorlist` with:
   
    ```sh
    eos-rankmirrors
    ```

2. The `eos-rankmirrors` process only shows terminal output (no GUI tool).

3. The terminal may display errors/warnings as the system tests various mirrors for connectivity and speed. It may take a few minutes to find the requisite amount of mirrors.
   
   [rank-mirrors-1]: ../images/eos-rankmirrors-1.png
   ![`eos-rankmirrors` terminal output listing timed-out mirrors and the new mirrorlist.][rank-mirrors-1]

4. By default, the `eos-rankmirrors` script generates a new `mirrorlist` containing the 20 fastest EOS mirrors. These are listed along with the original `mirrorlist`.

5. To confirm and save the changes, enter your system's root password.
   
   [rank-mirrors-3]: ./images/eos-rankmirrors-3.png 
   ![Bottom of `eos-rankmirrors` terminal output waiting for root password confirmation to save the mirrorlist.][rank-mirrors-3]

6. If you do **NOT** wish to make the  `mirrorlist` changes, stop the terminal process. By default, this shortcut is bound to `Ctrl+C` in the terminal.

7. After confirming any mirrorlist changes, refresh the system with:
   
    ```sh
    yay -Syyu
    ```

> [!CAUTION]\
>  Do not run `yay` with root permissions (`sudo`), or it may cause accidental (and potentially fatal) system changes. The AUR helper does not require root permissions to manage packages.

---

## Common issues: outdated mirrors

When `pacman` receives a command to update packages and refresh the system, it attempts to connect to the package databases stored in mirrors. Outdated mirrors can prevent `pacman` from updating your system to the newest packages. 

Common error or warning messages include:

| Terminal message       | Issue                   |
|----------------------- | ----------------------- |
| `GPGME error: No data` | Files from the package database are outdated or corrupt | 
| `failed to synchronize all databases (invalid or corrupted database (PGP signature))` | Outdated mirrors - not in sync with package databases |
| `failed retrieving file 'package-version.pkg' from arch.mirror.mx : The requested URL returned error: 404` | Mirror cannot be reached, or package files are not available | 
| `failed to commit transaction (failed to retrieve some files)` | Mirror cannot be reached, or package files are not available |
| `warning: too many errors from arch.mirror.mx, skipping for the remainder of this transaction` | Slow/unstable mirror connection (timed out) or network issues | 

If `pacman` runs into these errors during a system update, be sure to [re-rank mirrors](#re-rank-mirrors) before another update attempt.

> [!WARNING]\
> If these errors/warnings persist despite re-reranking mirrors, this may indicate **outdated AUR packages** and require updating with `yay`.
>
> See: [System updates with `pacman` and `yay`][pacman-yay]

[pacman-yay]: ../system-maintenance/system-updates-with-pacman-and-yay.md#yay

---

## FAQs

Useful links:
- [Arch mirrors wiki][arch-mirrors]
- [Official Arch mirror status][arch-status]
- `reflector`<sup>[AUR][reflector-aur]</sup> | [`reflector` wiki][reflector-wiki]

[arch-mirrors]: https://wiki.archlinux.org/title/Mirrors
[arch-status]: https://archlinux.org/mirrors/status/
[reflector-aur]: https://archlinux.org/packages/?name=reflector
[reflector-wiki]: https://wiki.archlinux.org/title/Reflector

---

### How does running `pacman -Syu` use mirrors?

When the user enters `sudo pacman -Syu` into a terminal, the `pacman` package manager begins the process to sync (`-S`), refresh (`-y`), and update (`-u`) the system.

  1. `pacman` attempts to connect and sync to Arch and EOS package databases.
   
  2. If successful, `pacman` searches for and detects new versions of packages/dependencies that are installed on your system.
   
  3. The terminal outputs a list of the updateable packages with a comparison of the old and new versions.
   
  4. `pacman` waits for user permission to proceed with the update. If proceeding, user is required to enter the system's root password.
   
  5. After initiating the package(s) update, `pacman` retrieves new package files from the mirror.
   
  6. If `pacman` successfully retrieves package files, it installs them then deletes old versions.

---

### What is GPGME?

 **GnuPG** and **GPGME** are two tools are used to safely encrypt/decrypt the package files that `pacman` retrieves from package databases. If mirrors cannot access package databases (or are out of sync), you may see `GPGME` or `PGP` related errors.

- The [GPGME][gpgme] (or GnuPG Made Easy) library provides applications easier access to GnuPG functions.

- [GnuPG][gnupg] is a command-line interface (CLI) tool and universal crypto engine. It is often used as the **crypto backend** for applications.

[gpgme]: https://www.gnupg.org/software/gpgme/index.html
[gnupg]: https://www.gnupg.org/documentation/index.html

---

### How do I use `reflector` instead of `reflector-simple`?

Endeavour OS uses uses `reflector` as its default mirror management program. `reflector-simple` provides a GUI tool to assist the user, but it is also possible to use specific CLI commands and options for the same result.
  
To update to and save the **latest 20 mirrors** sorted by **speed**, enter:

 ```sh
 reflector --latest 20 --sort rate --save /etc/pacman.d/mirrorlist
 ```

This process will:

 1. Retrieve the latest mirrorlist from the [Arch mirror status page][arch-mirrors].

 2. Filter/rank the mirrors by speed (until it has found 20, or a user-specified amount).

 3. Saves then overwrites the current `/etc/pacman.d/mirrorlist` config file.

> [!NOTE]\
> Refer to the [`reflector manpage`][reflector-manpage] documentation for usage details. 
>
> This information can also be accessed offline by running `reflector --help` in the terminal.

[reflector-manpage]: https://man.archlinux.org/man/reflector.1

---

### Are there mirror management alternatives?

Popular alternatives to mirror management are listed on the [Arch mirrors wiki][arch-mirrors]. Some programs can automate mirror management when configured properly.

One such example is `ghostmirror`, which:

1. Checks that mirrors are **synchronized**.
   
2. Performs **download speed tests** on top of the usual ping test.
   
3. Automates the process via `systemd`.

> [!NOTE]\
> See: `ghostmirror`<sup>[AUR][ghostmirror-aur]</sup>, [`ghostmirror` wiki][ghostmirror-wiki]

[ghostmirror-aur]: https://aur.archlinux.org/packages/ghostmirror/
[ghostmirror-wiki]: https://wiki.archlinux.org/title/Ghostmirror

<!-- EOF -->
