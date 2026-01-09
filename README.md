# Iiyama Display Control Plugin for Q-SYS

## Overview
This Q-SYS plugin provides control and monitoring for Iiyama Interactive Displays (LHxx42UHS series and compatible) via TCP/IP or RS232. It supports essential functions like Power, Input selection, Volume, Mute, and Wake-on-LAN (WoL).

## Features
- **Connection Modes**: TCP/IP (Network) or RS232 (Serial).
- **Power Control**: On/Off with Wake-on-LAN (WoL) support for waking up displays from deep sleep.
- **Input Selection**: Direct switching for HDMI 1-3, DP, VGA, DVI, USB, OPS, and Android/iiWare.
- **Audio Control**: Volume and Mute control with real-time feedback.
- **Status Monitoring**: Connection status, Online indicator, and feedback synchronization.
- **Debug Mode**: Detailed hex logs for Tx/Rx/WoL frames.

## Installation
1. Download the `Iiyama_Display.qplug` file.
2. Place it in your Q-SYS Designer Plugins folder:
   - Typically: `Documents\QSC\Q-SYS Designer\Plugins`
3. Restart Q-SYS Designer.
4. Drag the "Iiyama Display Control" plugin from the Schematic Library > Plugins into your design.

## Configuration (Properties)
| Property | Description | Default |
|----------|-------------|---------|
| **Connection Type** | Choose between `TCP` or `RS232`. | TCP |
| **Host** | IP Address of the display (TCP mode). | 192.168.1.10 |
| **Port** | TCP Port (usually 5000 or 4660). | 5000 |
| **MAC Address** | MAC Address required for Wake-on-LAN functionality. Format: `AA:BB:CC:DD:EE:FF`. | 00:00:00:00:00:00 |
| **Baud Rate** | Serial baud rate (RS232 mode). | 115200 |
| **Monitor ID** | Display ID (Monitor ID in OSD). | 1 |
| **Poll Interval (s)** | How often to query status (0 to disable). | 5 |
| **Debug Print** | Enable detailed logging to Q-SYS Probe. | No |

## Usage
### Power & WoL
- The plugin uses "Smart Power On". If the TCP connection is active, it sends a standard Power On command.
- If the connection is lost (display is sleeping), it automatically sends a Magic Packet (WoL) to the configured MAC address.
- **Note**: Ensure WoL is enabled in the display's OSD menu.

### Inputs
Supported inputs:
- HDMI 1, HDMI 2, HDMI 3
- DisplayPort (DP)
- VGA
- DVI
- USB
- OPS (Slot-in PC)
- Android (iiWare)

## Protocol
Based on NEC/Iiyama Serial Protocol:
- **Header**: `0xA6`
- **Command Structure**: `Header + ID + Cat + Page + Len + Ctrl + Cmd + Val + Checksum`

## Author
**AGTOM sp. z o.o.**

## License
MIT License
