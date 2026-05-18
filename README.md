# zmk-sweep-config

ZMK firmware configuration for the **Ferris Sweep 34** split keyboard with nice!nano v2 controllers.

## Keyboard

- **Keyboard**: Ferris Sweep (Cradio) — 34 keys, split
- **Controllers**: nice!nano v2 (both halves)
- **Firmware**: ZMK

## Layers

| Layer | Activation | Description |
|-------|-----------|-------------|
| 0 BASE | — | QWERTY with mod-taps |
| 1 NAV/NUM | Hold left thumb | Numbers, navigation, arrows |
| 2 SYM/FN | Hold right thumb | Symbols, F-keys |

## Building firmware

Firmware is built automatically via GitHub Actions on every push to `main`.

Go to **Actions → latest run → Artifacts** to download the `.uf2` files.

To trigger a manual build: **Actions → Build ZMK firmware → Run workflow**.

## Flashing

> Flash the **right half first**, then the left. The left half is the Bluetooth central.

### Steps (repeat for each half)

1. Plug the nice!nano into your computer via USB-C.
2. **Double-tap** the reset button on the controller — the board mounts as a USB drive named `NICENANO`.
3. Drag the corresponding `.uf2` file onto the drive:
   - `cradio_left-nice_nano-zmk.uf2` → left half
   - `cradio_right-nice_nano-zmk.uf2` → right half
4. The board reboots automatically and the drive disappears — flashing is complete.

### If the drive doesn't appear

- Try double-tapping reset more quickly
- If the board was previously flashed and is unresponsive, hold the reset button for 5 seconds to force bootloader mode

## Pairing via Bluetooth

1. After flashing both halves, the two halves pair with each other automatically.
2. On your computer, open Bluetooth settings and connect to **Cradio** (or **Ferris Sweep**).
3. The left half is the central — keep it powered on when pairing.

To clear a Bluetooth profile: hold the key mapped to `&bt BT_CLR` (if configured) or reflash both halves.

## Keymap

```
Layer 0 BASE:
  Q  W  E  R  T    Y  U  I  O  P
  A  S  D  F  G    H  J  K  L  ;
  Z  X  C  V  B    N  M  ,  .  SFT/SL
       GUI/` SPC/1    BSPC/2 ALT/TAB

Layer 1 NAV/NUM (hold left thumb):
  1  2  3  4  5    6  7  8  9  0
 ESC CTL SFT _  END  LFT DN UP RT  '
  _  _  ?   _   _    _   _   _   _  ENT

Layer 2 SYM/FN (hold right thumb):
  F1 F2 F3 F4 F5   F6  F7 F8 F9 F10
 TAB _  _  "  {     -   =  [  ]  |
  _  _  _  '  }     _   +  _  _  BOOT
```

## Modifying the keymap

Edit `config/cradio.keymap` and push to `main` — GitHub Actions will build new firmware automatically.

For ZMK documentation: [zmk.dev/docs](https://zmk.dev/docs)
