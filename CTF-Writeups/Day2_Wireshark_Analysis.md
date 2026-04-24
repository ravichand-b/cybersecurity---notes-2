# 🦈 Day 2 — Wireshark Network Traffic Analysis
**Date:** 24 April 2026  
**Platform:** Real Network (Home Lab Practice)  
**Tools Used:** Kali Linux, Wireshark  
**Type:** Network Traffic Analysis / Packet Capture  

---

## 🎯 Objective
- Capture live network traffic
- Analyse packets on local network
- Identify protocols being used
- Filter specific traffic types
- Understand how data travels on a network

---

## 🖥️ My Setup
- **Machine:** Kali Linux (VirtualBox)
- **Tool:** Wireshark
- **Network:** 192.168.1.0/24
- **Interface:** eth0

---

## 📋 Step 1 — Open Wireshark
```bash
wireshark
```
Or find it in Kali menu → Network → Wireshark

Select interface **eth0** → Click blue shark fin button to start capture

---

## 🔍 Step 2 — Capture Live Traffic
Once capture starts you will see packets flowing in real time:

| Column | Meaning |
|--------|---------|
| No. | Packet number |
| Time | When packet was captured |
| Source | Who sent the packet |
| Destination | Who received it |
| Protocol | What protocol used (TCP, UDP, HTTP, DNS) |
| Length | Size of packet |
| Info | Summary of what packet contains |

---

## 🎯 Step 3 — Important Display Filters

These filters help you find specific traffic quickly:

| Filter | What it shows |
|--------|--------------|
| `http` | All web traffic |
| `dns` | All DNS lookups |
| `tcp` | All TCP traffic |
| `udp` | All UDP traffic |
| `ip.addr == 192.168.1.1` | Traffic to/from router |
| `ip.src == 192.168.1.27` | Traffic from my machine |
| `tcp.port == 80` | HTTP web traffic only |
| `tcp.port == 443` | HTTPS traffic only |
| `icmp` | Ping traffic |
| `arp` | ARP requests on network |

---

## 📡 Step 4 — Protocols I Found

### DNS Traffic
- Every time a website is opened → DNS request is made
- Shows which websites devices are visiting
- Filter: `dns`
```
Query: Who is google.com?
Response: google.com = 142.250.x.x
```

### ARP Traffic
- ARP = Address Resolution Protocol
- Devices asking "Who has this IP? Tell me your MAC!"
- Filter: `arp`
```
Who has 192.168.1.1? Tell 192.168.1.27
192.168.1.1 is at 44:95:3B:CC:80:80
```

### TCP Traffic
- Most web communication uses TCP
- 3-way handshake: SYN → SYN-ACK → ACK
- Filter: `tcp`

### ICMP Traffic
- Ping packets
- Filter: `icmp`
```bash
ping 192.168.1.1
```
Shows request and reply packets

---

## 🔑 Key Findings

| Finding | Details |
|---------|---------|
| DNS queries visible | Can see which websites devices visit |
| ARP broadcasts | All devices announcing themselves |
| TCP handshakes | Normal web connections visible |
| Router traffic | 192.168.1.1 most active device |

---

## 📚 What I Learned

1. **Wireshark** captures all packets passing through network interface
2. **Display filters** help narrow down specific traffic
3. **DNS** requests reveal which websites are being visited
4. **ARP** protocol maps IP addresses to MAC addresses
5. **TCP 3-way handshake** = SYN, SYN-ACK, ACK
6. **Promiscuous mode** allows capturing all network traffic
7. **Protocols** are rules for how data is sent and received
8. **Packet analysis** is a key skill for SOC analysts

---

## 🛠️ Commands Used
```bash
# Open Wireshark
wireshark

# Capture from terminal (no GUI)
tcpdump -i eth0

# Save capture to file
tcpdump -i eth0 -w capture.pcap

# Read saved capture
tcpdump -r capture.pcap

# Capture only HTTP traffic
tcpdump -i eth0 port 80

# Capture only DNS traffic  
tcpdump -i eth0 port 53
```

---

## ⚠️ Disclaimer
All packet captures were performed on my own network for educational purposes only. No personal data was collected or stored from other devices.

---

*Written by: Ravichand B*  
*GitHub: github.com/ravichand-b/cybersecurity-notes*  
*Learning Path: Cybersecurity — 15 Day Challenge*
