# Kodak Charmera firmware: build v008_test (Nov 19 2025)

Firmware read from a Kodak Charmera keychain camera with a SuperPix SP140A-class sensor, and published as a restore file by Hyperlite-Media/charmera-film-mods. I can't confirm where it sits in the release waves, but I wanted to make sure it was kept hosted somewhere just in case. Copy kept here so owners can **study and repair their own cameras**.

## No rights claimed

- **We claim no copyright, ownership, license or other right** in this firmware. All rights belong to their respective owners: the chip vendor (GeneralPlus) and the maker of the camera sold under the Kodak brand. "Kodak" is a trademark of its owner. This repository is **not affiliated with or endorsed by** Kodak, GeneralPlus or the camera's maker.
- The file is offered **only for reference, interoperability and repair**, free of charge. It is not sold or licensed, and nothing here grants any right to use it for anything else.
- **Takedown:** if you hold rights in this file and want it removed, open an issue. It will be taken down promptly.
- Provided as is, with no warranty. Flashing firmware can leave a camera unable to start. Mess with this at your own risk.

## File Details

| Field | Value |
| --- | --- |
| File | `charmera-v008_test-2025-11-19.bin` |
| Size | 1,478,656 bytes (`0x169000`, firmware-only update file) |
| SHA-256 | `5b352e46f1f52175cb4da2278be8db32ecc36be4943424d58cfd8e2cc9c4386f` |
| Build | `v008_test`, compiled Nov 19 2025 |
| Version stamp | `202505201029`, build string `JH5408  20250520` |
| Target Sensor | SuperPix SP140A-class (8-bit registers, bus address 0x78) |
| Initial Source | the public restore file `JH_5408202505201029_0852C329.bin` from Hyperlite-Media/charmera-film-mods (release Charmera_Restore) |

## Which Charmera does this work for?

- The firmware version needed is driven by which image sensor your camera has. This build drives an **SP140A-class** sensor only, with the same sensor init table as `v006`.
- WARNING: On cameras with any other sensor, including the **OmniVision OV9732**, this build starts and its menus work, but it will *not* be capable of using the camera. Attempting to access Photo or Video modes will cause the camera to freeze until shut down. Those cameras need build `v012` (see charmera-firmware-v012).
- The version stamp doesn't tell builds apart: `v006`, `v008_test` and `v012` all report `202505201029`. The build name is the factory's source-folder name, left inside the image in its source paths, and the compile date differs.
- **Hypothetical method to determine Charmera version without opening the camera:** look at a photo the camera took on its original firmware. `v008_test` and `v006` write the same 1,424-byte JPEG header with an EXIF block that names "Generalplus" / "CBB3", so a photo can't tell those two apart. `v012` writes a bare 624-byte header with no EXIF.
  - NOTE: I only have the v012 OmniVision version of the camera, so this has not been tested.

## Source

Published unchanged from the public restore file `JH_5408202505201029_0852C329.bin` in Hyperlite-Media/charmera-film-mods (release Charmera_Restore).

- It is complete firmware (boot header, code and resource pack) but not a full chip image.
- It holds nothing of a camera's own area (no settings, no photos), so there was nothing to clean.

## How to Use

- **Flashing it from a card resets your settings.** The updater's final erase for a file of this size wipes the settings bank, so the camera starts with factory settings. Photos on the card are not touched.
- Options:
  - **Flash from a card:** rename it to `JH_5408<stamp>_0852C329.bin` and put it in the card's root folder.
    - `0852C329` is the file's byte sum, which the updater checks. Keep it as is.
    - `<stamp>` is 12 digits. The updater compares it with the stamp of the firmware the camera is running and skips the file when they are equal. Every known factory build runs `202505201029`, so on one of those cameras use any other 12 digits, for example `JH_5408202505201030_0852C329.bin`. The file's original name only works on a camera running something else.
  - **Chip clip and programmer:** Writing the file to the start of the chip with a clip and a programmer also works but will require opening the camera.
- The only secure method is to **read your own camera's chip** before flashing anything. That read is the **only certain way to recover a bad flash**.
