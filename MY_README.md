# How to get everything working
### 1. Verify you can flash the keyboard with unmodified firmware
Complete all the instructions in the original [README](README.md) to verify you can successfully flash unmodified firmware. Some tips:
- Install `west` with brew.
- Install zephyr directly from https://docs.zephyrproject.org/latest/develop/toolchains/zephyr_sdk.html.
- https://github.com/zephyrproject-rtos/zephyr/issues/1392#issuecomment-2314762284 
- https://ibb.co/27BHS3GN from https://note.com/ryokucharyoku2/n/n70fae84f1898.
- The file to patch is `0001-esb-nrf-fix.patch` not `001-esb-nrf-fix.patch`.
- If flashing doesn't appear to be work, or is working inconsistently, try clicking "Reset Layout" in [Keychron Launcher](https://launcher.keychron.com/#/keymap) and then **stop** editing directly in Keychron Launcher. It seems to override values in the keymap.
- Keychron Launcher can be used to verify the time of the last successful firmware flash (`Settings -> Device Info -> Current Version`).

### 2. Edit keymap
Once you are able to complete everything listed on Step 1, edit app/boards/shields/keychron/b1/us/keychron_b1_us.keymap in the repo installed in Step 1.

### 3. Build
From `/app` run:
```
west build -b keychron -p -- -DSHIELD=keychron_b1_us
```
This will generate a uf2 file in zmk/app/build/zephyr. This is the file that will be flashed onto the keyboard.

### 4. Flash onto keyboard
Flash onto keyboard by following instructions in https://www.keychron.com/blogs/archived/how-to-use-the-launcher-web-app-or-manually-flash-firmware-for-your-b-pro-series-keyboard. Note: it doesn't matter if the uf2 file has a different name than what's currently on the keyboard. Dragging the uf2 onto the keyboard will still cause the keyboard to reboot with the new firmware (it will complain about ejecting, that's not a problem).

### 5. Verify
Verify changes with [Keychron Launcher](https://launcher.keychron.com).