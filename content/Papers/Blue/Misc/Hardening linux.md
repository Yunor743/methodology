- Firewall
- Fail2Ban
- AV / NGAV
- HIDS
- SIEM
- Auditd
- SysmonForLinux (eBPF)
- SELinux / Apparmor (SELinux = more granular, Apparmor = easier to use. Use only **one** of them at a time. [source](https://askubuntu.com/questions/23422/is-it-a-bad-idea-to-run-selinux-and-apparmor-at-the-same-time)
- LKRG
- USBGuard
- Backup (rsync / rclone + google drive)
- BIOS password
- Filesystem encrypted

#### Audit
- Lynis
- Linpeas.sh

#### Monitoring
- hunt for revshell with : `sudo netstat -anp | grep ESTABLISHED`

---

# To check

##### HIDS eBPF Based
- Falco
- https://tetragon.io/
- https://github.com/chriskaliX/Hades
- SysmonForLinux

##### Network
- zeek
- snort
- suricata

#### Wazuh Integrations:
- [wazuh x auditd](https://wazuh.com/blog/monitoring-root-actions-on-linux-using-auditd-and-wazuh/) [other link](https://documentation.wazuh.com/current/user-manual/capabilities/system-calls-monitoring/audit-configuration.html)
- [wazuh x falco](https://github.com/wazuh/wazuh-ruleset/pull/528)
- [wazuh x suricata](https://documentation.wazuh.com/current/proof-of-concept-guide/integrate-network-ids-suricata.html) [other link](https://wazuh.com/blog/detecting-illegitimate-crypto-miners-on-linux-endpoints/) [other link](https://wazuh.com/blog/responding-to-network-attacks-with-suricata-and-wazuh-xdr/)
- [wazuh x virustotal](https://documentation.wazuh.com/current/proof-of-concept-guide/detect-remove-malware-virustotal.html)
- [wazuh x URLhaus](https://wazuh.com/blog/detecting-malicious-urls-using-wazuh-and-urlhaus/)
- [wazuh x theHive](https://wazuh.com/blog/using-wazuh-and-thehive-for-threat-protection-and-incident-response/)


---
### SIEM XDR solutions:

- Wazuh (more HIDS ?)
- UTMStack (more XDR ?)
- SecurityOnion (More SIEM ?)

https://www.reddit.com/r/AskNetsec/comments/10lw9cy/utmstack_vs_wazuh_vs_security_onion/
https://www.blackhillsinfosec.com/wp-content/uploads/2021/03/SLIDES_OpenandFreeEDR.pdf

---

### HIDS Comparison

https://en.wikipedia.org/wiki/Host-based_intrusion_detection_system_comparison

---

##### Sources:

- https://madaidans-insecurities.github.io/guides/linux-hardening.html