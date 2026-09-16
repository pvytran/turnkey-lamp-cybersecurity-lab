# Security Hardening

## Webmin Network Access Restriction

### Before Hardening

Webmin was listening on all IPv4 interfaces:

```text
0.0.0.0:12321

The firewall initially used an ACCEPT policy with no INPUT rules.

Hardening Change

Webmin TCP port 12321 was restricted using the firewall.

The Kali testing system at 192.168.56.105 was explicitly allowed
to access Webmin.

Other IPv4 sources were blocked from accessing TCP port 12321.

Firewall Configuration

ACCEPT  TCP  source 192.168.56.105  destination port 12321
DROP    TCP  other sources           destination port 12321


Retest

The configuration was tested from Kali Linux.

Expected result:

12321/tcp open

This confirms that the authorized Kali testing system can still
access Webmin after the firewall restriction was applied.

Testing Environment

The hardening was performed against the TurnKey LAMP virtual
machine in a private VirtualBox lab.

## Webmin Retest

After applying the firewall restriction, Webmin remained accessible
from the authorized Kali testing system at `192.168.56.105`.

The Webmin interface was successfully accessed using:

`https://192.168.56.106:12321/`

This confirmed that the firewall restriction did not prevent the
authorized management system from accessing Webmin.

## Result

The Webmin access restriction was successfully applied and verified
from the Kali testing machine.

## Firewall Persistence

The `iptables-persistent` package was configured so that the
Webmin firewall rules survive a system reboot.

The IPv4 firewall configuration was saved in:

```text
/etc/iptables/rules.v4
