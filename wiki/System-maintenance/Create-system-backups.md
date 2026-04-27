
# System maintenance > Create system backups

## Overview

System backups are created with `timeshift`, an important utility tool that creates "snapshots" of key system settings and files. 

These snapshots can be used to restore the system to a prior state if the current state becomes unbootable or unusable.

## How to create a snapshot

1. Create an unscheduled, on-demand snapshot:

     ```sh
      $ sudo timeshift --create
     ```

2. Check if a snapshot is due first, and create one only if needed:

     ```sh
      $ sudo timeshift --check
     ```

> [!IMPORTANT]\
> It is highly recommended to create daily backups and before making changes to important system settings (such as config files).
>
> See: [`Timeshift` wiki][timeshift], [Restore system with snapshot][restore-snapshot]

[timeshift]: https://wiki.archlinux.org/title/Timeshift
[restore-snapshot]: https://itsfoss.gitlab.io/post/how-to-use-timeshift-to-backup-and-restore-linux-system/#restoring-your-linux-system-with-timeshift


## `timeshift` options

`timeshift` options can be adjusted in the application, or through the terminal by running `timeshift` with root permissions. 

---

### Snapshot type

**RSYNC** snapshots are incremental copies of changed system files.

 -  Keeps hard-links for files unchanged from the previous snapshot.

 -  Take up more space but are much more simple to set up.

**BTRFS** snapshots are only available on systems set up with a BTRFS file system.

 - Much quicker and space-efficient.

 - Requires more technical knowledge of files systems to properly configure.

---

### Back up location

It is recommended to set snapshots to save onto an external drive, or an internal drive separate from the system's boot partition. 
 - This eases the process of recovering to a previous state if the current one becomes unbootable.

 - Note that BTRFS snapshots can only be saved onto the same device with the system's root partition.

 > [!NOTE]\
> You can select the specific drive/device to save snapshots to. However, aside from the device, the default directory path for `timeshift` **cannot be changed**.

---

### Saved data

To save disk space, `timeshift` does not save any user files by default. 

Setting `timeshift` to save **non-system files** will use a very large amount of disk space, especially with automatic snapshots enabled.

---

### Snapshot limits

Once the number of snapshots reaches the set limit, `timeshift` deletes the oldest snapshot of that category. The exact amounts vary between users. Here is an example of snapshot limits:

 - 4 monthly
 - 4 weekly
 - 7 daily
 - 5 hourly
 - 5 boot

---

### Scheduled snapshots

Users can set up `cron` to schedule time-based jobs. 

When configured, the system automatically generates scheduled snapshots up to the set limit, and deletes old snapshots when the limit is reached.

> [!TIP]\
> Automated snapshots at scheduled intervals require a scheduling daemon, which must be manually enabled. The `cron` scheduling daemon is used in Endeavour OS.
>
> See: [Enable the `cron` scheduler][cron]

[cron]: Enable-cron-scheduler

<!-- EOF -->