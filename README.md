# NetRipper

A fast, multi-threaded Python network scanner designed for the average joe. NetRipper makes home network pentesting and auditing straightforward, safe, and highly effective.

## Features
* **Lightning Fast:** Fully multi-threaded to speed up scan times.
* **Comprehensive Scanning:** Capable of scanning all 65,535 ports.
* **Smart Subnet Detection:** Automatically identifies and maps your local subnet.
* **Safe & Smart:** Built-in security guardrails and privilege awareness to prevent accidental disruptions.
* **Highly Customizable:** Flexible command-line flags to tailor your scans exactly how you need them.

## Installation
You can run NetRipper directly from the source code, or make it executable to run globally from anywhere on your machine.

**Option 1: Run directly**
```
git clone https://github.com/YourUsername/NetRipper.git
cd NetRipper
python3 netripper.py
```

**Option 2: Make it globally executable**
```
chmod +x netripper.py
sudo cp netripper.py /usr/local/bin/netripper
```

## Usage
NetRipper is driven by flexible command-line flags. 

**Basic Scan (Top 1000 ports):**
```
netripper [target-ip]
```

**Full Port Scan:**
```
netripper -t [target ip] -p all
```

**Subnet Scan:**
```
netripper -s [subnet]
```

## Disclaimer
*This tool is intended for educational purposes and authorized network auditing only. Do not use NetRipper on networks or devices you do not own or have explicit permission to test.*
