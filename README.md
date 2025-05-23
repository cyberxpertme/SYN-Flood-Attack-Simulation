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


3. Set static IP addresses on each VM manually:

---

### Set Static IP on Attacker (Kali):

Open terminal on attacker and run:

```bash
sudo ip addr flush dev eth0
sudo ip addr add 192.168.56.10/24 dev eth0
sudo ip link set dev eth0 up
```
Set Static IP on Victim (Kali):
Open terminal on victim and run:
```bash
sudo ip addr flush dev eth0
sudo ip addr add 192.168.56.11/24 dev eth0
sudo ip link set dev eth0 up
```
Verify Connectivity
From attacker, ping victim:
```bash
ping 10.0.2.15
```
![1](https://github.com/user-attachments/assets/fafe039b-40dc-4e2c-a585-b5ba62c63eb1)

