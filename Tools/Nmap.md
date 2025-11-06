Scans for version, runs scripts, runs verbose and saves output:
* sudo nmap -sV -sC \<IP> -vv -oN nmap
Run default vuln scripts:
* sudo nmap -sS –script=vuln
Scan for all devices on a network IP/MAC:
* sudo nmap -sn 192.168.1.0/24
