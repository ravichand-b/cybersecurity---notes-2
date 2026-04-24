# 🛡️ Day 1 — Network Reconnaissance Using Nmap
**Date:** 23 April 2026  
**Platform:** Real Network (Home Lab Practice)  
**Tools Used:** Kali Linux, Nmap 7.99  
**Type:** Network Enumeration / Host Discovery  

---

## 🎯 Objective
Perform a full network reconnaissance on a local /24 subnet to:
- Discover all live hosts
- Identify device types (phones, laptops, routers)
- Detect operating systems
- Find open ports and running services

---

## 🖥️ My Setup
- **Attacker Machine:** Kali Linux (VirtualBox)
- **My IP:** 192.168.1.27
- **Network Range:** 192.168.1.0/24
- **My MAC:** 08:00:27:8a:35:d2

---

## 📋 Step 1 — Find My Own IP
First I checked my own IP address using:
```bash
ip a
```
**Result:**
- My IP = `192.168.1.27/24`
- Network range = `192.168.1.0` to `192.168.1.255`
- `/24` means 256 possible addresses on this network

---

## 🔍 Step 2 — Ping Scan (Find All Live Hosts)
```bash
nmap -sn 192.168.1.0/24
```
**Result — 8 live hosts found:**

| IP Address | MAC Address | Vendor |
|------------|-------------|--------|
| 192.168.1.1 | 44:95:3B:CC:80:80 | RLTech India Private Limited |
| 192.168.1.5 | 16:50:C3:A7:20:B1 | Unknown (Random MAC) |
| 192.168.1.11 | 2E:94:5E:EB:75:8C | Unknown (Random MAC) |
| 192.168.1.20 | BA:10:0F:09:98:C7 | Unknown (Random MAC) |
| 192.168.1.24 | C2:FB:75:B7:BE:82 | Unknown (Random MAC) |
| 192.168.1.26 | 94:BB:43:C7:A5:C9 | AzureWave Technology |
| 192.168.1.42 | 20:23:51:A5:AF:29 | TP-Link Systems |
| 192.168.1.27 | — | My Kali Machine |

**Key observation:**
- `RLTech India` = Indian WiFi router brand = this is the **network router**
- `AzureWave` = laptop WiFi chip manufacturer = **laptop**
- `TP-Link` = networking device = **range extender or adapter**
- `Unknown MACs` = modern phones use **random MAC** for privacy

---

## 🔬 Step 3 — Service Version Detection
```bash
nmap -sV 192.168.1.0/24
```
**Interesting findings:**

### 192.168.1.1 — Router
```
Port 53/tcp  open  domain  dnsmasq 2.78
Port 80/tcp  open  http    Boa HTTPd 0.94.13
MAC: RLTech India Private Limited
```
- Port 53 = DNS service running
- Port 80 = Web admin panel accessible at http://192.168.1.1
- Running **Boa HTTP server** — lightweight web server used in routers

### 192.168.1.24 — Suspicious Device
```
Port 49152/tcp open  tcpwrapped
Port 62078/tcp open  tcpwrapped
```
- Port 62078 = Apple iPhone sync port → **iPhone detected!**

### 192.168.1.26 — Developer Laptop
```
Port 3306/tcp open  mysql  MySQL (unauthorized)
MAC: AzureWave Technology
```
- Port 3306 = MySQL database running
- Someone has a **database server** running on their laptop!

### 192.168.1.17 — Windows Machine
```
Port 135/tcp open  msrpc        Microsoft Windows RPC
Port 139/tcp open  netbios-ssn  Microsoft Windows NetBIOS
Port 445/tcp open  microsoft-ds Windows SMB
Port 7070/tcp open  ssl/realserver
Port 9999/tcp open  abyss — TallyPrime Accounting Software!
```
- Ports 135 + 139 + 445 = **100% Windows machine**
- Port 9999 running **TallyPrime** = business accounting software
- MAC = `70:A6:CC:35:CE:15` = Intel Corporate = Intel WiFi chip = laptop confirmed

