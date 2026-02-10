# PERSONAL-CYBERSECURITY-LAB
Personal cybersecurity lab (Kali + vulnerable web app) using VMware, NAT + Host-Only networks, with evidence screenshots.

This repository documents my isolated cybersecurity lab.
The lab uses VMware Workstation, Kali Linux as the attacker, and OWASP Juice Shop as the vulnerable web application, with NAT + Host-Only networking for isolation.

## 1. Lab Architecture

- Hypervisor: VMware Workstation
- Attacker: Kali Linux
- Target: OWASP Juice Shop (Docker on Kali / Ubuntu)
- Networks:
  - NAT: Internet access for updates
  - Host-Only: Isolated attacker–target traffic


## 2. Kali Linux Attacker VM

Kali VM resources:
- 2 vCPUs
- ~10 GB RAM
- 40 GB virtual disk

Kali is successfully booted and used as the main attacker machine.


### Network adapters in VMware

Kali has two network adapters:
- Adapter 1: NAT – used for internet updates
- Adapter 2: Host-Only – used for lab traffic


### IP configuration inside Kali

The `ip a` output shows:
- `eth0` with a NAT IP (192.168.222.x)
- `eth1` with a Host-Only IP (192.168.56.x)
- Additional Docker bridge interfaces for Juice Shop

ip a

Kali can reach the Docker bridge network:

bash
ping 172.17.0.1

## 3. Vulnerable Target – OWASP Juice Shop
OWASP Juice Shop is running in Docker and exposed on port 3000.
From Kali’s browser I can reach the application using:

http://172.17.0.1:3000/


## 4. Network Discovery and Scanning
From Kali I verified connectivity to the target with Nmap.

Host discovery scan:

bash
nmap -sn 192.168.222.134
The scan reports the host as up.


## 5. Burp Suite Validation
Burp Suite Community Edition is installed on Kali to intercept HTTP traffic.
I created a temporary project and used Burp as an intercepting proxy while browsing.


## 6. Wireshark Traffic Capture
Wireshark is used to capture and analyze HTTP traffic in the lab.
The capture shows TCP packets on port 80 between the client and server, with full headers and payload visible.


## 7. Summary
This lab demonstrates:

Creating and configuring VMs in VMware Workstation

Using NAT and Host-Only networking for an isolated pentest environment

Running a vulnerable web app (OWASP Juice Shop)

Basic validation with ip a, ping, Nmap, Burp Suite, and Wireshark
