ansible
========

This is my collection of useful ansible playbooks.

It is (strongly) biased towards RedHat-likes (CentOS, specifically), and openSUSE.
No testing with debian-likes (or others, e.g. Arch) is done.

It started as a means of doing simple post-install housekeeping and hardening.
These are part of the common playbook (playbooks/common.yml), which is applied to all hosts by default.

All roles (will eventually) come with a README that details their functionality.

Motivations
------------

I have two domains, and two VPSes.

I currently have one VPS per domain.

I run some services for each domain, which are mainly web-based apps, with DBs.

I would like to have both VPSes serve both domains, without a load balancer in front.
I don't necessarily have the VPSes on the same provider, and my only tool is DNS.
I may introduce a load-balancer layer in future, but the basic site should work either way.

I would like to have this setup be completely transparent to users.

I would like to ensure my domains are completely separated (i.e. tenant isolation).

I would like to use only my system's init manager (which is systemd), and not rely on docker beyond containerisation.
I don't want orchestration, because I basically only run Daemonsets/StatefulSets ( in k8s terms ).

I would like all data to be encrypted between endpoints.

I don't care so much about efficient packing, I mainly want one instance per node of my domain services.

I want monitoring and logging to be available centrally, and built in to the system.

Approach
-------------

The playbooks aim to fullfill two basic deployment scenarios:

* within a trusted LAN, to build either a lab or home/soho network for a person with too much time on their hands.
* to provision internet facing services across machines that speak SSH.

The intent is for the latter scenario to be the default one, with switches to disable the paranoia/overhead.

Docker is used/assumed for running containers.

However, docker is only used for two aspects of the overall setup:

* actually running containers (i.e. could be replaced by rkt)
* container network creation (calico is already used to provide policy and IPAM)

The basic result is a fully uncoordinated service set based on node count.
Failover is achieved by having each node run a container-aware proxy that can use services running on other nodes.
Additionally, systemd is used to (try and) restart failed containers.

Wherever possible, DNS SRV records are used for service discovery.


Basic usage
---------------

The intent is for a host to use layers of setup:

* the common layer provides a reasonably good basis for any given system
* the infra layer provides shared services like etcd, ntp, dns and service discovery with consul
* the monitoring layer provides a prometheus based monitoring setup (currently)
* the logging layer defines the logging infrastructure, with syslog, ELK
* the identity layer currently provides 2FA and auth via privacyIDEA, and a PKI using cfssl
* the compute layer provides docker and/or libvirt with kvm/qemu, calico
* the load balancing layer provides haproxy and vulcand
* the application layer deploys containerised applications and services


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

