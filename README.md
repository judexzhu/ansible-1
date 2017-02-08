ansible
========

This is my collection of useful ansible playbooks.

It is (strongly) biased towards RedHat-likes (CentOS, specifically), and openSUSE.
No testing with debian-likes (or others, e.g. Arch) is done.

It started as a means of doing simple post-install housekeeping and hardening.
These are part of the common playbook (playbooks/common.yml), which is applied to all hosts by default.

All roles (will eventually) come with a README that details their functionality.

default profile
-----------------

Currently, calling ansible-playbook, and using the included site.yml, will:

* do some basic setup and hardening (see common and hardening roles)
* install firewalld and fail2ban
* install auditd
* install docker (for RedHat-likes, it will use the docker repo, rather than EPEL).
* install rkhunter, sysdig, and falco
* tighten up the SSH server
* install and configure selinux to enforcing mode
* install prometheus' node_exporter

The following switches exist to skip parts of this

* skip_auditd
* skip_firewalld
* skip_sysdig
* skip_monitoring (which currently skips prometheus)
* skip_docker

Additionally, it can:

* for hosts in the 'consul' group, install consul and run it as an agent, to advertise services running on the node
* for hosts in the 'ids' group, configure suricata, and configure fail2ban to use its logs.
* for hosts in the 'consul_server' group, configure consul in server mode, and install the UI.
* for hosts in the 'prometheus_server' group, configure prometheus, and advertise it with consul.
* for hosts in the 'prometheus_alertmanager' group, configure prometheus' alertmanager, and advertise it with consul.

You can ignore/avoid all service (i.e. systemd) related calls with `--skip-tags service`.
This aims to help use the roles in docker containers.

License
--------


Copyright (C) 2017 iwaseatenbyagrue

This program is free software: you can redistribute it and/or modify
it under the terms of the GNU General Public License as published by
the Free Software Foundation, either version 3 of the License, or
(at your option) any later version.

This program is distributed in the hope that it will be useful,
but WITHOUT ANY WARRANTY; without even the implied warranty of
MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
GNU General Public License for more details.

You should have received a copy of the GNU General Public License
along with this program.  If not, see <http://www.gnu.org/licenses/>.

