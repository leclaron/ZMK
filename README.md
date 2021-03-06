# Zephyr™ Mechanical Keyboard (ZMK) Firmware

[![Build](https://github.com/zmkfirmware/zmk/workflows/Build/badge.svg)](https://github.com/zmkfirmware/zmk/actions)
[![Contributor Covenant](https://img.shields.io/badge/Contributor%20Covenant-v2.0%20adopted-ff69b4.svg)](CODE_OF_CONDUCT.md)

This project is a complete work in progress, with absolutely nothing functioning yet. The goal is to explore a new MK firmware
with a less restritive license and better BLE support, built on top of the [Zephyr™ Project](https://www.zephyrproject.org/)

Check out the website to learn more: https://zmkfirmware.dev/

## TODO

- Document boards/shields/keymaps usage.
- Display support, including displaying BLE SC auth numbers for "numeric comparison" mode if we have the screen.
- Fix BT settings to work w/ Zephyr. Do we really need them?
- Tests?

# Missing Features

- Layer Tap
- One Shot
- Combos
- Tap Dance
- Shell over BLE?
- Split support
  - custom kscan driver? that recieves events from other side over BLE notifications?
  - Need to figure out how to do "custom" GATT services. Custom UUID?
  - Do we need to send any state updates over from primary to secondary side?
- Encoders
- Battery reporting.
- Low power mode, with wakeup from interrupt?
- Better keymaps to avoid needing extra KC_NO for locations in the matrix that don't even exist!

## Long Term

- Tool to convert keymap `info.json` files into a DTS keymap file?
- Firmware build service?
