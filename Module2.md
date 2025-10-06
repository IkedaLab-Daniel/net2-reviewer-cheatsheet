## ⚙️ **CCNA 2 – Module 2 Cheatsheet: Switching Concepts**

---

### 🧠 **1. Core Concepts to Memorize**

| Concept                           | Description                                                           |
| --------------------------------- | --------------------------------------------------------------------- |
| **Switch**                        | A Layer 2 device that forwards frames based on **MAC addresses**.     |
| **MAC Address Table (CAM Table)** | Table of known MAC addresses and their associated ports.              |
| **Switching Logic**               | 1️⃣ Learn → 2️⃣ Forward/Filter → 3️⃣ Flood (if unknown).              |
| **Unicast Frame**                 | Sent from one source to one destination.                              |
| **Broadcast Frame**               | Sent to all devices in the same VLAN (MAC = FF:FF:FF:FF:FF:FF).       |
| **Multicast Frame**               | Sent to multiple specific devices (uses special MAC prefix 01:00:5E). |

---

### 🔍 **2. Switch Forwarding Process**

| Step            | Description                                                       |
| --------------- | ----------------------------------------------------------------- |
| **Learning**    | Switch records source MAC address + incoming port.                |
| **Forwarding**  | Frame sent to the port associated with destination MAC.           |
| **Flooding**    | If MAC unknown → switch sends frame to all ports (except source). |
| **Aging Timer** | MAC table entries expire after **300 seconds** (default).         |

---

### 🧩 **3. Forwarding Methods**

| Method                | Description                                      | Notes                               |
| --------------------- | ------------------------------------------------ | ----------------------------------- |
| **Store-and-Forward** | Receives entire frame → verifies CRC → forwards. | Most common; error checking.        |
| **Cut-Through**       | Starts forwarding once destination MAC read.     | Faster but no error checking.       |
| **Fragment-Free**     | Forwards after first 64 bytes (min frame size).  | Balance between speed and accuracy. |

---

### 🌐 **4. Collision and Broadcast Domains**

| Concept              | Description                                                                          |
| -------------------- | ------------------------------------------------------------------------------------ |
| **Collision Domain** | Area where data packets can collide. <br> Each **switch port** = 1 collision domain. |
| **Broadcast Domain** | Area where broadcast frames are propagated. <br> Each **VLAN** = 1 broadcast domain. |
| **Router**           | Breaks up broadcast domains.                                                         |
| **Switch**           | Breaks up collision domains.                                                         |

---

### 🧱 **5. Duplex and Speed**

| Setting               | Meaning                                                            |
| --------------------- | ------------------------------------------------------------------ |
| **Half Duplex**       | Data can flow in one direction at a time. (Shared media like hubs) |
| **Full Duplex**       | Data can flow in both directions simultaneously. (Modern switches) |
| **Auto-Negotiation**  | Automatically selects best duplex/speed combination.               |
| **Mismatched Duplex** | Causes collisions, slow performance.                               |

---

### 📡 **6. Switch Port Modes**

| Mode                         | Description                                             |
| ---------------------------- | ------------------------------------------------------- |
| **Access Port**              | Belongs to only one VLAN; used by end devices.          |
| **Trunk Port**               | Carries multiple VLANs using **802.1Q tagging**.        |
| **Dynamic Auto / Desirable** | Automatically negotiates trunk (depends on both sides). |

---

### 🔐 **7. Port Security (Intro Concept)**

| Concept              | Description                                                                                                |
| -------------------- | ---------------------------------------------------------------------------------------------------------- |
| **Port Security**    | Limits which devices can connect to a port (based on MAC).                                                 |
| **Sticky MAC**       | Automatically learns and saves MAC to running-config.                                                      |
| **Violation Modes:** | 1️⃣ **Protect** (drops frames) <br> 2️⃣ **Restrict** (drops + logs) <br> 3️⃣ **Shutdown** (disables port). |
| **Enable Example:**  |                                                                                                            |

```bash
interface fa0/1
switchport mode access
switchport port-security
switchport port-security maximum 2
switchport port-security violation shutdown
switchport port-security mac-address sticky
```

---

### 🧾 **8. Important Show Commands**

| Command                               | Purpose                               |
| ------------------------------------- | ------------------------------------- |
| `show mac address-table`              | Displays learned MACs and ports.      |
| `show interfaces status`              | Displays interface status and VLANs.  |
| `show interfaces fa0/1`               | Detailed stats for one port.          |
| `show running-config interface fa0/1` | View port security & VLAN assignment. |
| `show port-security interface fa0/1`  | Displays violation count & mode.      |

---

### ⚠️ **9. Common Issues**

| Problem                           | Likely Cause                                       |
| --------------------------------- | -------------------------------------------------- |
| **No connectivity between VLANs** | VLAN misconfiguration (different VLANs).           |
| **MAC flooding**                  | Attack filling MAC table to cause broadcast storm. |
| **Slow performance**              | Duplex mismatch or CRC errors.                     |
| **Broadcast storm**               | Redundant links without STP.                       |

---

### 📚 **10. Key Terminology**

| Term               | Meaning                                             |
| ------------------ | --------------------------------------------------- |
| **CAM Table**      | Content Addressable Memory storing MACs.            |
| **CRC**            | Cyclic Redundancy Check — verifies frame integrity. |
| **Latency**        | Time delay in frame forwarding.                     |
| **Bandwidth**      | Maximum data transfer rate.                         |
| **Frame Flooding** | Sending unknown destination frames to all ports.    |
| **Aging**          | Removal of old MAC entries after timer expires.     |

---

### 🧩 **11. Real Exam Trigger Phrases**

| Question Clue                                              | What It Means               |
| ---------------------------------------------------------- | --------------------------- |
| “**Switch receives a frame with unknown destination MAC**” | Flooding occurs.            |
| “**Which device separates broadcast domains?**”            | Router (or Layer 3 switch). |
| “**Each port on a switch is its own…**”                    | Collision domain.           |
| “**Switch forwards frame immediately after reading MAC**”  | Cut-through method.         |
| “**Which forwarding method checks CRC?**”                  | Store-and-forward.          |

---

### ⚡ **12. Quick Command Recap**

| Action             | Command                      |
| ------------------ | ---------------------------- |
| View MAC table     | `show mac address-table`     |
| Clear MAC table    | `clear mac address-table`    |
| View port details  | `show interfaces fa0/1`      |
| View switch uptime | `show version`               |
| View port VLAN     | `show interfaces switchport` |