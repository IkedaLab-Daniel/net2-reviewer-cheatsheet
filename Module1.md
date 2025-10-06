## ⚡ CCNA 2 – Module 1 Cheatsheet: *Basic Device Configuration*

---

### 🧠 **1. Core Concepts to Remember**

| Concept                                 | Description                                                         |
| --------------------------------------- | ------------------------------------------------------------------- |
| **Switch Boot Sequence**                | 1️⃣ POST → 2️⃣ Boot loader → 3️⃣ Load IOS → 4️⃣ Load startup-config |
| **POST (Power-On Self Test)**           | Hardware diagnostic run by the switch on boot.                      |
| **Boot Loader**                         | Small program that loads the Cisco IOS into RAM.                    |
| **IOS (Internetwork Operating System)** | The OS that controls switch/router operation.                       |
| **Startup-config**                      | Saved configuration stored in NVRAM.                                |
| **Running-config**                      | Active configuration stored in RAM.                                 |
| **VLAN 1**                              | Default management VLAN on Cisco switches.                          |

---

### 🔐 **2. Security and Access**

| Feature                 | Command / Note                                                                                      |
| ----------------------- | --------------------------------------------------------------------------------------------------- |
| **Console Access**      | `line console 0` → `password [pass]` → `login`                                                      |
| **VTY (Remote) Access** | `line vty 0 4` → `password [pass]` → `login`                                                        |
| **Enable Secret**       | `enable secret [pass]` → encrypted privileged password                                              |
| **Banner MOTD**         | `banner motd # Unauthorized Access Prohibited #`                                                    |
| **Password Encryption** | `service password-encryption`                                                                       |
| **SSH (Secure Shell)**  | Used instead of Telnet for secure remote access.                                                    |
| **SSH Config Steps**    | `ip domain-name`, `crypto key generate rsa`, `username [user] secret [pass]`, `transport input ssh` |

---

### 🌐 **3. Switch Management Interface**

| Concept             | Description / Command                                                          |
| ------------------- | ------------------------------------------------------------------------------ |
| **Management IP**   | Assigns an IP to the switch for remote management via VLAN 1.                  |
| **Command:**        | `interface vlan 1 ip address 192.168.1.2 255.255.255.0 no shutdown`            |
| **Default Gateway** | Required for managing switch across networks: `ip default-gateway 192.168.1.1` |
| **Verify IP**       | `show ip interface brief`                                                      |

---

### ⚙️ **4. Configuration Commands**

| Action              | Command                              |
| ------------------- | ------------------------------------ |
| View running config | `show running-config`                |
| Save config         | `copy running-config startup-config` |
| View version info   | `show version`                       |
| View MAC address    | `show mac address-table`             |
| Clear MAC table     | `clear mac address-table`            |
| Reboot device       | `reload`                             |
| Delete config       | `erase startup-config`               |

---

### 🧩 **5. Device Modes**

| Mode                 | Prompt                 | Purpose                                      |
| -------------------- | ---------------------- | -------------------------------------------- |
| **User EXEC**        | `Switch>`              | Limited access; basic monitoring only.       |
| **Privileged EXEC**  | `Switch#`              | Access to all show commands & debugging.     |
| **Global Config**    | `Switch(config)#`      | Configure system-wide settings.              |
| **Interface Config** | `Switch(config-if)#`   | Configure a specific port or VLAN interface. |
| **Line Config**      | `Switch(config-line)#` | Configure console, vty, or aux lines.        |

---

### ⚡ **6. Key Files and Memory Locations**

| Memory    | Description                                       |
| --------- | ------------------------------------------------- |
| **NVRAM** | Stores `startup-config`.                          |
| **RAM**   | Holds `running-config` and IOS in use.            |
| **Flash** | Stores IOS image and other files.                 |
| **ROM**   | Contains boot loader & basic diagnostic software. |

---

### 📶 **7. Useful Verification Commands**

| Command                   | Use                                          |
| ------------------------- | -------------------------------------------- |
| `show ip interface brief` | Displays interface status & IPs.             |
| `show interfaces status`  | Displays port mode (access/trunk) and VLANs. |
| `show history`            | Shows previously entered commands.           |
| `show users`              | Displays who’s logged in.                    |
| `show version`            | Shows IOS version, uptime, hardware details. |
| `ping` / `traceroute`     | Tests network connectivity.                  |

---

### 💡 **8. Common Troubleshooting Tips**

| Problem                      | Check                                            |
| ---------------------------- | ------------------------------------------------ |
| **Can’t ping switch**        | Verify VLAN 1 IP and default gateway.            |
| **SSH not working**          | Check RSA key, domain name, and vty settings.    |
| **Config lost after reboot** | Save it! → `copy running-config startup-config`. |
| **Interface down**           | Run `no shutdown` under the interface.           |

---

### ⚙️ **9. Essential Terminology**

| Term                 | Meaning                                                 |
| -------------------- | ------------------------------------------------------- |
| **MAC Address**      | Unique physical address of a NIC.                       |
| **Port Security**    | Limits devices per switch port to prevent MAC flooding. |
| **Base MAC Address** | Switch’s burned-in MAC used for management.             |
| **Duplex**           | Determines if device can send/receive simultaneously.   |
| **Speed**            | Defines data rate of the interface.                     |

---

### 🧩 **10. Memorize These Shortcuts**

| Shortcut   | Description                    |
| ---------- | ------------------------------ |
| `Ctrl + A` | Move to beginning of line      |
| `Ctrl + E` | Move to end of line            |
| `Ctrl + Z` | Return to privileged EXEC mode |
| `Tab`      | Auto-complete command          |
| `?`        | Context-sensitive help         |

---

### 🚨 **11. Real Exam Triggers (Be Familiar With)**

* “**Switch boots up to ‘Switch:’ prompt**” → Missing or corrupted IOS.
* “**Can’t access switch remotely**” → Management IP or gateway misconfig.
* “**Telnet insecure**” → Use SSH instead.
* “**Banner MOTD**” → Legal warning displayed before login.
* “**erase startup-config**” → Deletes saved config; requires reload.