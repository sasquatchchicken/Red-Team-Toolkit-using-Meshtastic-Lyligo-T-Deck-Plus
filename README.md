# Red-Team-Toolkit-using-Meshtastic-Lyligo-T-Deck-Plus
Version: 1.0

Platform: Windows w/ Lyligo T Deck Plus (Meshtastic 2.6.9 UI firmware)

Comm Method: LoRa-only (No IP/BLE/Wi-Fi)

Role: Secure Red Team Telemetry + Exfiltration Ops

A mission-switchable Python tool designed for Red Team covert simulation in air-gapped environments. It uses the Lyligo T Deck Plus running Meshtastic 2.6.9 UI firmware as a LoRa-based off-grid beaconing platform.
It is ideal for non-IP communications, passive telemetry, and counter-SDR evasion all within a secure training or adversarial research context.

**mission_launcher.py** is a field-ready, interactive TUI(tangible user interface) launcher engineered to simulate covert Red Team operations over an encrypted LoRa mesh. It interacts with a Lyligo T Deck Plus using meshtastic-cli, executing three operational modules:

1. Relay Obfuscation Node

2. Dead Drop Payload Exfil

3. ReAct Maneuver (hostile SDR detected)

All communication is AES-256-CBC encrypted, timestamped, jittered, and logged locally—ensuring no digital signature leakage beyond LoRa.

### Dependencies
```
pip install meshtastic pycryptodomex rich
```
### Set Up

**Flash your T Deck with Meshtastic UI 2.6.9 firmware.**

**Connect via USB (confirm COM port via Device Manager).**

**Open cmd prompt or PowerShell and configure:**
```
meshtastic.exe --port COMx --set region US915
meshtastic.exe --port COMx --set encryption.key <your_32_byte_key> #something you will generate
meshtastic.exe --port COMx --set channel.name OP_RED #this can be anything you choose
meshtastic.exe --port COMx --set device.role ROUTER ##simulated relay fuzzing
meshtastic.exe --port COMx --reboot

meshtastic.exe --port COMx --setdevice.role NODE   #for mobile/normal operation.
```
### Update mission_launcher.py with:
```
PORT = "COMx"  # Your T Deck COM port
KEY = b'xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx'  # 32-byte AES-256 key
IV = b'xxxxxxxxxxxxxxxx'  # 16-byte IV
```

### Launch GUI
```
python mission_launcher.py
```
### 
Choose from the menu:
```
[1] Relay Obfuscation Node
[2] Dead Drop Payload Exfil
[3] ReAct Maneuver
[4] Exit
```
###
Generated Files
```
    File	                                              Description
beacon_log.txt	                              Timestamped heartbeat messages sent by Relay module
rx_log.txt	                              Placeholder for future passive capture node
EXFIL_TRUTH_FILE_<timestamp>.txt	      Recon or sensitive payloads (e.g. OPFOR photos, SIGINT)
EXFIL_TRUTH_FILE_<timestamp>.txt.enc	      AES-256-CBC Base64 encrypted payload
```
### Use a decryption utility to decode captured logs
## Disclaimer 
**The AES generator, TUI launcher, and the decryption utility will not be made available or open source for the time being. However this may change in the future**
```
Strong_Random_Key_IV.py
mission_launcher.py
decrypt_payload.py
```
