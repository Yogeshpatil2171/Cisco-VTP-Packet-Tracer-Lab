# 🌐 Cisco Packet Tracer – VTP Network Simulation

Welcome to a practical simulation of **VTP (VLAN Trunking Protocol)** using Cisco Packet Tracer! 🚀  
This setup involves three switches in different VTP modes: `Server`, `Transparent`, and `Client`.

---

## 🧠 What is VTP?

**VTP (VLAN Trunking Protocol)** allows Cisco switches to share VLAN information across a network, reducing manual configuration.  
It operates in 3 main modes:

- 🧭 **Server** – Central controller that creates/modifies VLANs.
- 🕸️ **Transparent** – Passes VLAN info but does **not** apply changes.
- 📥 **Client** – Receives VLAN info from the server.

---

## 🛠️ Topology Overview

```
[SERVER] 🌐─────📶─────[TRANSPARENT] 🌐─────📶─────[CLIENT]
   |                       |                      |
  Fa0/1                  Fa0/1, Fa0/2            Fa0/2
```

- **All trunk links**
- **VTP Domain**: `cisco`
- **VTP Password**: `abc@123`

---

## 🔧 Switch Configuration Summary

| 🔗 Switch      | 🧱 Hostname    | 🎭 VTP Mode   | 🔐 Password  | 🌐 Trunk Ports         |
|---------------|----------------|---------------|--------------|------------------------|
| Server        | `server`       | `server`      | `abc@123`    | `FastEthernet0/1`      |
| Transparent   | `transparent`  | `transparent` | `abc@123`    | `FastEthernet0/1, 0/2` |
| Client        | `client`       | `client`      | `abc@123`    | `FastEthernet0/2`      |

---

## 📝 Configuration Commands

Here’s a quick reference for applying basic VTP settings on each switch:

### 🧭 Server Mode:
```bash
Switch> enable
Switch# configure terminal
Switch(config)# vtp domain cisco
Switch(config)# vtp mode server
Switch(config)# vtp password abc@123
Switch(config)# vtp version 2
Switch(config)# interface fa0/1
Switch(config-if)# switchport mode trunk
```

### 🕸️ Transparent Mode:
```bash
Switch(config)# vtp domain cisco
Switch(config)# vtp mode transparent
Switch(config)# vtp password abc@123
Switch(config)# vtp version 2
Switch(config)# interface range fa0/1 - 2
Switch(config-if)# switchport mode trunk
```

### 📥 Client Mode:
```bash
Switch(config)# vtp domain cisco
Switch(config)# vtp mode client
Switch(config)# vtp password abc@123
Switch(config)# vtp version 2
Switch(config)# interface fa0/2
Switch(config-if)# switchport mode trunk
```

---

## 📡 How to Test

1. ✅ Create VLANs on the **Server**:
   ```bash
   vlan 10
   name SALES
   vlan 20
   name HR
   ```

2. 🔍 On the **Client**, run:
   ```bash
   show vlan brief
   ```

3. 🧪 VLANs 10 & 20 should now appear — without manually creating them on the client! 🎉

---

## 📦 Extras

- 💡 Use `show vtp status` to verify mode, domain, revision number.
- 🔧 Ensure trunk links are UP and properly configured on all switches.
- 🧯 If VLANs don't sync, check:
  - Trunk links
  - VTP password
  - Domain name mismatch
  - VTP version differences

---

## 👨‍💻 Author

Designed for learning and practical understanding of VTP using Cisco Packet Tracer.  
Feel free to tweak it and explore more complex VLAN scenarios!

Happy networking! ⚙️🌐
