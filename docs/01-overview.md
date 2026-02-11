### Lab Roles

- Splunk SIEM  
  Central log ingestion, detection, and investigation platform.

- Ubuntu Target (Victim)  
  Simulates a real Linux server exposed to brute-force attacks.

- Attacker VM (planned)  
  Kali Linux used to generate attack traffic.


  What we used:

Splunk Universal Forwarder on the victim

It sends logs over TCP port 9997

Splunk SIEM listens on that port
