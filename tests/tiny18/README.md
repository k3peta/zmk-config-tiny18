# Tiny18 native simulator tests

These tests run the production `config/tiny18.keymap` on ZMK's
`native_sim//zmk_test_mock` target. Each test replaces the physical key scanner
with a deterministic 1 x 18 mock scanner, injects press/release events, and
compares the emitted HID key events with a checked-in snapshot.

Run the suite from a Linux ZMK workspace:

```sh
ZMK_EXTRA_MODULES=/path/to/zmk-config-tiny18 \
  west test /path/to/zmk-config-tiny18/tests/tiny18
```

The GitHub Actions firmware workflow runs this suite in ZMK's official Zephyr
4.1 build container. The suite validates keymap logic only; GPIO wiring, the
XIAO bootloader, BLE radio behavior, batteries, and physical RGB LEDs still
require real-device testing.
