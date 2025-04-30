# 🏨 Hotel Network Infrastructure – Cisco Project

## 📘 Overview

This project showcases a comprehensive Cisco-based network infrastructure designed for a multi-story hotel with **4 floors**, integrating **IoT technologies**, **VLAN segmentation**, and **inter-router communication using routing protocols**. The implementation supports both wired and wireless communications, device management, and service isolation through VLANs and proper routing configuration.

---

## 🏗️ Project Structure

### 🏢 Hotel Layout

- **Floor 1 (Reception, Store & Restaurant):**
  - 2 Switches (Switch0 for Reception, Switch1 for Store & Restaurant)
  - Connected to Router0
  - Hosts PCs, printers, and wireless access points

- **Floor 2 (Room 1 & Room 2):**
  - Switch2
  - Connected to Router1

- **Floor 3 (Room 3 & Room 4):**
  - Switch3
  - Connected to Router1

- **Floor 4 (Servers, IT, HR, Admin, Marketing):**
  - Switch4 (Servers)
  - Switch5 (Departments)
  - Connected to Router2

---

## 🌐 Network Devices

### Routers
- **Router0:** Connects to Switch0 and Switch1, uplinks to Router1 and Router2 via Serial interfaces
- **Router1:** Connects to Switch2 and Switch3, uplinks to Router0 and Router2
- **Router2:** Connects to Switch4 and Switch5, uplinks to Router0 and Router1

### Switches and End Devices
- **Switch0 (Reception):** PC0, Printer0, AccessPoint0
- **Switch1 (Store & Restaurant):** PC1, PC2, Printer1, AccessPoint1, AccessPoint2
- **Switch2 (Floor 2 Rooms):** End devices as needed
- **Switch3 (Floor 3 Rooms):** End devices as needed
- **Switch4 (Servers):** Server infrastructure
- **Switch5 (Departments):** PCs and IoT devices for IT, HR, Admin, and Marketing

---

## 🧠 Technologies Used

- **Routing:** Static IP routing between routers using serial connections
- **VLANs:** Isolate traffic (Users, Wireless, Management, Printers)
- **IoT:** Integration of access points and devices for smart room and automation
- **Trunking:** Router-on-a-stick configuration to route between VLANs
- **Management VLANs:** Secure access to switch configuration interfaces

---

## 🔧 VLAN Configuration

Example on Switch0:
- `VLAN 10` – USER (PCs, Printers)
- `VLAN 30` – WIRELESS (Access Points)
- `VLAN 99` – MANAGEMENT (Switch access)

Switch1 includes an additional:
- `VLAN 20` – PRINTER

Each VLAN is routed through Router0 using trunk ports.

---

## ⚙️ IP Addressing Scheme

| Network        | IP Range            | Device Type         |
|----------------|---------------------|---------------------|
| 192.168.60.0/24 | Router0 ↔ Switch0   | VLAN10/VLAN30       |
| 192.168.61.0/24 | Router0 ↔ Switch1   | VLAN10/VLAN20/VLAN30|
| 192.168.62.0/24 | Router1 ↔ Switch2   | User Devices        |
| 192.168.63.0/24 | Router1 ↔ Switch3   | User Devices        |
| 192.168.64.0/24 | Router2 ↔ Switch4   | Servers             |
| 192.168.65.0/24 | Router2 ↔ Switch5   | Office Departments  |
| 192.168.99.0/24 | Management VLAN     | Switches            |
| 192.168.10.0/30 | Serial (Router0 ↔ Router1) |
| 192.168.11.0/30 | Serial (Router0 ↔ Router2) |
| 192.168.12.0/30 | Serial (Router1 ↔ Router2) |

---

## ✅ Routing

- Each router uses **static routing** with specific serial IPs to communicate across the network.
- `ip routing` is enabled on all routers.
- Trunk links are configured to allow VLAN routing via **router-on-a-stick**.

---

## 🔐 Security & Management

- VLAN 99 is used for switch management access
- Default gateways are set for VLAN management interfaces
- IoT devices are segmented from user traffic for improved performance and security

---

## 📌 Author

- [Ilyas El Asri]


---

## 📎 Notes

- Ensure all trunk links have correct allowed VLANs.
- Save configurations after changes using `write memory`.
- Use `ping` to verify inter-VLAN and inter-router connectivity.
