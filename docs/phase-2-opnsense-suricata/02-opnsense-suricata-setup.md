
### Custom Rules Added
Because OPNsense 26.x restricts the Web UI and CLI for custom rules, we used the boot script method (`/usr/local/etc/rc.syshook.d/early/99-custom-suricata`) to inject our rules into `/usr/local/etc/suricata/rules/opnsense-user.rules` and force Suricata to load them.

Custom Rules:
- `sid:1000001` - LAB-NMAP SYN Scan Detected (Threshold: 20 SYN packets in 5 secs)
- `sid:1000002` - LAB-Reverse Shell Outbound Detected (Content: "bash")
- `sid:1000003` - LAB-SSH Brute Force Attempt (Threshold: 5 connections in 30 secs on Port 22)

### Current Status
- [x] Suricata settings configured
- [x] Rulesets enabled and updated
- [x] Suricata engine started and running
- [x] Custom lab rules injected and loaded
- [x] EVE JSON log verified (Nmap scan from Kali successfully triggered alert!)
```

#!/bin/sh

# Create the custom rules file for Suricata
mkdir -p /usr/local/etc/suricata/rules/
cat << 'EOF' > /usr/local/etc/suricata/rules/opnsense-user.rules
alert tcp any any -> any any (msg:"LAB-NMAP SYN Scan Detected"; flags:S; threshold:type both, track by_src, count 20, seconds 5; classtype:attempted-recon; sid:1000001; rev:1;)
alert tcp any any -> any any (msg:"LAB-Reverse Shell Outbound Detected"; flow:established,to_server; content:"bash"; nocase; classtype:trojan-activity; sid:1000002; rev:1;)
alert tcp any any -> any 22 (msg:"LAB-SSH Brute Force Attempt"; flow:to_server; threshold:type both, track by_src, count 5, seconds 30; classtype:attempted-admin; sid:1000003; rev:1;)
EOF

# Ensure OPNsense includes this file in its rule list
grep -q "opnsense-user.rules" /usr/local/etc/suricata/installed_rules.yaml || echo "  - opnsense-user.rules" >> /usr/local/etc/suricata/installed_rules.yaml