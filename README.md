# Iris rev6 — my QMK configuration

Keymap for the Keebio Iris rev6. CI builds the firmware and publishes the `.hex`
in the releases of this repository.

| Item | Value |
|---|---|
| Keyboard | `keebio/iris/rev6` |
| Keymap | `rcruzper` |
| MCU | ATmega32U4 |
| Bootloader | `atmel-dfu` |
| QMK | pinned in `.github/workflows/build_binaries.yaml` |

## Releases

- `latest`: always the most recent build of `main`.
- `vN-<commit>`: one per push to `main`. Use them to roll back.

## Flashing

You need `dfu-programmer`:

```bash
brew install dfu-programmer
```

Each half has its own MCU. **You must flash both** with the same file.
The hardware decides which hand is which, not the firmware.

### 1. Download

```bash
cd ~/Downloads
gh release download latest -R rcruzper/qmk_userspace
```

### 2. Separate the halves

> **CAUTION:** remove power before you touch the cable between the halves.

1. Unplug the USB.
2. Unplug the cable between the two halves.
3. Plug the USB into the left half only.

### 3. Enter the bootloader

- Press the reset button on the board once, **or**
- hold the center left thumb key (NAV layer) and press the top-left key.

### 4. Check and flash

```bash
dfu-programmer atmega32u4 get     # if it says "no device present", repeat step 3
dfu-programmer atmega32u4 erase --force
dfu-programmer atmega32u4 flash keebio_iris_rev6_rcruzper.hex
dfu-programmer atmega32u4 reset
```

### 5. Repeat on the right half

Unplug the USB, plug it into the right half and repeat steps 3 and 4.
The BOOT key is on the left half: for this half use the reset button.

### 6. Reconnect

Unplug the USB, connect the cable between the halves and plug in the USB.
Test one key on each side.

