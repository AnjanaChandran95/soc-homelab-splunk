# Proxmox Networking Setup

## Objective
Create an isolated SOC lab network without impacting existing Proxmox projects.

## Existing Networks
- vmbr0: Home / WAN – 192.168.178.0/24
- vmbr1: 10.50.0.0/24
- vmbr2: 10.50.10.0/24
- vmbr3: 10.50.20.0/24

## Selected Network for SOC Lab
- Bridge: vmbr4
- CIDR: 10.50.30.0/24
- Reason: Unused bridge, no physical uplink, full isolation

## Static IP Configuration (Splunk SIEM)

File: `/etc/netplan/00-installer-config.yaml`

```yaml
network:
  version: 2
  ethernets:
    ens18:
      dhcp4: no
      addresses:
        - 10.50.30.10/24

        Verification
        ip a

        Result:

Interface ens18 is UP

IP address 10.50.30.10/24 assigned

## Ubuntu Target (Victim) VM Networking

This VM acts as the **SSH brute-force target** for SOC attack simulations.

### Dual-NIC Design

The victim VM is dual-homed to separate **management access** from **attack traffic**.

#### NIC 1 — SOC Lab Network
- Interface: ens18
- Proxmox bridge: vmbr4
- IP address: 10.50.30.20/24 (static)
- Purpose:
  - Receives attack traffic from attacker VM (Kali)
  - Sends authentication logs to Splunk SIEM

#### NIC 2 — Management / Home Network
- Interface: ens19
- Proxmox bridge: vmbr0
- IP address: 192.168.178.82/24 (DHCP)
- Purpose:
  - SSH access from host laptop
  - Temporary internet access for setup

### Verification

The following was verified on the VM:

- ens18 has IP `10.50.30.20/24`
- ens19 has IP `192.168.178.82/24`
- VM is reachable via SSH from host machine

### Security Note

The management interface (vmbr0) will be **removed or disabled later** to keep the SOC lab isolated.


---


