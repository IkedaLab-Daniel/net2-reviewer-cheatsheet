## ⚙️ CCNA Module 6 Cheatsheet: **EtherChannel and Redundancy**

---

### 🧠 1. Purpose of EtherChannel

* **EtherChannel** combines **multiple physical links** into **one logical link**.
* Provides:

  * **Higher bandwidth** (load-balancing)
  * **Link redundancy**
  * **Simplified management** (one logical interface)
* Seen as a **single interface** by STP and routing protocols.

---

### 🧩 2. Benefits

✅ Increased bandwidth (e.g., 4 × 1 Gbps = 4 Gbps total)
✅ Link redundancy – if one link fails, traffic continues on others
✅ STP treats EtherChannel as **one port**, preventing blocking of individual links
✅ Easier config and troubleshooting

---

### ⚙️ 3. EtherChannel Technologies

| Mode                                         | Description                                         | Protocol      |
| -------------------------------------------- | --------------------------------------------------- | ------------- |
| **PAgP (Port Aggregation Protocol)**         | Cisco proprietary, automatically negotiates channel | Cisco only    |
| **LACP (Link Aggregation Control Protocol)** | IEEE 802.3ad standard, multi-vendor compatible      | Open standard |
| **Static (Manual)**                          | Manually configures aggregation without negotiation | None          |

---

### 🗳️ 4. EtherChannel Modes

| Protocol   | Active Modes | Passive Modes | Notes                               |
| ---------- | ------------ | ------------- | ----------------------------------- |
| **PAgP**   | desirable    | auto          | Both must agree to form a channel   |
| **LACP**   | active       | passive       | Both must agree; active talks first |
| **Static** | on           | on            | No negotiation, manually forced     |

> ⚠️ Mismatch (e.g., one side LACP, other static) = no channel formed.

---

### 🔢 5. Common EtherChannel Requirements

* Same **speed & duplex** on all links
* Same **VLAN membership** (trunk/access consistency)
* Same **switch port mode** (all trunk or all access)
* **No dynamic negotiation mismatch**
* **Max 8 physical links** per EtherChannel

---

### 📦 6. Load Balancing

* Switch uses **hashing algorithms** to distribute traffic.
* Common methods:

  * Source MAC / Destination MAC
  * Source IP / Destination IP
  * Source–Destination pairs combined

**Command Example:**

```
switch(config)# port-channel load-balance src-dst-mac
```

---

### 🧱 7. Interface Configuration Example

**Static EtherChannel:**

```
Switch(config)# interface range g0/1 - 2
Switch(config-if-range)# channel-group 1 mode on
Switch(config)# interface port-channel 1
Switch(config-if)# switchport mode trunk
```

**LACP:**

```
Switch(config)# interface range g0/1 - 2
Switch(config-if-range)# channel-group 1 mode active
```

**PAgP:**

```
Switch(config)# interface range g0/1 - 2
Switch(config-if-range)# channel-group 1 mode desirable
```

---

### 🧭 8. Verification Commands

| Command                                       | Description                           |
| --------------------------------------------- | ------------------------------------- |
| `show etherchannel summary`                   | Displays EtherChannel status          |
| `show interfaces port-channel`                | Shows details about logical interface |
| `show running-config interface port-channel1` | Displays config                       |
| `show spanning-tree interface port-channel1`  | Checks STP role                       |

> **Flags in summary output**:
> `P` = in port-channel, `S` = layer2, `R` = in use, `U` = up

---

### 🧩 9. EtherChannel and STP

* STP views EtherChannel as **a single logical link**.
* Prevents **individual link blocking** — only blocks if the **entire bundle fails**.
* **Faster convergence** and **loop prevention** work hand-in-hand.

---

### ⚡ 10. Redundancy Concepts

| Feature               | Description                                         |
| --------------------- | --------------------------------------------------- |
| **Link Redundancy**   | Uses multiple links to prevent single link failure. |
| **Device Redundancy** | Backup switch/router if primary fails.              |
| **Path Redundancy**   | Multiple paths between devices for fault tolerance. |

---

### 🔁 11. Redundancy in Switching

* **STP** + **EtherChannel** = Prevents loops while keeping backups ready.
* **PortFast + BPDU Guard** → Protect end devices.
* **Rapid STP (RSTP)** → Speeds up reconvergence after a failure.

---

### 🧮 12. EtherChannel Troubleshooting Tips

| Issue                  | Cause                       | Fix                               |
| ---------------------- | --------------------------- | --------------------------------- |
| Ports not bundling     | Mode mismatch               | Use same protocol (LACP↔LACP)     |
| Err-disabled port      | Config mismatch             | Remove and re-add to group        |
| VLAN mismatch          | Access/Trunk mismatch       | Ensure same mode on both ends     |
| STP blocking all ports | Wrong load-balance / mis-ID | Check `show etherchannel summary` |

---

### 💡 13. Exam Key Takeaways

* **EtherChannel = Logical aggregation** of multiple physical links.
* **PAgP** = Cisco only; **LACP** = IEEE standard.
* **Active–Passive (LACP)** or **Desirable–Auto (PAgP)** combos form channels.
* **STP sees EtherChannel as one link**.
* Verify using `show etherchannel summary`.
* Keep **same settings** on all bundled ports.