# Splunk Enterprise Installation

## Objective
Install Splunk Enterprise on the SOC SIEM server in an isolated environment.

## Environment
- OS: Ubuntu Server
- Hostname: splunk-siem
- IP: 10.50.30.10
- Network: vmbr4 (isolated)

# Splunk Enterprise Installation (VM 500)

## Goal
Install Splunk Enterprise on Ubuntu VM 500 in Proxmox and access Splunk Web.

## Environment
- Hypervisor: Proxmox (node: pve)
- VM: 500 (Splunk-SIEM)
- OS: Ubuntu Server (24.04.x)
- Temporary management access: vmbr0 (192.168.178.0/24)
- Splunk Web: http://192.168.178.80:8000
- Note: Browser shows “Not secure” because Splunk uses a self-signed certificate by default.

## Steps

### 1. Prepare VM
- Create VM 500 (Ubuntu Server)
- Ensure VM boots successfully
- Configure temporary management NIC if needed (vmbr0) to download packages directly from the VM

### 2. Download Splunk (.deb) inside VM
From the VM console/SSH:

```bash
cd ~
wget -O splunk.deb "https://download.splunk.com/products/splunk/releases/10.2.0/linux/splunk-10.2.0-d749cb17ea65-linux-amd64.deb"
ls -lh splunk.deb

```

3. Install Splunk

```bash
sudo dpkg -i splunk.deb
# If dependencies fail:
sudo apt --fix-broken install -y
sudo dpkg -i splunk.deb
```
4. Start Splunk and accept license
```bash
         sudo /opt/splunk/bin/splunk start --accept-license
sudo /opt/splunk/bin/splunk status

```

5. Access Splunk Web

Open in browser:

http://192.168.178.80:8000


