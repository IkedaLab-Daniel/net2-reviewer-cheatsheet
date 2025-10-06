## 🧭 **CCNA 2 – Module 4 Cheatsheet: Inter-VLAN Routing**

---

### 🧠 **1. Core Concept**

| Concept                | Description                                                                                                             |
| ---------------------- | ----------------------------------------------------------------------------------------------------------------------- |
| **Inter-VLAN Routing** | Allows devices in different VLANs (different subnets) to communicate.                                                   |
| **Why Needed?**        | VLANs isolate broadcast domains — a **Layer 3 device** (router or multilayer switch) is required to route between them. |
| **Each VLAN**          | = Separate IP subnet.                                                                                                   |

---

### ⚙️ **2. Methods of Inter-VLAN Routing**

| Method                                | Description                                                                    | Devices Used      |
| ------------------------------------- | ------------------------------------------------------------------------------ | ----------------- |
| **Legacy Inter-VLAN Routing**         | Each VLAN connected to a **physical router interface**.                        | Router + Switch   |
| **Router-on-a-Stick (ROAS)**          | One router interface with multiple **subinterfaces**, each assigned to a VLAN. | Router (Layer 3)  |
| **Layer 3 Switch Inter-VLAN Routing** | Uses **Switch Virtual Interfaces (SVIs)**.                                     | Multilayer Switch |

---

### 🧩 **3. Legacy Routing (Old Method)**

* Each VLAN connected to **dedicated router port**.
* Example:

  * VLAN 10 → Router Fa0/0
  * VLAN 20 → Router Fa0/1
* ❌ Inefficient, requires multiple cables.

---

### ⚡ **4. Router-on-a-Stick (ROAS)**

**Most common exam configuration**

**Concept:** One physical router interface handles multiple VLANs through *subinterfaces* using 802.1Q encapsulation.

**Configuration Example:**

```bash
interface g0/0
 no shutdown
!
interface g0/0.10
 encapsulation dot1Q 10
 ip address 192.168.10.1 255.255.255.0
!
interface g0/0.20
 encapsulation dot1Q 20
 ip address 192.168.20.1 255.255.255.0
!
interface g0/0.99
 encapsulation dot1Q 99 native
 ip address 192.168.99.1 255.255.255.0
```

**Key Notes:**

* `encapsulation dot1Q [vlan-id]` = Assign VLAN to subinterface.
* Use `native` keyword for native VLAN.
* Default gateway for hosts = router subinterface IP.

---

### 🧮 **5. Layer 3 Switch Routing (SVI)**

**Concept:** The switch performs routing internally (no router needed).

**Configuration Example:**

```bash
ip routing
interface vlan 10
 ip address 192.168.10.1 255.255.255.0
 no shutdown
!
interface vlan 20
 ip address 192.168.20.1 255.255.255.0
 no shutdown
```

**Enable routing:** `ip routing`
**Verify:** `show ip interface brief`

---

### 🧱 **6. VLAN and Subnet Pairing**

| VLAN           | Subnet          | Gateway      |
| -------------- | --------------- | ------------ |
| VLAN 10        | 192.168.10.0/24 | 192.168.10.1 |
| VLAN 20        | 192.168.20.0/24 | 192.168.20.1 |
| VLAN 99 (Mgmt) | 192.168.99.0/24 | 192.168.99.1 |

Each VLAN **must** be in a **unique subnet**.

---

### 🧾 **7. Verification Commands**

| Command                   | Description                               |
| ------------------------- | ----------------------------------------- |
| `show ip interface brief` | Lists all interfaces and IP addresses.    |
| `show interfaces trunk`   | Ensures switch port to router is trunked. |
| `show vlan brief`         | Confirms port-to-VLAN assignments.        |
| `show running-config`     | Displays router/switch configuration.     |
| `ping`                    | Test inter-VLAN communication.            |
| `traceroute`              | Tests path to destination VLAN.           |

---

### 🧩 **8. Troubleshooting Tips**

| Symptom                                         | Likely Cause                                        |
| ----------------------------------------------- | --------------------------------------------------- |
| **PCs in different VLANs can’t ping**           | Inter-VLAN routing not enabled or wrong IP gateway. |
| **One VLAN works, another fails**               | Missing subinterface or SVI.                        |
| **No response from router**                     | Switch trunk misconfigured.                         |
| **Subinterface error: “encapsulation not set”** | Missing `encapsulation dot1Q` command.              |
| **Native VLAN mismatch warning**                | Both sides of trunk use different native VLAN IDs.  |

---

### 🔐 **9. Important Notes**

* Each **VLAN → Subnet → Default Gateway** pattern must match.
* Router-on-a-stick link **must be a trunk**.
* Layer 3 switch routing is faster than router-on-a-stick (no external hop).
* **Default gateway** of a PC = IP of VLAN interface (SVI or subinterface).
* If trunk fails, **no inter-VLAN communication** is possible.

---

### 🧠 **10. Exam Triggers**

| Question Clue                                          | Remember This                                   |
| ------------------------------------------------------ | ----------------------------------------------- |
| “**Single interface routes multiple VLANs**”           | Router-on-a-stick.                              |
| “**Switch handles routing without external router**”   | Layer 3 switch (SVI).                           |
| “**Inter-VLAN communication fails despite IP config**” | Trunk misconfiguration or missing `ip routing`. |
| “**Router subinterface missing encapsulation**”        | Add `encapsulation dot1Q [vlan]`.               |
| “**Default gateway not set**”                          | End device cannot reach other VLANs.            |

---

### 🧩 **11. Quick Command Recap**

| Task                       | Command                    |
| -------------------------- | -------------------------- |
| Enable routing (L3 switch) | `ip routing`               |
| Create VLAN interface      | `interface vlan [id]`      |
| Set VLAN IP                | `ip address [IP] [mask]`   |
| Router subinterface        | `interface g0/0.[vlan-id]` |
| Trunk setup (switch side)  | `switchport mode trunk`    |
| View VLANs                 | `show vlan brief`          |
| Verify trunk               | `show interfaces trunk`    |

---

### ⚡ **12. Easy Mnemonics**

* 💡 **“1 link, many VLANs = Router-on-a-Stick.”**
* 🧱 **“Each VLAN = unique subnet.”**
* 🔄 **“Trunk between router & switch = lifeline.”**
* 🔑 **“SVI needs IP + no shutdown + ip routing.”**