---

## 🖥️ Step 4 — OS Detection
```bash
nmap -O 192.168.1.0/24
```
**Results:**

| IP | OS Detected | Confidence |
|----|-------------|------------|
| 192.168.1.1 | Linux 3.2 - 4.14 (Embedded) | High |
| 192.168.1.24 | Apple iOS 16 / macOS 11-13 | High — iPhone confirmed! |
| 192.168.1.26 | Microsoft Windows 11/10 | 92% |
| 192.168.1.17 | Microsoft Windows | Confirmed via CPE |
| 192.168.1.27 | — | 0 hops = my own machine |

---

## 🗺️ Step 5 — Final Network Map

```
192.168.1.0/24 — Hostel WiFi Network
│
├── 192.168.1.1   🔴 Router      — RLTech, Linux Embedded, Port 53+80
├── 192.168.1.5   📱 Phone       — Random MAC, all ports closed
├── 192.168.1.7   📱 Phone       — Random MAC, all ports closed  
├── 192.168.1.8   📱 Phone       — Random MAC, all ports closed
├── 192.168.1.13  📱 Phone       — Random MAC, all ports closed
├── 192.168.1.17  💻 Windows PC  — Intel WiFi, TallyPrime port 9999, SMB
├── 192.168.1.20  📱 Phone       — Random MAC
├── 192.168.1.24  🍎 iPhone      — iOS 16, port 62078 confirmed Apple
├── 192.168.1.26  💻 Windows PC  — AzureWave, MySQL port 3306
├── 192.168.1.29  📱 Phone       — Random MAC
├── 192.168.1.42  📶 TP-Link     — TP-Link Systems, all ports filtered
└── 192.168.1.27  ✅ My Kali     — 0 hops, attacker machine
```

---

## 🔑 Key Findings Summary

| Finding | Details | Risk Level |
|---------|---------|------------|
| Router admin page exposed | http://192.168.1.1 open, no HTTPS | 🟡 Medium |
| MySQL database exposed | Port 3306 open on 192.168.1.26 | 🔴 High |
| TallyPrime server running | Port 9999 on 192.168.1.17 | 🟡 Medium |
| SMB ports open | Ports 135/139/445 on Windows machine | 🔴 High |
| iPhone identified | iOS 16 on 192.168.1.24 | 🟢 Info only |
| Phones using random MAC | 6+ devices with privacy MAC | 🟢 Info only |

---

## 📚 What I Learned

1. **`/24` subnet** means 256 IP addresses (0-255) on same network
2. **MAC address OUI lookup** reveals device manufacturer
3. **Random MAC addresses** are used by modern phones for privacy
4. **Port 62078** = Apple iPhone specific port
5. **Ports 135/139/445** = Windows machine signature
6. **1 hop** = network distance — all devices on local WiFi are 1 hop away
7. **Embedded Linux** = lightweight Linux running inside routers
8. **OS detection percentage** = Nmap confidence level based on packet response matching
9. **Local network** is always traceable via MAC + DHCP logs — Tor/VPN cannot hide you
10. **Port 80 on router** = admin web panel accessible via browser

---

## 🛠️ Commands Used

```bash
# Check my own IP
ip a

# Discover all live hosts
nmap -sn 192.168.1.0/24

# Detect services and versions
nmap -sV 192.168.1.0/24

# OS detection
nmap -O 192.168.1.0/24

# Aggressive scan on specific target
nmap -A 192.168.1.17
```

---

## ⚠️ Disclaimer
This scan was performed on a network I am connected to for **educational purposes only.**  
No systems were accessed, exploited or modified.  
All findings are documented purely for learning network reconnaissance techniques.

---

*Written by: [Your Name]*  
*GitHub: github.com/[yourusername]*  
*Learning Path: Cybersecurity — 15 Day Challenge*
