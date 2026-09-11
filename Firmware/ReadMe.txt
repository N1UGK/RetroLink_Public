RetroLink Firmware Release Notes

Note - In order to update the firmware, you will need to place the RetroLink into bootloader mode. This can be done via the OLED display menu: Settings -> Update Firmware, or by holding the configured startup button combination on power-up.

RetroLink will reboot into its bootloader mode. Plug RetroLink into a Mac or PC with a USB cable, and drag and drop the firmware file onto the removable drive that appears.

The RetroLink bootloader will decrypt the firmware file, verify the signature, and if it passes, it will flash the image and reboot.

Note that the RetroLink bootloader is distinct from the default RP2350 ROM bootloader — if you use the BOOTSEL button on the Pico 2 W directly, the ROM bootloader cannot decrypt signed RetroLink firmware images. You can determine which bootloader is active by checking the directory contents of the USB drive:
- If you see `RetroLink.txt` / `INFO_UF2.TXT` with RetroLink identifiers, you are in the RetroLink Custom Bootloader.
- If you see default Raspberry Pi files, you are in the RP2350 ROM bootloader.

--------------------------------------------------------------------------------
09-11-2026 - RetroLink_V1.00_B0001.uf2

- Initial firmware release shell for RetroLink (Raspberry Pi Pico 2 W / RP2350).
- Drivers:
  - Ag1170 SLIC: hook switch detection, debounce, ring-trip auto-cancel, 20Hz ring cadence generator, power down.
  - TLV320AIC1110 voice codec: 8 kHz PCM sampling, I2C register configuration, PGA volume/gain controls.
  - SSD1306 128x64 OLED display: real-time status display and menu navigation.
  - MAX7329 I/O expanders: 4 tactile buttons and 7 status LEDs (OH, SD, VM, RNG, CON, LNK, ERR).
  - SD Card / FatFS: SPI0 storage with USB Mass Storage bridge.
  - Wi-Fi & Web UI: CYW43 Wi-Fi connection, SNTP network time sync, and remote HTTP status dashboard.
