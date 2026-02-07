
# SOC Homelab – Splunk SIEM

This project documents the design and implementation of a personal Security Operations Center (SOC) home lab using **Splunk SIEM**.

The lab is built on **Proxmox** and simulates real-world SOC workflows:
- Attacks
- Log ingestion
- Detection
- Investigation

## Architecture Overview
- Hypervisor: Proxmox
- SIEM: Splunk Enterprise
- Victim: Windows
- Attacker: Kali Linux
- Network: Isolated internal bridge (vmbr4)

## Lab Network Design
| Component | IP Address |
|--------|-----------|
| Splunk SIEM | 10.50.30.10 |
| Windows Victim | 10.50.30.20 |
| Kali Attacker | 10.50.30.30 |

## Scenarios
- Brute-force login attack detection
- Windows log ingestion
- Alert creation and investigation

## Status
- [x] Proxmox network isolation
- [x] Static IP configuration
- [ ] Splunk installation
- [ ] Windows forwarder setup
- [ ] Brute-force detection rule

## Disclaimer
This lab is for **educational purposes only** and runs in an isolated environment.