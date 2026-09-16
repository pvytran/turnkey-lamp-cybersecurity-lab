# TurnKey LAMP Cybersecurity Lab

## Overview

This project documents a security assessment of a TurnKey LAMP
server deployed in a controlled VirtualBox lab.

The assessment covers network reconnaissance, web service
enumeration, administrative interface review, firewall hardening,
and post-remediation testing.

## Lab Architecture

| System | Role | IP Address |
|---|---|---|
| Kali Linux | Security Testing Machine | 192.168.56.105 |
| TurnKey LAMP | Target Web Server | 192.168.56.106 |

**Network:** VirtualBox Host-Only `192.168.56.0/24`

## Objectives

- Deploy a TurnKey LAMP server
- Configure a private security testing environment
- Perform network reconnaissance
- Identify exposed services
- Enumerate web applications
- Review administrative interfaces
- Identify security findings
- Apply firewall hardening
- Verify remediation
- Document the assessment

## Tools

- Kali Linux
- TurnKey LAMP
- VirtualBox
- Nmap
- cURL
- iptables
- iptables-persistent
- Web browser

## Initial Reconnaissance

Nmap identified the following services:

| Port | State | Service |
|---|---|---|
| 22/tcp | Open | SSH |
| 80/tcp | Open | HTTP |
| 443/tcp | Open | HTTPS |
| 3306/tcp | Closed | MySQL |

Apache was identified as the web server.

## Web Enumeration

The TurnKey web interface exposed:

- Control Panel
- Webmin
- Adminer

### Webmin

Webmin was identified on:

`https://192.168.56.106:12321/`

Webmin used HTTPS and MiniServ.

The service was initially listening on:

`0.0.0.0:12321`

### Adminer

Adminer **4.8.1** was identified through the web interface.

The login interface requested:

- Server
- Username
- Password

No credential attacks or authentication bypass attempts were performed.

## Security Findings

The assessment identified:

1. Administrative web interfaces exposed through the network
2. Webmin listening on all IPv4 interfaces
3. A local TurnKey TLS certificate
4. MySQL port 3306 not directly accessible from Kali

## Hardening

Webmin TCP port `12321` was restricted using the firewall.

Kali:

`192.168.56.105`

was explicitly allowed to access Webmin.

Other IPv4 sources were blocked from accessing TCP port `12321`.

The firewall configuration was saved using `iptables-persistent`:

`/etc/iptables/rules.v4`

## Retesting

After hardening and rebooting the TurnKey LAMP server:

- Firewall rules remained present
- Webmin remained accessible from Kali
- Authorized management access continued to work

## Evidence

Screenshots and supporting documentation are organized in:

```text
reconnaissance/
screenshots/
security/
report/

Security Testing Workflow

Reconnaissance
      ↓
Service Enumeration
      ↓
Web Enumeration
      ↓
Security Findings
      ↓
Hardening
      ↓
Retesting
      ↓
Documentation


Testing Scope

Testing was performed only against an intentionally configured
TurnKey LAMP virtual machine in a private VirtualBox lab.

No production systems were tested.

No credential attacks, brute-force attacks, authentication
bypasses, or destructive exploitation were performed.

Project Status
 TurnKey LAMP deployed
 Private lab network configured
 Nmap reconnaissance completed
 Web services enumerated
 Webmin identified
 Adminer 4.8.1 identified
 Security findings documented
 Webmin firewall hardening completed
 Firewall persistence configured
 Post-hardening retest completed
 Final security assessment documented
