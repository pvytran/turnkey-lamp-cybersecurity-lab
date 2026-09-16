# TurnKey LAMP Security Assessment

## 1. Executive Summary

A security assessment was performed against an intentionally
configured TurnKey LAMP virtual machine in a private VirtualBox lab.

The assessment focused on network reconnaissance, web service
enumeration, administrative interface exposure, and basic
network-level hardening.

The assessment identified Webmin and Adminer as administrative
interfaces that increase the server's attack surface.

Webmin access was subsequently restricted to the authorized Kali
testing system using an IPv4 firewall rule.

The firewall configuration was saved using iptables-persistent
and verified after reboot.

---

## 2. Lab Environment

| System | Role | IP Address |
|---|---|---|
| Kali Linux | Security Testing Machine | 192.168.56.105 |
| TurnKey LAMP | Target Web Server | 192.168.56.106 |

### Network

Private VirtualBox Host-Only Network:

`192.168.56.0/24`

---

## 3. Reconnaissance

An Nmap service scan was performed against the TurnKey LAMP server.

Initial results:

| Port | State | Service |
|---|---|---|
| 22/tcp | Open | SSH |
| 80/tcp | Open | HTTP |
| 443/tcp | Open | HTTPS |
| 3306/tcp | Closed | MySQL |

Apache was identified as the web server.

---

## 4. Web Enumeration

The TurnKey LAMP web interface exposed several administrative
and management components.

Identified interfaces included:

- Control Panel
- Webmin
- Adminer

### Webmin

Webmin was identified on:

`https://192.168.56.106:12321/`

Webmin used HTTPS and the MiniServ server.

The Webmin configuration showed:

- HTTPS enabled
- SSLv2 disabled
- SSLv3 disabled

The Webmin service was initially listening on:

`0.0.0.0:12321`

### Adminer

Adminer version 4.8.1 was identified through the web interface.

The login page requested:

- Server
- Username
- Password

No credential attacks or authentication bypass attempts were
performed.

---

## 5. Security Findings

### Finding 1 — Administrative Interfaces Exposed

Webmin and Adminer provide administrative functionality and
increase the attack surface of the server.

### Finding 2 — Webmin Listening on All IPv4 Interfaces

Webmin was initially observed listening on:

`0.0.0.0:12321`

This allows the service to receive connections through available
IPv4 interfaces.

### Finding 3 — Local TLS Certificate

The Webmin certificate identified:

- Common Name: tkldev
- Organization: TurnKey GNU/Linux
- RSA 2048-bit key
- SHA-256 signature algorithm

The certificate appears intended for the local lab environment.

### Finding 4 — Database Port Not Directly Exposed

TCP port 3306 was closed during the initial scan.

This prevented direct database network access from the Kali
testing machine.

---

## 6. Remediation

A firewall restriction was applied to Webmin.

The Kali testing system was explicitly allowed to access TCP port
12321:

`192.168.56.105`

Other IPv4 sources were blocked from accessing TCP port 12321.

The resulting firewall policy included:

```text
ACCEPT TCP from 192.168.56.105 to port 12321
DROP TCP from other sources to port 12321


The configuration was saved using iptables-persistent.

The saved IPv4 configuration was:

/etc/iptables/rules.v4

7. Retesting

After the firewall change and system reboot, the firewall rules
were verified and remained present.

Webmin remained accessible from the authorized Kali testing system.

The Webmin interface was accessed using:

https://192.168.56.106:12321/

This demonstrated that the hardening change did not prevent the
authorized testing system from accessing Webmin.

8. Tools Used
Kali Linux
TurnKey LAMP
VirtualBox
Nmap
cURL
iptables
iptables-persistent
Web browser
9. Testing Limitations

Testing was performed only against the intentionally configured
TurnKey LAMP virtual machine in a private VirtualBox environment.

The assessment did not include:

Credential attacks
Brute-force attacks
Authentication bypass
Destructive exploitation
Testing of production systems
10. Conclusion

The assessment demonstrated a complete security testing workflow:

Network reconnaissance
Service enumeration
Web application enumeration
Security finding identification
Network-level hardening
Firewall persistence
Post-remediation retesting

The project demonstrates practical experience with Linux
administration, network reconnaissance, web service enumeration,
firewall configuration, and security documentation.
