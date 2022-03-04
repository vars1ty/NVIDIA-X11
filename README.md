# NVIDIA-X11
A guide on how to make your experience with dual monitors on X11 with NVIDIA smoother
## Syncing refresh-rate
To synd your refresh-rate to whichever monitor you want, follow these basic steps:
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
