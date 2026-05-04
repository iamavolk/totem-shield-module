<picture>
  <source media="(prefers-color-scheme: dark)" srcset="/docs/images/TOTEM_logo_dark.svg">
  <source media="(prefers-color-scheme: light)" srcset="/docs/images/TOTEM_logo_bright.svg">
  <img alt="TOTEM logo font" src="/docs/images/TOTEM_logo_bright.svg">
</picture>


# ZMK config for the great TOTEM split row-staggered keyboard 


Originally conceived and designed by [GEIST](https://github.com/GEIGEIGEIST)  
Hardware files and the build process guide can be found [here](https://github.com/GEIGEIGEIST/totem)

![TOTEM layout](./docs/images/TOTEM_layout.svg)

## Why yet another ZMK config repo?
As it turns out, the shield (ZMK's parlance for the normies' term "keyboard") isn't in the upstream yet, and hasn't been
for quite some time. The original repo is unmaintained in the sense of keeping the firmware up to date as the ZMK and 
Zephyr projects move, and things get altered, and builds break and are no longer working as expected.  
So the goal of this repo is simple: to be up-to-date with the ZMK project since I personally use this stuff all day every day.

## My build

I used a replica of the original [Seeed Xiao nRF52840](https://wiki.seeedstudio.com/XIAO_BLE/) just because I already happened to 
have a TOTEM keyboard at the moment and was willing to experiment somewhat. The replica board
is more than twice as cheap (~$10 at the time of writing).


The default firmware uses standard QWERTY keyboard with (a variant of) Home-Row mods. 
As I use neither of those (I use a slightly customized [Graphite](https://github.com/rdavison/graphite-layout) layout, if you're curious; and home-row mods never really
grew on me since the delay, while being negligible, is nonetheless still real), my keymap tends to be 
quite different. However, the standart default firmware is included in the **artifacts** directory and you can just download it, flash your board
and test it out before delving any deeper into customizations.
[default firmware](./artifacts/)

### Here's a pic:
![build](./docs/images/build.png)

## User guide

- fork and clone the repo
- edit the [totem.keymap](./config/totem.keymap) file to match your preferred layout and functionality
- push the changes; this will automatically start the Actions build for the firmware
- download and unzip the resultant artifact (`firmware.zip`)
- connect the board, hit reset twice, mount the device (if not done automatically)
- copy the `.uf2` file (left, right -- pay attention to the file name and use commond sense) onto the device
- depending on the chip (original Xiao vs replica) you may need to wait a bit until it unmounts itself and disappears
    (if it doesn't you most likely have a bootloader issue)
- the Xiao might be finicky with the initial Bluetooth pairing. Here's what I recommend if you're experiencing connectivity issues and are unable to pair the device: 
    - turn off and connect the boards to your machine via USB
    - upload the [settings_reset-xiao_zmk.uf2](./artifacts/settings_reset-xiao_zmk.uf2) firmware to both
    - when the device unmounts and disappears, reconnect and remount
    - flash regular firmware
    - this procedure lets you start from clean slate. Don't forget to remove the bluetooth connection that may have been saved by the daemon
- There's a GUI/web interface, [ZMK Studio](https://zmk.dev/docs/features/studio), for those who prefer visuals and runtime updates to writing code-like configs and flashing firmware.
This is WIP at the moment but feel free to add it or submit a PR
