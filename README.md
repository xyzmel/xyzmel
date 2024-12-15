# 🖥️ Home Lab Network Setup

![homelab drawio](https://github.com/user-attachments/assets/c4037cf7-ca96-4c7f-be62-3ac43b9f0053)

---

## 🌐 Network Notes

### 1. **Network Summary**
- **Network Address**: `192.168.0.0/24`
- **Subnet Mask**: `255.255.255.0`
- **Default Gateway**: `192.168.0.1`
- **Primary DNS**: `192.168.0.109` (*DC01 - DNS Server*)

---

### 2. **IP Address Allocation**
| Device                  | IP Address       | Notes                           |
|-------------------------|------------------|---------------------------------|
| **Router**              | `192.168.0.1`    | Default gateway                 |
| **Personal Computer**              | `192.168.0.104`    | Computer outside Domain                |
| **Hyper-V Host**        | `192.168.0.105`  | Hyper-V host                    |
| **DC01 (Windows Server 2025)** | `192.168.0.109`  | Domain Controller, DNS, DHCP   |
| **VM01 (Windows 11)**   | `192.168.0.122`  | DHCP (Client for AD testing)    |
| **UBUNTU01 (Ubuntu 22.04)** | `192.168.0.123`  | Static (Plex/Ansible Server)    |

---

### 3. **Hyper-V Switch Configuration**
- **External Virtual Switch**:
  - Used by **DC01** for external network connectivity.
  - Allows **DC01** to act as the gateway for other VMs to access the internet.
  
- **Internal Virtual Switch**:
  - Used for internal traffic between VMs (e.g., **VM01** ↔ **UBUNTU01** ↔ **DC01**).
  - VMs use **DC01** as the gateway to reach the internet.

---

### 4. **DHCP Server Configuration (DC01)**
- **DHCP Role**: Installed on **DC01**
- **Scope Range**: `192.168.0.120 - 192.168.0.150`
- **Default Gateway (For VMs)**: `192.168.0.109` (*DC01*)
- **DNS Server**: `192.168.0.109`

---

### 5. **Routing and Internet Access**
- **VM Internet Access**:
  - All other VMs (e.g., **VM01**, **UBUNTU01**) route traffic through **DC01** (`192.168.0.109`).
  - **DC01** acts as the default gateway for these VMs.

---

### 6. **Roles and Responsibilities**
| **Device**       | **Roles**                                           |
|------------------|-----------------------------------------------------|
| **DC01**         | - Domain Controller (Active Directory)              |
|                  | - DNS Server                                        |
|                  | - DHCP Server                                       |
|                  | - Default Gateway for Hyper-V VMs                   |
| **VM01**         | - Client machine for AD logins and GPO testing      |
| **UBUNTU01**     | - Plex Media Server                                 |
|                  | - Ansible Server                                    |

---

### 7. **Purpose of the Lab**
This lab simulates a small-scale network environment to test and validate:
- ✅ **Active Directory** and **Group Policy Objects (GPOs)**.
- ✅ **DNS and DHCP** server configurations.
- ✅ **Internal and external virtual network communication**.
- ✅ Routing traffic through a **Domain Controller**.
- ✅ Ubuntu-based **media/file server** functionality.

---

### 🎯 Key Goals
- Gain hands-on experience with **Windows Server roles**.
- Configure and manage **virtual switches** in **Hyper-V**.
- Implement **DHCP** for dynamic IP assignment.
- Set up a **media server** and test real-world use cases.
