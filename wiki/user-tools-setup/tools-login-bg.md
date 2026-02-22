---
User tools & setup > Change login Background
---

# Change login background

Background images set in the **Login Window GUI editor** will only display if the system's `display manager` (DM) and/or `greeter` can access the specified image file.
- i.e. Setting the background image to a file in a general "Pictures" folder may not work.

[login-window-gui]: ../../images/login-window-gui.png
![Login Window GUI editor on the Appearance options tab, which contains options for General, Background, Themes, and Optional pictures selections.][login-window-gui]

If the image cannot be accessed, the login screen displays only the background color that was set.

By default, the EndeavourOS with an `xfce` desktop environment (DE) uses the following folders.

- `/usr/share/endeavouros/backgrounds` \- for default EOS backgrounds

- `/usr/share/backgrounds/xfce` \- for users using the XFCE DE

---

## Move image into system backgrounds folder

To create access without changing permission settings, move the desired image into the appropriate backgrounds folder.

1. With root permissions (`sudo`), move the intended background file into the display manager's background folder:
   
   ```sh
   sudo pacman mv /my/bg-file.png /usr/share/endeavouros/backgrounds
   ```

2. Then use `nano` to edit the `slick-greeter` config file. If this file doesn't exist, a new one will automatically be created:

    ```sh
    sudo nano /etc/lightdm/slick-greeter.conf
    ```

3. Apply the changes in the section with the `[Greeter]` heading.
   
    ```sh
    [Greeter]
    draw-grid=false
    background=/usr/share/endeavouros/backgrounds/bg-file.png
    ```

4. Press `Ctrl+X` to quit the editor, then press `Y` to save the file.

5. **Reboot** for the changes to take place.

---

<!-- EOF -->