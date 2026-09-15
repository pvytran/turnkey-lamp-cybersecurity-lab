# Webmin Enumeration

## Target

TurnKey LAMP Server

**IP Address:** 192.168.56.106

## Webmin

Webmin was identified through the TurnKey LAMP web interface.

- Protocol: HTTPS
- Port: 12321/tcp
- URL: `https://192.168.56.106:12321`

## Service Identification

Nmap identified port 12321 as an SSL/TLS service.

Browser verification confirmed that the service is Webmin.

The HTTP response identified the Webmin MiniServ server:

```text
Server: MiniServ

The service also required authentication:
Auth-type: auth-required=1

TLS Certificate

Nmap identified a certificate issued to:

Common Name: tkldev
Organization: TurnKey GNU/Linux

The certificate uses:

RSA 2048-bit public key
SHA-256 with RSA encryption

The certificate appears to be a local/self-signed TurnKey certificate intended for the lab environment.

Security Observation

Webmin is a web-based administrative interface that provides
server administration capabilities.

Because Webmin provides administrative functionality, access
should be restricted to trusted management systems and protected
with strong authentication.

The service uses HTTPS, which protects the connection from
plain-text transmission. However, the certificate should be
reviewed in a production environment to ensure that it is
trusted and properly managed.

Testing Environment

The Webmin interface was identified during authorized testing
of the TurnKey LAMP virtual machine in a private VirtualBox lab.

No production systems were tested.

## Adminer Enumeration

Adminer was identified through the TurnKey LAMP web interface.

**Application:** Adminer

**Version:** 4.8.1

**Interface:** Database login page

The Adminer interface provides fields for:

- Server
- Username
- Password

## Security Observation

Adminer is a web-based database administration interface.

Because it provides database management functionality, exposing
Adminer through the web server increases the administrative attack
surface.

The interface should be restricted to authorized administrators
and should not be unnecessarily exposed to untrusted networks.

No authentication bypass or credential attacks were performed.

## Testing Environment

Adminer was identified during authorized testing of the TurnKey
LAMP virtual machine in a private VirtualBox lab.

No production systems were tested.
