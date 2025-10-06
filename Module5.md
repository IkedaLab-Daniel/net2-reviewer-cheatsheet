## 🧠 CCNA Module 5 Cheatsheet: **Spanning Tree Protocol (STP)**

### 🌳 1. Purpose of STP

* **STP prevents Layer 2 loops** in a switched network.
* **Loops** can cause:

  * Broadcast storms
  * Multiple frame copies
  * MAC address table instability
* STP ensures **one logical path** between switches while **blocking redundant paths**.

---

### ⚙️ 2. Key STP Concepts

| Term                     | Description                                                                      |
| ------------------------ | -------------------------------------------------------------------------------- |
| **Root Bridge**          | The central switch chosen by STP. All other switches calculate best path to it.  |
| **Bridge ID (BID)**      | Used to elect the Root Bridge. BID = Bridge Priority + MAC Address.              |
| **Bridge Priority**      | Default = 32768 (lower is better). You can change it to influence root election. |
| **Root Port (RP)**       | The port with the best path (lowest cost) to the root bridge.                    |
| **Designated Port (DP)** | The port with the lowest path cost on a segment; forwards traffic.               |
| **Blocked Port**         | Port that does not forward frames to prevent loops.                              |

---

### ⚡ 3. STP Port States

1. **Blocking** → No data frames forwarded (listens to BPDUs only).
2. **Listening** → Prepares to participate in STP, discards frames.
3. **Learning** → Learns MAC addresses, doesn’t forward data yet.
4. **Forwarding** → Fully operational, forwards traffic.
5. **Disabled** → Administratively shut down.

---

### 🧩 4. STP Port Roles Summary

| Role                      | Description                               |
| ------------------------- | ----------------------------------------- |
| **Root Port (RP)**        | Best path to root bridge.                 |
| **Designated Port (DP)**  | Best port on each LAN segment.            |
| **Non-Designated Port**   | Placed in blocking to prevent loops.      |
| **Alternate Port** (RSTP) | Backup path to root bridge.               |
| **Backup Port** (RSTP)    | Redundant port on the same segment as DP. |

---

### 🧮 5. STP Path Cost

* **Cost = link speed** (lower is better).
  | Link Speed | Cost |
  |-------------|------|
  | 10 Mbps | 100 |
  | 100 Mbps | 19 |
  | 1 Gbps | 4 |
  | 10 Gbps | 2 |

---

### 🗳️ 6. Root Bridge Election Process

1. Switches exchange **Bridge Protocol Data Units (BPDUs)**.
2. The **lowest Bridge ID** wins.

   * Bridge ID = Priority (2 bytes) + MAC (6 bytes).
3. If priorities are equal, the switch with the **lowest MAC address** becomes the root.

---

### 🛰️ 7. Types of STP

| Type              | Description                                             |
| ----------------- | ------------------------------------------------------- |
| **STP (802.1D)**  | Original version; slow convergence (~30-50s).           |
| **RSTP (802.1w)** | Rapid Spanning Tree Protocol; faster convergence (~6s). |
| **PVST+**         | Cisco’s Per-VLAN STP; runs separate STP per VLAN.       |
| **RSTP PVST+**    | Cisco’s rapid version per VLAN.                         |
| **MSTP (802.1s)** | Multiple STP instances for grouped VLANs.               |

---

### ⚡ 8. BPDU (Bridge Protocol Data Unit)

* Used by switches to share STP information.
* Sent every **2 seconds by default**.
* Two main BPDU types:

  1. **Configuration BPDU** – carries STP info.
  2. **TCN BPDU (Topology Change Notification)** – signals a change in the network.

---

### 🚀 9. Convergence Time (Traditional STP)

* Up to **50 seconds**:

  * Listening (15s)
  * Learning (15s)
  * Forward Delay (15s each phase)
  * * Hello & Max Age timers

RSTP improves this using **handshakes** instead of waiting timers.

---

### 🧱 10. STP Timers (default values)

| Timer             | Description                      | Default |
| ----------------- | -------------------------------- | ------- |
| **Hello Time**    | BPDU send interval               | 2 sec   |
| **Forward Delay** | Time spent in listening/learning | 15 sec  |
| **Max Age**       | Time before BPDU info expires    | 20 sec  |

---

### 🔍 11. Troubleshooting & Commands

* **show spanning-tree** → Displays STP status.
* **spanning-tree vlan [id] root primary** → Forces switch to become root.
* **spanning-tree portfast** → Immediately moves port to forwarding (for end hosts only).
* **spanning-tree bpduguard enable** → Protects from receiving BPDUs on access ports.

---

### 💡 12. Exam Pointers

* Always **lower the bridge priority** to make a switch the root.
* Remember **cost = inverse of link speed**.
* **RSTP** is preferred in modern networks.
* **BPDU Guard + PortFast** are **best friends** on access ports.
* **Blocking ports** prevent loops, not failures.