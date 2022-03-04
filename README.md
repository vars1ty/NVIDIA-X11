# NVIDIA-X11
A guide on how to make your experience with dual monitors on X11 with NVIDIA smoother with mixed refresh-rate monitors.
## Syncing refresh-rate
To sync your refresh-rate to whichever monitor you want, follow these basic steps:
1. Open `/etc/environment` inside any text-editing program you want with sudo permissions
2. Add these flags to the end of the file:
   - `CLUTTER_DEFAULT_FPS=YOUR_REFRESH_RATE`
   - `__GL_SYNC_DISPLAY_DEVICE=DESIRED_MONITOR_INPUT` -- This can be found inside nvidia-settings (for ex: `HDMI-0`)
   - `__GL_SYNC_TO_VBLANK=0`
3. Save the file, then run `sudo nvidia-settings` and enable `Force Composition Pipeline` on **all** of your displays! ![image](https://user-images.githubusercontent.com/54314240/156833269-5cf5a3ad-c2f3-489d-a356-4c9eb7eec33a.png)
   - This option is only visible after you press the "Advanced" button.
4. Open the `OpenGL Settings` tab and disable `Sync to VBlank` and `Allow Flipping` if they are enabled or available
5. Go back to `X Server Display Configuration` and save your configuration, then restart your computer.
## Disabling V-Sync inside picom (a.k.a Compton)
This is required because otherwise you may experience stuttering issues when scrolling!
***
1. Open `~/.config/picom.conf` inside any text-editing program you want
2. Search for `vsync =` and change the value to `false` like shown here ![image](https://user-images.githubusercontent.com/54314240/156833869-9558a257-77c8-4fd9-9b74-1e280706a666.png)
3. Save the file and restart your computer.
## Done
Congrats, you went through the forest of NVIDIA + X11 Hell while Wayland and NVIDIA still struggle like most casual teenage e-relationships.
## Bonus Tip
If you like having `Allow Flipping` on, then follow these steps to optimize picom:
1. Open `~/.config/picom.conf` inside any text-editing program you want
2. Find the line where it says `backend =`, change the value to `xrender`. The end result should look like this ![image](https://user-images.githubusercontent.com/54314240/156851395-1140772e-248a-4e43-9500-64d9af0ce7c7.png)
3. Save and exit out of the file, then preferably restart your computer so everything is fully updated.
4. Enable `Allow Flipping`
5. Done


Enabling this makes your FPS in several games increase by a fair bit, while also allowing you to have smooth scrolling just like if it was off.

Without setting the backend to xrender and keeping `Allow Flipping` on, scrolling will most likely become extremely laggy for you and you may also notice slight FPS decreases inside games and other applications (use glxgears as an example to measure the gains and losses).
