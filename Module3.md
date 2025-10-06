## 🧩 **CCNA 2 – Module 3 Cheatsheet: VLANs (Virtual Local Area Networks)**

---

### 🧠 **1. Core Concept**

| Concept                | Description                                                             |
| ---------------------- | ----------------------------------------------------------------------- |
| **VLAN (Virtual LAN)** | Logical segmentation of a Layer 2 network to isolate broadcast domains. |
| **Purpose**            | Improve security, reduce congestion, and simplify network management.   |
| **Default VLAN**       | VLAN 1 — all ports are members until assigned elsewhere.                |
| **Each VLAN**          | Operates as a separate subnet and broadcast domain.                     |

---

### 🗂️ **2. VLAN Types**

| VLAN Type            | Description                                              |
| -------------------- | -------------------------------------------------------- |
| **Default VLAN (1)** | Exists on all switches; cannot be deleted.               |
| **Data VLAN**        | Carries user-generated traffic.                          |
| **Native VLAN**      | Used for untagged traffic on a trunk (default = VLAN 1). |
| **Management VLAN**  | Used for switch management (recommended ≠ VLAN 1).       |
| **Voice VLAN**       | Prioritizes VoIP traffic; QoS applied automatically.     |

---

### ⚙️ **3. VLAN Configuration**

```bash
Switch# configure terminal
Switch(config)# vlan 10
Switch(config-vlan)# name SALES
Switch(config)# interface fa0/1
Switch(config-if)# switchport mode access
Switch(config-if)# switchport access vlan 10
```

* Assign each device port to its VLAN.
* Each VLAN requires a separate IP subnet.

---

### 🌐 **4. VLAN Verification**

| Command                            | Description                              |
| ---------------------------------- | ---------------------------------------- |
| `show vlan brief`                  | Lists all VLANs and port assignments.    |
| `show interfaces fa0/1 switchport` | Displays VLAN mode and membership.       |
| `show interfaces trunk`            | Displays trunk status and allowed VLANs. |
| `show running-config`              | View VLAN configuration.                 |

---

### 🔀 **5. Trunking (802.1Q Encapsulation)**

| Concept                  | Description                                          |
| ------------------------ | ---------------------------------------------------- |
| **Trunk Port**           | Carries traffic for multiple VLANs between switches. |
| **Encapsulation Type**   | 802.1Q (industry standard).                          |
| **Tagging**              | Adds VLAN ID to Ethernet frame header.               |
| **Untagged Frames**      | Belong to the **native VLAN**.                       |
| **Native VLAN Mismatch** | Causes connectivity issues and security alerts.      |

**Configuration Example:**

```bash
interface fa0/24
switchport mode trunk
switchport trunk native vlan 99
switchport trunk allowed vlan 10,20,99
```

---

### 🧩 **6. Dynamic Trunking Protocol (DTP)**

| Mode                  | Description                       | Forms Trunk With               |
| --------------------- | --------------------------------- | ------------------------------ |
| **Access**            | Permanent non-trunk mode          | None                           |
| **Trunk**             | Permanent trunk mode              | Access, Trunk, Desirable, Auto |
| **Dynamic Auto**      | Waits to be invited               | Trunk, Desirable               |
| **Dynamic Desirable** | Actively attempts trunk formation | Trunk, Desirable, Auto         |

---

### 🧱 **7. VLAN Ranges**

| Range              | VLAN IDs  | Description                                             |
| ------------------ | --------- | ------------------------------------------------------- |
| **Normal Range**   | 1–1005    | Stored in VLAN database (vlan.dat)                      |
| **Extended Range** | 1006–4094 | Used in larger networks (requires VTP transparent mode) |
| **Reserved VLANs** | 0, 4095   | Not usable by users                                     |

---

### 🔒 **8. Security and Best Practices**

| Recommendation                                        | Reason                       |
| ----------------------------------------------------- | ---------------------------- |
| Change **native VLAN** to non-default (e.g., VLAN 99) | Prevent VLAN hopping attacks |
| Avoid using **VLAN 1** for user traffic               | Reduces attack surface       |
| Create **dedicated management VLAN**                  | Isolate switch management    |
| Disable unused ports                                  | Prevent unauthorized access  |
| Assign unused ports to an **unused VLAN**             | Adds security layer          |

---

### ⚡ **9. Troubleshooting VLANs**

| Symptom                           | Possible Cause                        |
| --------------------------------- | ------------------------------------- |
| **No connectivity between VLANs** | Inter-VLAN routing not configured.    |
| **Host not in VLAN**              | Access port assigned to wrong VLAN.   |
| **Native VLAN mismatch**          | Trunks use different native VLANs.    |
| **Trunk not forming**             | DTP mismatch or one side access mode. |
| **Ping fails between switches**   | VLANs not allowed on trunk.           |

---

### 🧾 **10. Key Show/Verify Commands**

| Command                            | Purpose                                       |
| ---------------------------------- | --------------------------------------------- |
| `show vlan`                        | Displays VLANs configured and assigned ports. |
| `show interfaces trunk`            | Shows trunk ports, allowed/native VLANs.      |
| `show interfaces switchport`       | Shows VLAN and mode per port.                 |
| `show mac address-table vlan [id]` | Displays MACs in that VLAN.                   |
| `show running-config`              | Check VLAN-related commands.                  |

---

### 🧠 **11. Common Exam Triggers**

| Question Clue                                                | Remember This                                   |
| ------------------------------------------------------------ | ----------------------------------------------- |
| “**Which VLAN carries untagged frames on a trunk?**”         | Native VLAN                                     |
| “**Which VLAN cannot be deleted or renamed?**”               | VLAN 1                                          |
| “**How many broadcast domains on a switch with 4 VLANs?**”   | 4                                               |
| “**Why devices on different VLANs can’t communicate?**”      | Need inter-VLAN routing                         |
| “**What happens when VLAN doesn’t exist on both switches?**” | Traffic dropped on trunk                        |
| “**What is DTP?**”                                           | Cisco protocol that automates trunk negotiation |

---

### 🧩 **12. Quick Memory Aids**

* 🧱 **“VLANs = Virtual Walls”** – They isolate groups in the same switch.
* 🌉 **“Trunks = Bridges between walls”** – Carry all VLANs between switches.
* ⚠️ **“VLAN 1 is default, but don’t use it for management.”**
* 🧾 **“802.1Q adds a 4-byte tag”** – VLAN ID field inside Ethernet frame.
* 🚧 **“Native VLAN untagged!”** – Appears in Wireshark without VLAN tag.