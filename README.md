# TurnKey LAMP Cybersecurity Lab

## Overview

This project documents the deployment, reconnaissance, security assessment,
and hardening of a TurnKey LAMP server in a controlled VirtualBox lab.

## Lab Architecture

| System | Role | IP Address |
|---|---|---|
| Kali Linux | Security Testing Machine | 192.168.56.105 |
| TurnKey LAMP | Web Server / Target | 192.168.56.106 |

## Technologies

- TurnKey Linux LAMP
- Apache
- PHP
- MariaDB/MySQL
- Webmin
- Adminer
- Kali Linux
- Nmap
- VirtualBox

## Objectives

- Deploy a TurnKey LAMP server
- Configure a private lab network
- Perform network reconnaissance
- Identify exposed services
- Enumerate the web server
- Review administrative interfaces
- Identify security risks
- Apply security improvements
- Retest the configuration
- Document findings and remediation

## Initial Network Scan

The TurnKey LAMP server was scanned from Kali Linux.

Initial findings:

| Port | State | Service |
|---|---|---|
| 22/tcp | Open | SSH |
| 80/tcp | Open | HTTP |
| 443/tcp | Open | HTTPS |
| 3306/tcp | Closed | MySQL |

## Web Server

The server was identified as Apache.

The TurnKey landing page exposed:

- Control Panel
- Webmin
- Adminer
- Resources and References

## Initial Security Observation

Administrative applications such as Webmin and Adminer increase
the potential attack surface of the server and should be reviewed
and appropriately restricted.

The MySQL service was not directly accessible from the Kali testing
machine because port 3306 was closed.

## Testing Environment

All testing was performed against an intentionally configured
TurnKey LAMP virtual machine in a private VirtualBox lab.

No production systems were tested.

## Status

- [x] TurnKey LAMP deployed
- [x] Kali connectivity established
- [x] Apache identified
- [x] HTTP/HTTPS identified
- [x] Initial Nmap reconnaissance completed
- [x] Web interface identified
- [ ] Webmin security review
- [ ] Adminer security review
- [ ] Security findings
- [ ] Hardening
- [ ] Retesting
- [ ] Final security report
