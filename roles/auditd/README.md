ansible::auditd
================

The auditd role installs and configures the Linux audit daemon.

It also provides a base ruleset, based on:

* the NSA RedHat 5 hardening guide
* CIS benchmarks for Centos 6 and 7

Ruleset
--------

The auditd ruleset is built by concatenating files in /etc/audit/rules.d, in lexical order.

This role delivers two files to provide a basic ruleset:

* 00-auditd-base.rules, providing a number of rules monitoring significant aspects of the system.
* 999-immutable.rules, which makes the ruleset immmutable, in line with documented best practice.

Any custom rules should (ideally) be added with a prefix between 01 and 998.
