# dSPACE V2Gshark Wireshark Plugin
[![Release](https://img.shields.io/github/v/release/dspace-group/dsV2Gshark?label=release)](https://github.com/dspace-group/dsV2Gshark/releases)
[![dSPACE](https://img.shields.io/badge/-OpenSource%20powered%20by%20dSPACE-blue)](https://www.dspace.com/)

## Overview
This Wireshark plugin allows to analyze and decode packets between electric vehicles (EV) and charging stations (EVSE), also known as V2G messages.  

![ISO 15118-2 Overview](Images/WS_ISO15118_2_Overview.png)

## Features

### Overview
- Supports decoding of:
    - V2GTP layer (Vehicle to Grid Transport Protocol)
    - SAP messages (Supported App Protocol)
    - SDP messages (SECC Discovery Protocol)
    - DIN 70121  messages
    - ISO 15118-2 messages
    - ISO 15118-20 messages (preliminary support)
- Additional analysis features:
    - Validation of V2G messages according to XSD specification
    - Certificate information details for Plug & Charge (PnC)
    - Live TLS decryption
- Automatic schema detection
    - Detect schema automatically in case of missing SDP or SAP
- Color filter for V2G packets
- Filter buttons for V2G packets
- Wireshark I/O Graph support for V2G packets

### Live TLS Decryption
The plugin processes a TLS master secret disclosure packet after handshake to decode the following V2G session.  
The disclosure message is a UDP packet within the source port range 49152-65535 (see Wireshark protocol settings) containing the ASCII string "CLIENT_RANDOM <32-byte client random> <48-byte master secret>" as payload data. This disclosure message has to be sent from one of the communication partners in a testing environment.

### Wireshark I/O Graph
This optional feature updates the Wireshark I/O Graph preferences to display a V2G session. The graph can be accessed via 'Statistics' -> 'I/O Graphs' (shortcut: Alt + S + I).  
The graph displays the data in 1 second intervals. This can be changed using the drop down menu at the bottom.  
To simplify the visualisation, some V2G related signals (e.g., MaxVoltage) are disabled by default. They can be enabled using the check boxes in the selection view.  
Click on a packet in the graph to inspect it in the Wireshark main window. Press the SPACE key to activate a helper line on the graph if you need more precision.

## Requirements
- Wireshark (64 bit) 3.5.0 or higher
- Operating Sytems:
    - Windows 7 or higher
    - Linux x64 (see [Limitations](#limitations))
    - Mac OS currently not supported

## Installation notes
- The installer can be downloaded from [GitHub Releases](https://github.com/dspace-group/dsV2Gshark/releases/latest)
- When updating Wireshark, please reinstall the plugin to avoid any warnings
- Not compatible with other V2G dissector plugins. Please uninstall these plugins before installing dsV2Gshark.
- Not compatible with 32 bit versions of Wireshark.
- Updates of the plugin can be performed directly without uninstalling the old version.
- Installation size is about 10 MB
- Supports normal and portable version of Wireshark
- Filter buttons and color filters will be installed for the current user only. In multi-user environments, the plugin must be installed for each user to enable these two optional features.

## Limitations
- ISO 15118-20 is not fully supported yet
    - some BPT messages are not fully decoded
- Live TLS decryption is only supported for TLS 1.2
- Linux
    - no installer
    - filter buttons and color filters must be added manually

## Support
- If you encounter any problems, feel free to open an issue or contact us at support@dSPACE.de
- We appreciate all contributions, from reporting bugs to implementing new features

## Further notes
- When sniffing V2G communication, lost packets may occur, which cause corrupted TCP/TLS sessions. In that case, it may help to activate the option to ignore Message Authentication Code (MAC) check failures in the Wireshark TLS protocol settings.  
    This option can be found under Wireshark Preferences - Protocols - TLS
- This plugin was built and tested with Wireshark 4.2.3
- The EXI decoding is based on [cbExiGen](https://github.com/EVerest/cbexigen)


## Screenshots
### Message Inspection
![ISO 15118-2 CurrentDemand](Images/WS_ISO15118_2_CurrentDemand.png)
### Certificate Details
![ISO 15118-2 Certificates](Images/WS_ISO15118_2_Certificate.png)
### Message Validation
![ISO 15118-20 Message Validation](Images/WS_ISO15118_20_MsgValidation.png)
### Live TLS Decryption
![ISO 15118-2 Live TLS](Images/WS_ISO15118_2_LiveTLS.png)
### Filter Buttons
![Filter Buttons](Images/WS_FilterButtons.png)
### Plugin Preferences
![Plugin Preferences](Images/WS_Preferences.png)
### Wireshark I/O Graph
![I/O Graph](Images/IO_Graph.png)
