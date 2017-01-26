fail2ban
=========

The fail2ban role installs and manages the configuration for fail2ban.

By default, this provides a fail2ban install that works with firewalld, and looks for sshd logins.
It will DROP packets instead of REJECT.
Please note the fail2ban author feels this is the wrong way to go (https://github.com/fail2ban/fail2ban/issues/507).

It (will) also provides jails for other software, such as suricata and nginx.

