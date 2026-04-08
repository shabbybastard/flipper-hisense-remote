# Flipper Zero Hisense TV Remote

This is a custom Hisense TV remote application for the Flipper Zero, designed to demonstrate how to build a custom user interface and send specific, hard-coded infrared (IR) commands.

The application features a unique vertical layout, intended for use when holding the Flipper sideways so the IR port can be pointed at a TV like a traditional remote.

## Features

* **Custom Graphical UI:** A complete, custom-built user interface with buttons, icons, and a selection highlight.
* **Rotated Vertical Layout:** The UI is rotated +90 degrees to be used like a conventional remote control.
* **Remapped Directional Input:** The physical D-pad is re-mapped to provide an intuitive navigation experience in the rotated orientation.
* **Visual & Haptic Feedback:** The Flipper's LED blinks purple and the device vibrates briefly every time an IR command is sent.
* **Hard-coded IR Signals:** The application does not rely on `.ir` files. Instead, it sends specific Hisense IR protocols directly from the code, serving as a clear example for developers.

## Example: Sending a Custom IR Command

This application is a great example of how to send specific, known IR commands directly in your C code without needing to load external `.ir` files. The core logic is handled in the `send_ir_code` function.

Here's a breakdown of how the "Power" button command is sent:

```c
static void send_ir_code(TvButton button, NotificationApp* notifications) {
    // ... (feedback notifications) ...

    uint32_t address = 0xBF00; // Hisense extended NEC address: 00 BF 00 00
    uint8_t command;

    switch(button) {
    case Button_Power:
        command = 0x0D; // Power: 0D F2 00 00
        break;
    // ... other cases ...
    }

    // 1. Allocate memory for an InfraredSignal
    InfraredSignal* signal = infrared_signal_alloc();
    furi_check(signal);

    // 2. Create an InfraredMessage with the correct protocol, address, and command
    InfraredMessage message = {
        .protocol = InfraredProtocolNECext, // Extended NEC protocol for Hisense TVs
        .address = address,
        .command = command,
        .repeat = false
    };

    // 3. Assign the message to the signal structure
    infrared_signal_set_message(signal, &message);

    // 4. Transmit the signal
    infrared_signal_transmit(signal);

    // 5. Free the allocated memory
    infrared_signal_free(signal);

    // ... (delay and LED reset) ...
}
```
This demonstrates the fundamental process: define the protocol, address, and command, then use the `infrared_signal` library to build and transmit the signal.

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

**Author:** Tyler Berndt  
**Website:** https://purplefox.io  
**GitHub:** @purplefox-io

All credit for the original application design, architecture, and implementation goes to the original author.

## License

This project is licensed under the MIT License - see the LICENSE file for details.
