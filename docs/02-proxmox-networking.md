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


---


