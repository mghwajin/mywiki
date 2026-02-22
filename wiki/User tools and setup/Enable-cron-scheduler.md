
# User tools & setup > Enable `cron` scheduler

## `cron`/`cronie` overview

`cron` is a scheduling `daemon` that allows the system to automatically run programs and other jobs on a set schedule. In Arch systems, `cronie`, an implementation of `cron`, is used.

Notably, `cronie` is essential for setting up automatic system backups through `timeshift`. This ensures the system automatically creates snapshots on system boot, every hour, etc. at user-defined frequencies.

> [!NOTE]\
> See: [`cron manpage`][cron-manpage], [`cron` wiki guide][cron-wiki], [`cronie` timed tasks guide][cronie]

[cron-manpage]: https://www.man7.org/linux/man-pages/man8/cron.8.html
[cron-wiki]: https://wiki.gentoo.org/wiki/Cron
[cronie]: https://docs.rockylinux.org/10/guides/automation/cronie/

<!------------------------------------------->

## How to install `cronie`

To install `cronie`, enter:

```sh
sudo pacman -S cronie
```

`cronie` is disabled by default and must be manually enabled with:

```sh
sudo systemctl enable cronie.service
```

Once scheduled snapshots are configured in `timeshift`, the `cronie` scheduler will run regular jobs to automatically create snapshots.

<!------------------------------------------->

## Disable `cronie`

> [!WARNING]\
> Make sure that system daemons are **inactive** before disabling them.
>
> `daemons` such as `cronie` are needed for essential services. Forcibly disabling them while they are still active (and possibly running jobs) may cause the system to become unstable.

1. First, stop the `cronie` process with:
    ```sh
    systemctl stop cronie.service
    ```

2. Check that the process is inactive by running:
   ```sh
   systemctl status cronie.service
   ```
 <details>
  <summary>Terminal output with active process: </summary>

  ```sh
  cronie.service - Command Scheduler
  Loaded: loaded (/usr/lib/systemd/system/cronie.service; enabled; preset: disabled)
  Active: active (running) since Day YYYY-MM-DD HH:MM:SS -timezone; 00h 00min ago
  ...
  ```
 </details>
 <br/>

3. After verifying that `cronie` is **inactive**, enter:
   ```sh
   systemctl disable cronie.service
   ```

<!------------------------------------------->

## `cron` versus `cronie`

`cron` has several implementations with variations in scheduling and job management.

`cronie` comes with the `anacron` utility enabled by default, which will run backlogged jobs for systems not continuously running (ex. personal computers).

> [!NOTE]\
> See: [`anacron manpage`][anacron]

[anacron]: https://man.archlinux.org/man/anacron.8.en

<!-- EOF -->