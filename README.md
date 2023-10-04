# Boox Tab Ultra C custom hardware keyboard shortcuts

Removes some of the vanilla shortcuts and remaps a few too.

My raw notes below:

```
boox tab ultra c hardware keyboard shortcut redefinition
  - defined in /system/framework/framework-res.apk
    - /res/raw/bt-keypad.json
      - maps the f-keys (f1, f2, etc)
      - discovered that you can't remove entries from this JSON
      - so did "identity" remaps where each
        f-key mapped to itself (instead of some function)
    - /res/raw/keypad_color.json
      - here we largely have combinations
        - like Alt-Tab
      - here you can remove entries
      - so removed some and added some
        - added shortcuts for toggling backlight and opening backlight control dialogs
        - not sure how to control brightness or color with keys directly
    - /res/raw/keypad.json
      - this file is not used, can ignore
  - the basic workflow is
    - retrieve framework-res.apk from the android device
      - can't be accessed directly via adb pull
        - so have to do adb shell, then su, then copy over to Downloads, then adb pull from there
    - unzip
    - make changes
    - rezip
    - make a magisk module out of it
      - just zip it up, the zip file's name might have to match the module id defined in the module properties file
    - adb push the module to the device
    - adb shell, then su, then magisk --install-module module.zip, then reboot
      - installing via the magisk ui would fail, for some reason
  - when I would mess something up the android gui wouldn't boot
    - would be stuck at loading screen
    - but i would still be able to access device via adb shell, then su, then magisk --remove-modules
    - important to have su permission granted to shell via magisk beforehand
      - and have it be forvever
        - otherwise might not be able to recover via adb shell (su won't work)
          - because su permission might run out
  - jumped through a few hoops to get magisk module working
    - not sure what the problem was
```

## Patch file

Added to the root of module [a patch file](https://github.com/dmos62/boox-tab-ultra-c-custom-hw-keyboard-shortcuts/blob/main/framework_res.patch) of changes I made (it doesn't have a functional effect). Useful if I ever want to look at what changes I made or if I have to remake them on top of an updated apk.
