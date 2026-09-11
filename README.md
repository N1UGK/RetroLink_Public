# RetroLink (POTS Telephone Internet Interface)

RetroLink connects a standard POTS (Plain Old Telephone Service) analog telephone to the Internet over Wi-Fi, allowing peer-to-peer calling between devices and retro telephony interfacing.  The RetroLink is intended for private telephone networks in the same building, campus, or even across the globe.  It will not require subscription fees or a third party "app" or platform to use.  The idea came from my daughter (who is 6) asking for a phone to call her friends.  This device can be configured for connecting a close circle of friends or family and using their chosen "phone number" to dial and connect to them.  Any standard "retro" telephone can be plugged into the RetroLink.

<img alt="RetroLink" src="https://n1ugk.com/wp-content/uploads/2026/09/RetroLink.jpeg" />

## Overview

RetroLink provides a complete, self-contained telephone line interface for real analog telephones (both rotary and DTMF touch-tone). It generates real ringing voltages, provides line battery feed, detects off-hook and on-hook states, digitizes 2-wire voice audio with hardware codecs, and streams bidirectional voice data over Wi-Fi.

## Key Features

- **True POTS Line Interface**: Powered by the **Silvertel Ag1170-S5** SLIC with an onboard DC/DC converter generating -48V loop battery and 65Vrms ringing directly from a 5V supply.
- **Hardware Voice Codec**: **Texas Instruments TLV320AIC1110** providing 8 kHz PCM sampling, companded G.711 µ-law encoding, digital PGA gain control, and programmable sidetone.
- **Microcontroller**: **Raspberry Pi Pico 2 W** (RP2350 with dual ARM Cortex-M33 / Hazard3 RISC-V cores and onboard CYW43 Wi-Fi).
- **Dual-Core Architecture**:
  - **Core 0**: Real-time audio engine with DMA/PIO double buffering, low-latency audio packetization, and SLIC line supervision (hook switch debounce & ring cadence).
  - **Core 1**: CYW43 Wi-Fi stack, lwIP networking, VoIP stream/control protocol, web status interface, and OLED display navigation.
- **User Interface**:
  - 128x64 SSD1306 OLED display via I2C (0x3C)
  - 4-button tactile keypad (Up, Down, OK, Back) via MAX7329 GPIO expander (0x3A)
  - 7 Status LEDs (Off-Hook, MicroSD, Voice Mail, Ringing, Connected, Wi-Fi Link, Error) via MAX7329 (0x38)
- **Local Storage & USB**:
  - MicroSD card slot over SPI0 with FatFS for address books, call logs, and voicemail storage.
  - TinyUSB USB Mass Storage support for mounting the SD card on a PC or Mac.
- **Web Dashboard & Control**:
  - Embedded HTTP server for real-time OLED screen viewing, virtual button control, device status, and network configuration.
- **Secure Firmware Updates**:
  - Dedicated 64 KB custom bootloader with OTP key verification and drag-and-drop UF2 updates over USB.

## Hardware Specifications

| Component | Specification |
|---|---|
| Microcontroller | Raspberry Pi Pico 2 W (RP2350 @ 150MHz) |
| SLIC Module | Silvertel Ag1170-S5 (5V, 600Ω 2-wire impedance) |
| Ring Generator | Onboard Ag1170 ringing (65Vrms @ 20Hz, REN 3 capable) |
| Voice Codec | TI TLV320AIC1110 (PCM / G.711 µ-law, 8 kHz) |
| Display | 0.96" 128x64 I2C OLED (0x3C) |
| I/O Expanders | 2x MAX7329 I2C Expanders (0x38, 0x3A) |
| Power Supply | Single 18650 Li-Ion Cell with BQ24090 Charger & MCP1642B 5V Boost |
| Connector | Standard RJ-11 6P4C Modular Phone Jack |

## Firmware Updates

To update the firmware:
1. Place RetroLink into bootloader mode via the OLED menu: `Settings -> Update Firmware`, or hold the bootsel/startup button combo on power-up.
2. Connect RetroLink to your computer via USB. A mass-storage drive named `RETROLINK` will appear.
3. Drag and drop the latest release `.uf2` file from the `Firmware/` folder onto the drive.
4. The bootloader will verify and flash the image, then automatically reboot into the new firmware.

## Repository Structure

- `Firmware/`: Official firmware release binaries (`.uf2`) and release notes.
- `Hardware/`: 3D CAD STEP models, schematics, and mechanical design files.
- `Documentation/`: User guides, application notes, and reference manuals.
>>>>>>> b99fa2f (Initial commit for RetroLink_Public repository structure)
