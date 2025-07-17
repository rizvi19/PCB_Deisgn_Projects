# USB-C to UART Converter PCB

This repository contains the design files, schematics, and documentation for a custom USB-C to UART converter Printed Circuit Board (PCB). The project aims to provide a compact, reliable, and user-friendly solution for serial communication between a modern computer with a USB-C port and a microcontroller or other serial device operating at UART logic levels. The design leverages the **CP2102** USB-to-UART bridge IC, a USB-C connector, and ESD protection for robust performance.

## Features
- **USB-C Connectivity:** Modern, reversible USB-C connector supporting USB 2.0 Full Speed (12 Mbps).
- **CP2102 USB-to-UART Bridge:** Reliable single-chip solution for converting USB data to TTL-level UART signals.
- **ESD Protection:** LESD5D5.0CT1G diode array protects USB data lines from ±15 kV electrostatic discharge events.
- **Visual Feedback:** LEDs indicate power status and TX/RX data activity.
- **Compact Design:** Small form factor suitable for embedded systems development and prototyping.
- **Pin Header:** Provides easy access to UART signals (TX, RX, GND) and 3.3V power output.
- **Wide Baud Rate Support:** Configurable baud rates (e.g., 9600, 115200 bps) for compatibility with various microcontrollers.
- **Open-Source:** All design files (schematics, PCB layout, BOM) are available in this repository.

## Repository Contents
- `/schematics`: KiCad schematic files for the USB-C to UART converter.
- `/pcb`: KiCad PCB layout files and Gerber files for manufacturing.
- `/3d_models`: 3D visualization files of the assembled PCB.
- `/docs`: Project documentation, including the detailed design report (`USB-C_to_UART_Converter_Report.pdf`).
- `/bom`: Bill of Materials (BOM) listing all components with part numbers and suppliers.
- `LICENSE`: MIT License for the project.

## Hardware Overview
The PCB integrates the following key components:
- **CP2102:** Converts USB data to UART signals, enumerates as a Virtual COM Port (VCP) on the host computer.
- **USB-C Receptacle:** Provides a modern interface with VBUS (5V), GND, and USB 2.0 data lines (D+, D-).
- **LESD5D5.0CT1G:** ESD protection for USB data lines to enhance durability.
- **LEDs and Resistors:** Power LED (3.3V) and activity LED (TX/RX) with current-limiting resistors (330 Ω).
- **Capacitors:** Decoupling capacitors (0.1 µF, 1 µF, 4.7 µF) for power stability.
- **Pin Header:** 4-pin header for TX, RX, GND, and 3.3V output.

## User Manual
### Prerequisites
- A computer with a USB-C port and drivers for the CP2102 (available from [Silicon Labs](https://www.silabs.com/interface/usb-bridges/classic/device.cp2102)).
- A microcontroller or serial device with UART interface (3.3V or 5V logic levels).
- Jumper wires or a compatible connector for the pin header.
- Terminal software (e.g., PuTTY, Tera Term, or Arduino Serial Monitor) for serial communication.

### Setup Instructions
1. **Driver Installation:**
   - Download and install the CP2102 VCP drivers from [Silicon Labs](https://www.silabs.com/interface/usb-bridges/classic/device.cp2102).
   - Upon connecting the PCB to your computer via a USB-C cable, it should enumerate as a COM port (e.g., COM3 on Windows or `/dev/ttyUSB0` on Linux).

2. **Connecting to a Microcontroller:**
   - Connect the PCB’s pin header to your microcontroller:
     - **TX (PCB)** → **RX (Microcontroller)**
     - **RX (PCB)** → **TX (Microcontroller)**
     - **GND (PCB)** → **GND (Microcontroller)**
     - (Optional) **3.3V (PCB)** → Power input for the microcontroller (if needed, ensure current draw < 100 mA).
   - Use jumper wires or a compatible connector for secure connections.

3. **Configuring the Serial Port:**
   - Open your terminal software and select the appropriate COM port.
   - Set the baud rate to match your microcontroller (e.g., 9600, 115200 bps).
   - Configure other settings (typically 8 data bits, no parity, 1 stop bit, no flow control).

4. **Testing Communication:**
   - Power on the microcontroller and send data (e.g., via a simple `Serial.print()` in Arduino).
   - The activity LED on the PCB should blink during data transfer.
   - Verify that data appears in the terminal software and vice versa.

### LED Indicators
- **Power LED:** Lights up when the PCB is powered via USB (indicates 3.3V regulator is active).
- **Activity LED:** Blinks during TX or RX data transfers, providing visual feedback of serial communication.

### Troubleshooting
- **No COM Port Detected:** Ensure the CP2102 drivers are installed and the USB-C cable is functional (try a different cable/port).
- **No Data Transfer:** Verify TX/RX connections are correct (not swapped) and the baud rate matches on both devices.
- **LED Not Lighting:** Check USB power and connections; ensure the LED resistors are properly soldered.
- **Unstable Operation:** Inspect solder joints and verify that decoupling capacitors are correctly placed.

## Building the PCB
1. **Order Components:** Refer to the `/bom` directory for the Bill of Materials. Source components from suppliers like DigiKey, Mouser, or LCSC.
2. **Manufacture the PCB:** Use the Gerber files in `/pcb` to order the PCB from a manufacturer (e.g., JLCPCB, PCBWay).
3. **Assembly:**
   - Solder the USB-C receptacle, CP2102, ESD protection IC, capacitors, resistors, LEDs, and pin header.
   - Use a stencil for surface-mount components (e.g., CP2102) for best results.
   - Verify all solder joints for continuity and avoid shorts.
4. **Testing:** After assembly, connect the PCB to a computer and follow the setup instructions above.

## Design Notes
- **Differential Pair Routing:** USB D+ and D- lines are routed as a 90 Ω differential pair to ensure signal integrity.
- **Ground Plane:** A continuous ground plane minimizes noise and improves EMI performance.
- **ESD Protection:** The LESD5D5.0CT1G protects the CP2102 from voltage spikes, enhancing reliability.
- **Compact Layout:** The PCB is designed for minimal footprint, suitable for integration into larger projects or enclosures.

## Contributing
Contributions are welcome! Please submit a pull request or open an issue for bug reports, feature requests, or improvements. Ensure any changes are compatible with the existing design and follow the repository’s coding standards.

## License
This project is licensed under the MIT License. See the `LICENSE` file for details.

## Acknowledgments
- Thanks to Silicon Labs for the CP2102 documentation and drivers.
- Inspired by the need for a modern, reliable USB-to-UART interface for embedded systems development.