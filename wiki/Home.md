<!-- -->

![Endeavour OS logo and text for a dark background][eos-logo]

# Wiki overview

This wiki contains short guides and overviews of Linux terminal commands used for basic system maintenance. Some of the commands covered in this wiki are exclusive to Arch Linux-based systems, and may differ from those used in Ubuntu, Fedora, and other distros.

> [!NOTE]\
> **[Endeavour OS][eos]** is a resource-light and terminal-centric distro based on [Arch Linux][arch]. Along with the classic Arch installation experience for power users, it also provides an easy installation and setup process via the Calamares tool.

Linux systems are highly customizeable but require more hands-on maintenance to run smoothly. Users should regularly:

 1. **Back up** system files

 2. **Update** important programs

 3. **Clean** out old or unused files

Through various terminal commands, users can upgrade essential packages, obtain new program features, and ensure system stability and security. 

[arch]: https://archlinux.org/
[eos]: https://endeavouros.com/
[eos-logo]: wiki/images/endeavouros-logo-text-dark.svg

## Directory
- [README][readme] 
- [Wiki homepage][wiki] 

<!-- links -->
[readme]: https://github.com/mghwajin/mywiki/blob/main/README.md
[wiki]: https://github.com/mghwajin/mywiki/wiki


### System maintenance

- [Overview](System-maintenance-overview)

- [Create system backups](Create-system-backups) (`timeshift`)

- [Clean system files](Clean-system-files) (`paccache`, `journalctl`)

- [Update mirrors](Update-mirrors) (`eos-rankmirrors`, `reflector-simple`)

- [Update system packages](Update-system-packages) (`pacman`, `yay`, `eos-update`)

- [Resolve config conflicts](Resolve-config-conflicts) (`eos-pacdiff`, `pacdiff`, `meld`)

### User tools & setup

- [Change default kernel](Change-default-kernel) (`bootctl`)

- [Change login background](tools-login-bg) (`nano`, `slick-greeter`)

- [Copy cursor screen selection](Copy-cursor-screen-selection) (`xfce4-screenshooter`)

- [Enable `cron` scheduler](Enable-cron-scheduler) (`timeshift`, `cron`, `systemctl`)

- [`git clone` to a location](git-clone-to-a-location) (`git`, `git clone`, `cd`)

---

<!-- EOF -->