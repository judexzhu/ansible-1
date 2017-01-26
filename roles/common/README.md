ansible::common
================

The common role is used to create a suitable environment for ansible to manage the system in.

This role handles a few basic setup tasks.


Create local user for ansible to use
-------------------------------------

This is done in order to restrict (or deny) root logins (notably via SSH).

The part of the process does the following:

* looks for a suitable id_rsa.pub under ~/.ssh/ (of the user running ansible).
* creates an unprivileged user (ansible:deploy, by default) on the target system
* populates authorised keys for that user based on the id_rsa.pub found previously, or based on variable data.
* creates a sudoers.d file allowing tty-less, password-less access to ALL
