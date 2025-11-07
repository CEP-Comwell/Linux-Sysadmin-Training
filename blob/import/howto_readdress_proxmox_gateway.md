# Howto: Re-addressing the Proxmox Gateway Interface

## ✅ Overview
This guide explains how to **safely migrate or re-address the Proxmox VE gateway interface** without losing connectivity. It is designed for Proxmox VE 9.x and assumes you have **IPMI or console access** as a fallback.

---

## ✅ Why This Matters
Changing the management interface or gateway incorrectly can cause **loss of connectivity**, breaking cluster communication and web UI access. This guide ensures a **strategic, zero-downtime approach**.

---

## ✅ Prerequisites
- Proxmox VE 9.x installed
- IPMI/console access for emergency rollback
- `ifupdown2` installed for safe network reload:

```bash
apt install ifupdown2
```

---

## ✅ Strategic Approach
1. **Never remove the old IP until the new one is confirmed working**.
2. **Keep the default gateway on the original interface (vmbr0)** until migration is complete.
3. If using the **same subnet** on both interfaces, use `noprefixroute` to avoid routing conflicts.

---

## ✅ Step-by-Step Procedure

### 1. Add the new IP temporarily
```bash
ip addr add 172.16.10.13/24 dev eth3
```
Test connectivity:
```bash
ping 172.16.10.13
curl -k https://172.16.10.13:8006
```

### 2. Update `/etc/network/interfaces`
Add eth3 stanza:
```ini
auto eth3
iface eth3 inet static
    address 172.16.10.13/24
    # Do NOT add gateway here
```

### 3. Keep vmbr0 as gateway
Ensure vmbr0 retains:
```ini
gateway 172.16.10.1
```

### 4. Apply changes safely
```bash
ifreload -a
```

### 5. Verify
```bash
ip route show
ip addr show eth3
```
Expected:
```
default via 172.16.10.1 dev vmbr0
```

---

## ✅ Handling Same-Subnet Issues
If eth3 and vmbr0 share the same subnet, add:
```ini
noprefixroute yes
```
This prevents duplicate connected routes.

Or assign eth3 a **different subnet** temporarily.

---

## ✅ Persistence in `/etc/network/interfaces`
Example final config:
```ini
auto eth3
iface eth3 inet static
    address 172.16.10.13/24
    noprefixroute yes

auto vmbr0
iface vmbr0 inet static
    address 172.16.10.23/24
    gateway 172.16.10.1
    bridge-ports xg1
    bridge-stp off
    bridge-fd 0
```

---

## ✅ Rollback Plan
If connectivity fails:
1. Use IPMI console.
2. Remove eth3 IP:
```bash
ip addr flush dev eth3
```
3. Restart networking:
```bash
systemctl restart networking
```

---

## ✅ Verification
- Check routes:
```bash
ip route show
```
- Confirm Proxmox UI reachable on new IP.

---

## ✅ References
- [Proxmox Forum: Moving management interface safely](https://forum.proxmox.com/threads/moving-management-interface-to-new-interface.161932/)
- [ServeTheHome: Change Proxmox VE primary NIC](https://www.servethehome.com/how-to-change-proxmox-ve-primary-nic-when-a-new-interface-is-installed/)
- [NAKIVO: Change Proxmox IP address](https://www.nakivo.com/blog/how-to-change-primary-proxmox-ve-ip-address/)
