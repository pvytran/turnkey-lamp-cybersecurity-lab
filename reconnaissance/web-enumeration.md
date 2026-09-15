# Web Enumeration

## Target

TurnKey LAMP Server

**IP Address:** 192.168.56.106

## Web Server

Apache HTTP Server

## Web Services

- HTTP — Port 80
- HTTPS — Port 443

## TurnKey Web Interface

The TurnKey LAMP landing page provides access to:

- Control Panel
- Webmin
- Adminer
- Resources and References

## Initial Security Observation

The server exposes administrative web interfaces including Webmin
and Adminer.

These interfaces increase the server's attack surface and should
be reviewed to determine whether they are appropriately protected.

## Database Exposure

Port 3306 was identified as closed during the initial scan.

Therefore, the MySQL/MariaDB service was not directly accessible
from the Kali testing machine.

## Testing Environment

Testing was performed from Kali Linux against the intentionally
configured TurnKey LAMP server in a private VirtualBox lab.

No production systems were tested.
