
# System maintenance > Downgrade to specific date

## Downgrade to specific date

The `eos-shifttime` application can revert system packages to their state at a specified date. This tool is useful for when recent updates cause issues with system or program functionalities.

1. Open a terminal window and run `eos-shifttime` with root permissions.

2. Select the date to revert to on the GUI window, then click **Revert**.

      ![A GUI window for the `eos-shifttime` tool displaying a monthly calendar. The selected date is January 2, 2026.][eos-shifttime]

3. **Reboot** to apply the changes.

> [!IMPORTANT]\
> Using `eos-shifttime` does not revert AUR packages. The downgrade only applies to official Arch packages from the archive repositories.

The full `eos-shifttime` script can be viewed at `/usr/bin/eos-shifttime`. It was formerly known as the ["Easy Downgrade by Date"][downgrade] tool.

To set up `eos-shifttime` to conveniently run from the Welcome app, follow the steps in the [Set Up a Personal Command guide][set-command].


[downgrade]: https://discovery.endeavouros.com/pacman/easy-downgrade-by-date/2021/06/
[eos-shifttime]: ./images/eos-shifttime.png
[set-command]: 

---

<!-- EOF -->

