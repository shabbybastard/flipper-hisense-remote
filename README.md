# Flipper Zero Hisense TV Remote

This is a custom Hisense TV remote application for the Flipper Zero, designed to demonstrate how to build a custom user interface and send specific, hard-coded infrared (IR) commands.

The application features a unique vertical layout, intended for use when holding the Flipper sideways so the IR port can be pointed at a TV like a traditional remote.

## Features

* **Custom Graphical UI:** A complete, custom-built user interface with buttons, icons, and a selection highlight.
* **Rotated Vertical Layout:** The UI is rotated +90 degrees to be used like a conventional remote control.
* **Remapped Directional Input:** The physical D-pad is re-mapped to provide an intuitive navigation experience in the rotated orientation.
* **Visual & Haptic Feedback:** The Flipper's LED blinks purple and the device vibrates briefly every time an IR command is sent.
* **Hard-coded IR Signals:** The application does not rely on `.ir` files. Instead, it sends specific Hisense IR protocols directly from the code, serving as a clear example for developers.
* **D-Pad Capture Mode:** A special mode where physical D-pad buttons directly send IR commands without UI navigation.

## Operating Modes

The application supports two operating modes:

### Normal Mode
In normal mode, you navigate through the on-screen buttons using the D-pad and press OK to send the selected IR command:
- **D-pad** — navigate between buttons
- **OK** — send IR command for selected button
- **Hold Back** — exit the application

### Capture Mode
Capture mode allows you to use the Flipper like a traditional TV remote where physical buttons directly control the TV:
- Press the **cptr** button to activate capture mode
- In capture mode, physical D-pad buttons send IR commands directly:
  - **↑ ↓ ← →** — send directional IR commands
  - **OK** — send Enter IR command
  - **Back** — send Back IR command to the TV
- **Hold Back** — exit capture mode and return to normal mode
- The screen displays "capture mode" indicator at the bottom when active

## Compatibility

This application was tested and verified to work on:
- **Firmware:** [Momentum](https://github.com/Next-Flip/Momentum-Firmware) `mntm-012`

## Building the Application

### Prerequisites

This application is built using the standard **fbt** (Flipper Build Tool) that comes with the Flipper Zero firmware.

### Setup

1. Clone the Flipper Zero firmware repository:
```bash
git clone --recursive https://github.com/flipperdevices/flipperzero-firmware.git
cd flipperzero-firmware
```

2. Clone this repository into the `applications_user` folder:
```bash
cd applications_user
git clone https://github.com/shabbybastard/flipper-hisense-remote.git hisense
cd ..
```

### Build Commands

**Build the app:**
```bash
./fbt fap_hisense
```

**Build and launch on Flipper (via USB):**
```bash
./fbt launch APPSRC=applications_user/hisense
```

**Build app for distribution:**
```bash
./fbt fap_dist
```

The built `.fap` file will be located at `dist/f7-C/apps/Tools/hisense.fap`

---

## Acknowledgments

This project is a modified version of the **Flipper Zero Samsung TV Remote** originally created by:

**Original Author:** Tyler Berndt  
**GitHub:** @purplefox-io

All credit for the original application design, architecture, and implementation goes to the original author.


Neuroslop warning - The code has been modified and adapted by AI

## License

This project is licensed under the MIT License - see the LICENSE file for details.
