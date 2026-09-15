# Security Findings

## Finding 1 — Administrative Web Interfaces Exposed

### Description

The TurnKey LAMP server exposes administrative web applications
through the network.

The identified interfaces include:

- Webmin on TCP port 12321
- Adminer 4.8.1 through the web interface

### Evidence

Nmap identified TCP port 12321 as an open TLS service.

Browser verification confirmed that the service is Webmin.

Adminer 4.8.1 was also identified through the TurnKey LAMP
web interface.

### Security Impact

Administrative interfaces increase the attack surface of the
server. If improperly configured or exposed to untrusted networks,
they could provide additional opportunities for unauthorized access.

### Recommendation

Restrict administrative interfaces to trusted management systems
and ensure strong authentication is enabled.

---

## Finding 2 — Webmin Uses a Local TLS Certificate

### Description

The Webmin service uses a certificate identifying:

- Common Name: tkldev
- Organization: TurnKey GNU/Linux
- RSA: 2048-bit
- Signature Algorithm: SHA-256

### Security Impact

The certificate appears to be intended for the local TurnKey
environment. In a production environment, certificate trust and
proper certificate management should be verified.

### Recommendation

Use a properly trusted certificate for production deployments
and ensure certificates are monitored and renewed appropriately.

---

## Finding 3 — Database Port Not Directly Exposed

### Description

The initial Nmap scan showed TCP port 3306 as closed.

This indicates that the database service was not directly accessible
from the Kali testing machine.

### Security Impact

Keeping the database service inaccessible from the testing network
reduces direct network exposure.

### Recommendation

Continue restricting database access to only the systems that
require it.

---

## Testing Limitations

Testing was performed against an intentionally configured TurnKey
LAMP virtual machine in a private VirtualBox lab.

No credential attacks, authentication bypasses, or destructive
exploitation were performed.
