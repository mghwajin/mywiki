# Shell scripts

**Custom shell scripts** can be used to create useful shortcuts or automated tasks for your system. `eos-update` is an example of a script that provides advanced functions/options.

The scripts included in this repo are detailed below.

| Script  | Description           |
| ------- | --------------------- |
| [Autosave screenshot][a] | Requires `xfce4-screenshooter`. Instantly and automatically save a fullscreen screenshot with the date appended to the filename. Running this script bypasses the window waiting for filename input from the user. |
| [Convert video to MP3][b] | Requires `ffmpeg` and `thunar` file manager. Runs a custom action in `thunar` to convert a selected video file into an `.mp3` file. This script sets `ffmpeg` to use VBR (variable bit rate) for the highest possible audio quality for conversion. |

<!-- script links -->
[a]: scripts/xfce4-screenshooter-autosave.sh
[b]: scripts/thunar-convert-to-mp3.sh


## Tips

Generally, if you are using a custom script written by another user, you need to make adjustments to the script for it to work on your system.

- For example, a script referencing `/home/some-username` should be edited to match your `/home/your-username` directory.

- Be sure to set the `script.sh` file as an executable file by using the `chmod +x script.sh` command.

> [!TIP] \
> It is recommended to create a `/home/user/bin` directory to place scripts in for easy file access and organization.

---