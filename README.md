# Gridwalk

A fast, multi-threaded Python network scanner designed for the average joe. Gridwalk makes home network pentesting and auditing straightforward, safe, and highly effective.

## Features
* **Lightning Fast:** Fully multi-threaded to speed up scan times.
* **Comprehensive Scanning:** Capable of scanning all 65,535 ports.
* **Smart Subnet Detection:** Automatically identifies and maps your local subnet.
* **Safe & Smart:** Built-in security guardrails and privilege awareness to prevent accidental disruptions.
* **Highly Customizable:** Flexible command-line flags to tailor your scans exactly how you need them.

## Installation
You can run Gridwalk directly from the source code, or make it executable to run globally from anywhere on your machine.

**Option 1: Run directly**

```
git clone https://github.com/mentalEdge984/Gridwalk.git
cd Gridwalk
python3 gridwalk.py
```

**Option 2: Make it globally executable**
```
chmod +x gridwalk.py
sudo cp gridwalk.py /usr/local/bin/gridwalk
```

## Usage
Gridwalk is driven by flexible command-line flags.

**Basic Default Scan (Top 1000 ports):**

```
gridwalk -t [target IP]
```

**Full Port Scan**

```
gridwalk -t [target IP] -p all
```

**Subnet Scan**

```
gridwalk -s [subnet]
```

## Running on Windows
Gridwalk is fully cross-platform, but Windows requires a quick setup first since it doesn't come with Python pre-installed.

**1. Prerequisites**
* Download and install Python from [python.org](https://www.python.org/downloads/). 
* **Crucial:** During the installation, make sure to check the box at the bottom that says **"Add Python to PATH"**.

**2. Usage**
Open Command Prompt or PowerShell, navigate to the folder where you downloaded Gridwalk, and run the script by calling `python` first:

```
python gridwalk.py [target IP]
```

**3. Troubleshooting**
* **Permissions:** For the best results and to avoid OS-level socket errors, right-click Command Prompt and select **"Run as Administrator"**.
* **Firewalls:** Because Gridwalk scans rapidly, Windows Defender or your firewall might flag or block the outbound connections. You may need to temporarily allow the script through your firewall for the scan to complete accurately.

## Disclaimer
*This tool is intended for educational purposes and authorized network auditing only. Do not use Gridwalk on networks or devices you do not own or have explicit permission to test.*
