# Webmin Enumeration

## Target

TurnKey LAMP Server

**IP Address:** 192.168.56.106

## Webmin

Webmin was identified through the TurnKey LAMP web interface.

**Protocol:** HTTPS

**Port:** 12321/tcp

**URL:** `https://192.168.56.106:12321`

## Security Observation

Webmin is a web-based administrative interface. Because it provides
server administration capabilities, access to Webmin should be
restricted to trusted management systems and protected with strong
authentication.

## Testing Environment

The Webmin interface was identified during authorized testing of the
TurnKey LAMP virtual machine in a private VirtualBox lab.

No production systems were tested.
