#!/usr/bin/env python3
import socket
import concurrent.futures
import argparse
import sys
import os

# --- 1. THE MENU ---
parser = argparse.ArgumentParser(description="A lightning-fast, multi-threaded port scanner.")
# Notice we removed required=True from the line below!
parser.add_argument("-s", "--subnet", help="Specify the subnet (e.g., -s 16 - No need for the '/' symbol.")
parser.add_argument("-t", "--target", help="The base subnet (e.g., 192.168.5.)")
parser.add_argument("-w", "--workers", type=int, default=100, help="Number of concurrent workers (default: 100)")
parser.add_argument("-p", "--ports", default="1000", help="Number of ports (1-65535) or 'all'")
parser.add_argument("-to", "--timeout", type=float, default=0.1, help="Timeout in seconds per port (default: 0.1)")

args = parser.parse_args()

# --- 2. FALLBACK LOGIC ---
if args.target:
    base_network = args.target
else:
    base_network = input("Enter the base subnet (e.g., 192.168.5.): ")

# --- 3. THE WORKER INSTRUCTIONS ---
def scan_port(target_ip, port):
    s = socket.socket()
    s.settimeout(args.timeout)
    try:
        s.connect((target_ip, port))
        print(f"Success! {target_ip} has Port {port} OPEN.")
    except:
        pass
    s.close()

# --- 4. THE MAIN SCRIPT ---
ips_to_scan = []

# Port logic (All vs Number)
if args.ports.lower() == "all":
    max_ports = 65535
else:
    max_ports = int(args.ports)

# Determine the subnet number first so we can check it
# Default to 24 if they didn't specify a specific subnet number
subnet_num = int(args.subnet) if args.subnet else 24

# --- THE SANITY CHECK (The Guardrail) ---
if max_ports == 65535 and subnet_num < 24:
    # 1. Check if the user is Root
    if os.geteuid() != 0:
        print("\n[!] ELEVATION REQUIRED: This massive scan requires Root privileges to manage resources.")
        print("[!] Please run: sudo netripper " + " ".join(sys.argv[1:]))
        sys.exit()

    # 2. If they ARE root, give the final warning
    print("\n[!] WARNING: SUPERUSER MASSIVE SCAN DETECTED (Subnet: /" + str(subnet_num) + ")")
    print("[!] This will push your network card and CPU to the absolute limit.")
    
    confirm = input("[?] Confirm high-risk operation? (y/n): ").lower()
    
    if confirm != 'y':
        print("[!] Scan aborted. Stay cool!")
        sys.exit()
    else:
        print("[+] Root authorized. Starting the burn...")
# SMART DETECTION + FLAG SUPPORT
if base_network.endswith('.') or args.subnet:
    print("-" * 50)
    print(f"Scanning Subnet: {base_network.rstrip('.')}.0/{subnet_num} for {max_ports} ports...")
    print("-" * 50)
    
    # Ensure the base ends in a dot for the loop
    clean_base = base_network if base_network.endswith('.') else f"{base_network}."
    for host in range(1, 255):
        ips_to_scan.append(f"{clean_base}{host}")
else:
    print("-" * 50)
    print(f"Scanning Single Target: {base_network} for {max_ports} ports...")
    print("-" * 50)
    ips_to_scan.append(base_network)

# Execution logic
ports_to_check = range(1, max_ports + 1)

try:
    with concurrent.futures.ThreadPoolExecutor(max_workers=args.workers) as executor:
        for target_ip in ips_to_scan:
            for port in ports_to_check:
                executor.submit(scan_port, target_ip, port)
except KeyboardInterrupt:
    print("\n[!] Scan stopped. Cleaning up and exiting...")
    sys.exit()
