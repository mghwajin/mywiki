---
System maintenance > Overview
---

# Overview

Arch-based distros like Endeavour OS have rolling release updates. These frequent updates keep up with latest feature releases, but can also cause some unforeseen issues. Users should regularly run maintenance tasks to keep the system clean, up to date, and secure.

**Quick resources**
- [Key terms glossary](#key-terms-glossary)
- [Maintenance cheatsheet](#maintenance-cheatsheet)

**Guides**
- [Clean unused system files](sys-file-cleanup)
- [Create system backups with `timeshift`](sys-backup-timeshift)
- [System updates with `pacman` and `yay`](sys-update-packages)
- [Mirror maintenance guide](sys-update-mirrors)
- [Resolve conflicting config files](sys-config-conflicts)

> [!TIP]\
> Another key resource for Linux commands and other utility tools are [`manpages`][manpage], or "manual pages". These are available offline, in-terminal, and provide in-depth usage information for terminal commands and available options. It is recommended to reference a `manpage` when confused about a command or tool!

[manpage]: https://wiki.archlinux.org/title/Man_page

<!--------------------------------------------->

## Key terms glossary

| Term                | Description                  |
| ------------------- | ---------------------------- |
| Arch Linux          | Rolling-release distribution of Linux known for bleeding-edge features and highly customizeable environment. |
| Arch User Repository | Known as the [AUR][aur], a library of tools developed by the Arch user community. Popular packages are voted for and included in the official Arch extra repository. |
| Command-line interface | Also called the shell. Layer where users enter text commands for system to execute. Common Linux shells are Bash and Zsh. |
| Config files  | Configurations for system programs or apps stored in the `/etc` or `~/home` directory. |	
| Distro/distribution | Operating systems customized from a base Linux kernel with specific/unique packages, desktop environments, etc. |	
| Display manager | Manager that sets system login screen and interface, and launches the desktop session. |
| GUI wrapper   | Graphical interface used to more easily apply/execute command line options. |	
|[GnuPG][gnupg] | Command-line tool and universal crypto engine. Often used as the crypto backend for applications. |
|[GPGME][gpgme] | The GnuPG Made Easy library, used to provide applications easier access to GnuPG functions. |
| Greeter       | UI portion of display manager that accepts and verifies user credentials, and can customize the login screen. |	
| Mirror        | Servers with stored copies of software repositories. Provide user access to files without overburdening the original source. |	
| Mirrorlist    | List containing information for mirror access link, age, download speed, location, etc. |
| Orphans       | Dependencies no longer needed by any program. May accumulate due to updated versions sunsetting dependencies or incomplete uninstallations. |
| Package       | Collection of files used by package managers to un/install, upgrade, or remove programs, libraries, etc. |
| Dependency    | Additional packages or libraries required for specific software to run properly. |	
| Package manager | System tool that downloads, installs/uninstalls, upgrades, and verifies packages. Arch-based systems use `pacman`. |
| Rolling-release | Unscheduled updates that are continuously released, usually as soon as they are available. Updates are smaller and more frequent. |
| Shell      | Also called CLI. The layer where users enter text commands for the system to execute. Common Linux shells are Bash and Zsh. |
| System daemon | Background service/process that starts on system boot (or user demand) and provide functions suchs as timed scheduling and logging. |
| Terminal      | Interface that takes user commands and outputs text results. Emulates hardware terminals from old-style physical computers. |
| Terminal command | Instruction entered into the CLI, invoking the system or a program with specified options. |	
| Timeshift     | System backup utility tool used to restore system to a previous state. Createa "snapshots" of important system settings. |

[aur]: link
[gnupg]: https://www.gnupg.org/documentation/index.html
[gpgme]: https://www.gnupg.org/software/gpgme/index.html

<!--------------------------------------------->

## Maintenance cheatsheet

Below is a quick reference table of common terminal commands and the recommended frequency. 

| Frequency | Command                  | Usage                           | 
| --------- | :----------------------- | ------------------------------- | 
| Daily    | `sudo timeshift --create` | Create an unscheduled snapshot. Use before making any changes to system settings. | 
|          | `sudo timeshift --check` | Check for recent snapshot, create if needed. |
|           | `sudo pacman -Syu`       | Syncs, refreshes, and updates packages to match newest versions from mirrors. |
| As needed | `eos-pacdiff`            | Notifies user of conflicts, calls `pacdiff` and `meld` to assist with config merges. | 
|         | `DIFFPROG=meld pacdiff -s` | Use `pacdiff` tool and `meld` GUI to assist user with merging config files. |
|           | `sudo pacman -Rns <pkg>` | Uninstall and remove a package and any dependencies. | 
|            | `yay -Rns <pkg>`   | Uninstall and remove an AUR package and its dependencies. |
|            | `eos-shifttime`    | Revert to the system status on a set date, useful temporary solution if recent update causes issues. |
| Bi/weekly  | `yay`              | Updates core system packages. Same as `eos-update --aur`. | 
|            | `eos-update`       | Updates Endeavour OS-specific core packages. | 
| Bi/monthly | `yay -Sc`          | Clear the `yay` cache. |
|            | `reflector-simple` | Runs `reflector` with a GUI assistant to generate updated Arch `mirrorlist`. |
|            | `eos-rankmirrors`  | Generate new Endeavour OS-specific `mirrorlist`, ranking the latest 20 mirrors by rate. |
|            | `paccache -r`      | Clear `pacman` cache of uninstalled packages, maintain the last 3 versions. |
|            | `journalctl --vacuum-time=#weeks` | Clear `systemd` journal, retain logs for designated # of weeks. |
|       | `sudo pacman -Qdtq \| sudo pacman -Rns -` | Lists orphaned dependencies, removes with user confirmation. |

---

> [!TIP]\
> For users unfamiliar with terminal usage or needing quick system fixes, the [**Endeavour OS Welcome Assistant**][welcome-app] is a helpful alternative to manually running maintenance tasks.

Open the **Welcome App** from System Applications, or with the `eos-welcome` terminal command.

![Endeavour OS Welcome program v25.10.3-1 with a list of update scripts on the Assistant tab.][eos-welcome]

[eos-welcome]: ../../images/eos-welcome.png
[welcome-app]: https://discovery.endeavouros.com/endeavouros-tools/welcome/2021/03/

---

<!-- EOF -->
