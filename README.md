README.md

# Endeavour OS Basics

This user guide overviews maintenance tasks for systems running **Endeavour OS**, relevant terminal commands, general user tools, and links to additional resources.

## Overview 

[eos-logo]: wiki/images/endeavouros-logo-text-dark.svg
![Endeavour OS logo and text for a dark background][eos-logo]

**[Endeavour OS][eos]** is a resource-light and terminal-centric distro based on [Arch Linux][arch]. Along with the classic Arch installation experience for power users, it also provides an easy installation and setup process via the Calamares tool.

Linux systems are highly customizeable but require more hands-on maintenance to run smoothly. Users should regularly:

 1. **Back up** system files

 2. **Update** important programs

 3. **Clean** out unused files

Through terminal commands, users can upgrade essential packages, obtain new program features, and ensure system stability and security.

> [!NOTE]\
> This repository is a reference for my personal setup and experience with Endeavour OS. In addition to basic wiki guides and a maintenance cheatsheet, this repo includes custom scripts that can be used as general tools and program shortcuts.

<!-- links -->
[arch]: https://archlinux.org/
[eos]: https://endeavouros.com/

## Quicklinks

- [README][readme]
- [Wiki homepage][wiki]
- [Custom scripts overview][shell-scripts]

<!-- quicklinks -->
[readme]: https://github.com/mghwajin/mywiki/blob/main/README.md
[wiki]: https://github.com/mghwajin/mywiki/wiki
[shell-scripts]: scripts/Shell-scripts-overview.md

| System Maintenance Guides   | User Tools & Setup Guides    |
| --------------------------- | ---------------------------- |
| [Overview][1]               | [Change login background][7] |
| [Create system backups][2]  | [Copy cursor selection][8]   |
| [Clean system files][3]     | [Enable `cron` scheduler][9] |
| [Update system packages][4] | [`git clone` to a location][10] |
| [Update mirrors][5]         | [Change default kernel][11]  |
| [Resolve config conflicts][6] | ---   |

<!-- wiki links -->
[1]: https://github.com/mghwajin/mywiki/wiki/System-maintenance-overview
[2]: https://github.com/mghwajin/mywiki/wiki/Create-system-backups
[3]: https://github.com/mghwajin/mywiki/wiki/Clean-system-files
[4]: https://github.com/mghwajin/mywiki/wiki/Update-system-packages
[5]: https://github.com/mghwajin/mywiki/wiki/Update-mirrors
[6]: https://github.com/mghwajin/mywiki/wiki/Resolve-config-conflicts
[7]: https://github.com/mghwajin/mywiki/wiki/Change-login-background
[8]: https://github.com/mghwajin/mywiki/wiki/Copy-cursor-screen-selection
[9]: https://github.com/mghwajin/mywiki/wiki/Enable-cron-scheduler
[10]: https://github.com/mghwajin/mywiki/wiki/git-clone-to-a-location
[11]: https://github.com/mghwajin/mywiki/wiki/Change-default-kernel

## Official resources
Official **Endeavour OS** resources and links to additional useful information:

| Link            | Description            | 
| --------------- | ---------------------- | 
| [Official site][eos] | The official Endeavour OS site where you can download and verify ISO images for installation. |
| [Titan ISO][titan]   | The Titan ISO was released on March 12, 2026. | 
| [Ganymede ISO][ganymede] | The Ganymede ISO was released on November 29, 2025. |
| [EOS README][eos-rm] | Where you can find important news and EOS updates.      |
| [EOS forums][forums] | A place to read up on EOS system updates, ask for troubleshooting help, and connect with the user community. |
| [Knowledge base][kb] | Library of various tutorials, troubleshooting guides, and intros to Linux tools. |
| [Arch wiki][arch-wiki] | Wiki with detailed articles and common troubleshooting cases for Arch-related programs and processes. |
| [Distrowatch][distro]  | Comprehensive Linux resource center that includes a weekly newsletter and Linux terms glossary. |

Credits
- [Endeavour OS Branding][brand]
- [Endeavour OS Development][dev]

<!-- official links -->
[arch-wiki]: https://wiki.archlinux.org/title/Main_page
[distro]: https://distrowatch.com
[brand]: https://github.com/endeavouros-team/Branding
[dev]: https://github.com/endeavouros-team
[forums]: https://forum.endeavouros.com/
[kb]: https://discovery.endeavouros.com/
[eos-rm]: https://gitlab.com/endeavouros-filemirror/Important-news/blob/main/README.md
[ganymede]: https://endeavouros.com/news/the-long-wait-is-over-ganymede-has-arrived/
[titan]: https://endeavouros.com/news/whats-new-in-endeavouros-titan-release/

---

```
Revision history
    2026/04 - Add Titan ISO release, edit wiki, separate shell scripts 
    2026/03 - Update system maintenance wiki pages
    2026/02 - Major wiki restructuring, add shell scripts, archive old repo
    2026/01 - Typo and formatting fixes
    2025/12 - Added glossary, command cheatsheet, and Ganymede ISO info
    2025/11 - Rework of docs content and structure
```

<!-- EOF -->
