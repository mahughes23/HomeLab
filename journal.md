## Lab Journal

### 2025-11-01
- Installed OPNsense, Kali Linux on VMware
- Configured network adapters to make all Kali traffic go through OPNsense firewall
  - Issue: Kali could ping OPNsense but neither could ping the internet
  - Fix: Manually changed VMnet1 Host-only network to use same subnet addr as OPNsense
- Installed Suricata IDS/IPS
- Added rule to OPNsense to alert when the network is scanned with nmap:
```text
alert tcp $HOME_NET any -> 192.168.1.1/24 any (msg:"POSSIBLE NMAP SYNSTEALTH SCAN DETECTED"; flow:stateless; flags:S; priority:5; threshold:type threshold, track by_src, count 50, seconds 1; classtype:attempted-recon; sid:1234;)
```
- Tested out this rule by calling nmap 192.168.1.1 in terminal, successfully alerted