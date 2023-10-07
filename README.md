# BB40 ZMK Config

## Instructions

1. You will need to [sign up for a GitHub account](https://github.com/signup), and [fork this repository](https://docs.github.com/en/get-started/quickstart/fork-a-repo#forking-a-repository) so you can edit it.
2. Navigate to the **Actions** tab and click the "I understand my workflows, go ahead and run them" button to enable builds.
   ![Actions tab with "I understand my workflows" button](https://i.imgur.com/B7cTAE6.png)
3. Edit [config/bb40.conf](config/bb40.conf) to enable/disable features. Edit [config/bb40.keymap](config/bb40.keymap) to change the keymap. Lastly, make sure the [build.yaml](build.yaml) file has your board in the "boards" list.
4. After committing your changes, your firmware will begin compiling. Assuming there are no typos or other problems, it will eventually be [downloadable from the Actions tab](https://zmk.dev/docs/user-setup#installing-the-firmware).
5. [Flash the firmware](https://zmk.dev/docs/user-setup#flashing-uf2-files) that matches the board you're using, e.g. `bb40-pillbug-zmk.uf2` for a PillBug.

## Common Questions/Problems

### There was an error and the build didn't finish.

#### There is probably an error in your keymap.

Carefully double-check the last changes you made. ZMK syntax is very different from QMK syntax. Note that when editing keymaps, each ZMK code is generally preceded by a reference categorizing what that code does.

For example: the letter "Z" is categorized as a **k**ey **p**ress. To add the letter "Z" to a keymap, it must be written `&kp Z`.

A few more examples below:

| QMK | ZMK |
| --- | --- |
| `KC_A` | `&kp A` |
| `QK_REBOOT` | `&sys_reset` |
| `LT(1, KC_SPACE)` | `&lt 1 SPACE` |

There are many, many more differences. Don't forget to [check the ZMK docs](https://zmk.dev/docs/features/keymaps).

[nickcoutsos's in-browser keymap editor](https://nickcoutsos.github.io/keymap-editor) aims to provide a GUI for remapping, which may be helpful.

### The encoder doesn't work.

#### Double-check the features in the [config/bb40.conf](config/bb40.conf) file.

And double-check the Kconfig file in the build results to make sure what you've enabled is really enabled.

### The indicator LEDs don't work.

As of this firmware's creation time, ZMK does not support indicator LEDs. If desired, they could be configured as part of the backlighting feature with some [additional](https://zmk.dev/docs/features/backlight) [configuration](https://zmk.dev/docs/config/backlight).
From top to bottom, the LED pins are `&blackpill 43`, `&blackpill 45`, and `&blackpill 46`.

### After disconnecting the BB40 from Bluetooth, it won't reconnect.

#### Forget the Bluetooth connection on both the BB40 and the device, then try re-pairing.

If you don't remember which profile on the BB40 was used to connect to a specific device, this may mean cycling through each (`&bt BT_PRV`/`&bt BT_NXT`) and clearing them (`&bt BT_CLR`) one by one. [See ZMK's documentation for more info](https://zmk.dev/docs/behaviors/bluetooth#bluetooth-pairing-and-profiles).

As a last resort, try flashing the `settings_reset` firmware for your board; this will force-clear everything.

## Further Troubleshooting Resources

- [ZMK's troubleshooting page](https://zmk.dev/docs/troubleshooting)
- Stop by #keyboard-help in [MechWild's Discord](https://discord.gg/nfxHnsm)
- Ask the ZMK experts in [ZMK's Discord](https://zmk.dev/community/discord/invite)
