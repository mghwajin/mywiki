
# User tools & setup > Change default kernel

## Contents

1. [Find kernel id with `bootctl`](#1-find-kernel-id-with-bootctl)
2. [Edit boot loader config](#2-edit-boot-loader-config)
3. [Verify and reboot](#3-verify-and-reboot)
4. [Additional information](#additional-information)

## Overview

It is possible to have multiple kernels (or "versions") of the same Linux distro installed on a computer. The newest kernel is usually booted by default, but this can be adjusted to user preference.

To change the default kernel at system boot, you need to identify and adjust the kernel `ids` used in the `boot loader config` file.

> [!NOTE]\
> This guide assumes your system uses the default `systemd-boot` UEFI boot manager in Endeavour OS.

---

## 1. Find kernel id with `bootctl`

1. Change to the root user with `sudo -s` and enter your password.

2. Check which kernel is currently set as default with:

      ```sh
      $ bootctl list
      ```

3. The terminal will display various details for installed kernels, indicating the kernel `(selected)` at boot and set as `(default)`.

      ```sh
      # kernel currently booted and set as default 
         type: Boot Loader Specification Type 1 (.conf)      
        title: EndeavourOS (6.19.11-arch1-1)  (default) (selected) # current
           id: 1fcde8d015be4360aa122975ea19eca2-6.19.11-arch1-1.conf
       source: ...
     sort-key: endeavouros-6.19.11-arch1-1
      version: 6.19.11-arch1-1
   machine-id: 1fcde8d015be4360aa122975ea19eca2 # current default id
        linux: ...
       initrd: ...
      options: ...
      ```

      ```sh
      # kernel to set as default at boot
         type: Boot Loader Specification Type 1 (.conf) 
        title: EndeavourOS (6.19.12-arch1-1)
           id: af2ba735c1714a3ebdd24c10355d5b20-6.19.12-arch1-1.conf
       source: ...
     sort-key: endeavouros-6.19.12-arch1-1
      version: 6.19.12-arch1-1
   machine-id: af2ba735c1714a3ebdd24c10355d5b20 # id to set as default
      ```

4. Copy the `machine-id` of the kernel you want to set as the default. In this example:
   - **Current id**: `1fcde8d015be4360aa122975ea19eca2`
   - **New id**: `af2ba735c1714a3ebdd24c10355d5b20`

---

## 2. Edit boot loader config

1. Enter `nano /efi/loader/loader.conf` to edit the boot loader config in the terminal.

    [nano-efi-loader]: ./images/efi-nano-loader-conf.png
    ![Terminal window showing the loader.conf file being edited with GNU nano editor][nano-efi-loader]

2. Replace the old kernel `id` with the one you copied from earlier. This goes on the line containing `default` in the config file.

3. Be sure to add a wildcard/asterisk after the `id` (no space in between). This ensures the same kernel is booted regardless of version number.

     ```sh
     default af2ba735c1714a3ebdd24c10355d5b20* # add wildcard *
     timeout 20  # wait time (sec) before system boots default
     console-mode auto
     reboot-for-bitlocker 1
     ```

4. Double check the kernel `id` you entered is an **exact match** with the one from `bootctl list`.

5. Press `Ctrl+X` to finish editing, then press `Y` to save the updated config.

---

## 3. Verify and reboot

1. Run `bootctl list` again to verify the desired kernel was set as default, indicated with `(default)` by the kernel title.

     ```sh
         type: Boot Loader Specification Type 1 (.conf) 
        title: EndeavourOS (6.19.12-arch1-1)  (default) # new default
           id: af2ba735c1714a3ebdd24c10355d5b20-6.19.12-arch1-1.conf
       source: ...
     ```

2. `Reboot` the system to check that the correct kernel boots by default.

---

## Additional information

**Useful resources:**
- [EOS Boot Configuration wiki][bootconfig]
- [Arch Linux kernels][archkernel]

[bootconfig]: https://deepwiki.com/endeavouros-team/EndeavourOS-ISO/3-boot-configuration
[archkernel]: https://wiki.archlinux.org/title/Kernel

---

### Find kernel id with `ls`

A list of the installed kernels can also be viewed with the `ls` command. This does not indicate which kernel is set to default, but has a much simpler terminal output.

1. Enter `ls /efi/loader/entries/` to display a list of the kernel entries.
      ```sh
      $ sudo ls /efi/loader/entries/
      1fcde8d015be4360aa122975ea19eca2-6.18.21-1-lts.conf	      1fcde8d015be4360aa122975ea19eca2-6.19.11-arch1-1-fallback.conf
      1fcde8d015be4360aa122975ea19eca2-6.18.21-1-lts-fallback.conf  af2ba735c1714a3ebdd24c10355d5b20-6.19.12-arch1-1.conf
      1fcde8d015be4360aa122975ea19eca2-6.19.11-arch1-1.conf	      af2ba735c1714a3ebdd24c10355d5b20-6.19.12-arch1-1-fallback.conf
      ```

2. The kernel id is the identifying string in front of the version number.
      ```sh
      # kernel id                      # version number
      af2ba735c1714a3ebdd24c10355d5b20-6.19.12-arch1-1.conf
      1fcde8d015be4360aa122975ea19eca2-6.19.11-arch1-1.conf	
      ```

3. Enter `ls -l /efi/loader/entries/` to list all kernel entries with last updated dates.

      ```sh
      $ sudo ls -l /efi/loader/entries/
      total 24
      -rw-r----- 1 root root 534 Apr  6 03:23 1fcde8d015be4360aa122975ea19eca2-6.18.21-1-lts.conf
      -rw-r----- 1 root root 565 Apr  6 03:23 1fcde8d015be4360aa122975ea19eca2-6.18.21-1-lts-fallback.conf
      -rw-r----- 1 root root 542 Apr  6 03:23 1fcde8d015be4360aa122975ea19eca2-6.19.11-arch1-1.conf
      -rw-r----- 1 root root 573 Apr  6 03:23 1fcde8d015be4360aa122975ea19eca2-6.19.11-arch1-1-fallback.conf
      -rw-r----- 1 root root 542 Apr 20 18:18 af2ba735c1714a3ebdd24c10355d5b20-6.19.12-arch1-1.conf
      -rw-r----- 1 root root 573 Apr 20 18:18 af2ba735c1714a3ebdd24c10355d5b20-6.19.12-arch1-1-fallback.conf
      ```

4. In most cases, the `(selected)` kernel is likely the last updated file. In this case, it would be the entry accessed on `Apr 20 18:18`.

---

### Check default kernel with `cat`

While `bootctl` provides detailed information on installed kernels, you can use `cat` to display the boot loader config file.

1. Enter `sudo cat /efi/loader/loader.conf` to display the boot loader config.

     ```sh
     $ sudo cat /efi/loader/loader.conf
     default af2ba735c1714a3ebdd24c10355d5b20*  # kernel id
     timeout 20
     console-mode auto
     reboot-for-bitlocker 1
     ```

---

<!-- EOF -->