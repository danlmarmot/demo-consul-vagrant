Role Name
========

Installs Supervisord via Python pip.
This version is often more up-to-date than what is available via standard package manager repos.

Requirements
------------

Python pip.  Installed on RedHat and Debian if not present.

Role Variables
--------------

The only variable is the default version of supervisord to install, which is 3.0.

From defaults/main.yml

    supervisord_version: 3.0           # Default version to install.


Dependencies
------------

None.

Example Playbook
-------------------------

Here's an example playbook.

    - hosts: servers
      roles:
         - { role: supervisord, supervisord_version: 3.0 }

License
-------

BSD

Author Information
------------------

Daniel McKean
