ansible::fail2ban
==================

The fail2ban role installs and manages the configuration for fail2ban.

By default, this provides a fail2ban install that works with firewalld, and looks for sshd logins.

Please note that this role will DROP packets instead of REJECT.
The fail2ban maintainers feel this is the wrong way to go (https://github.com/fail2ban/fail2ban/issues/507).

This is done by overriding the iptables-blocktype with a .local file.
If you prefer to keep the default behaviour, set `fail2ban_blocktype` to any value other than DROP.


It (will) also provides jails for other software, such as suricata and nginx.

suricata
---------

Suricata logs can be used by fail2ban to identify hosts to block.

The current configuration looks for hosts triggering Sev. 1 alerts in suricata.
It also looks for hosts matching EmergingThreat's DROP and COMPROMISED rules.

Hosts identified in this way are prevented from connecting to SSH, HTTP, and HTTPS.
If you need other, or different, services to be protected, you can edit templates/jail.suricata.j2.
