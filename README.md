Ansible Role : dginhoux.pxe_init_syslinux
=========

This ansible role install all necessary to built a PXE install server (isc-dhcp, tftp, nginx).

In files/syslinux/, are provided version of syslinux for bios and efi64 systems. To upgrade them, theses files must be updated (like this role).



Requirements
------------

This role require a supported platform defined in `meta/main.yml`.
It will skip node with unsupported platform ; this behaviour can be bypassed by settings this variable `asserts_bypass=True`.


Role Variables
--------------

Necessary variables are defined on `defaults/main.yml`.
Specifics variables are in `vars/{{ ansible_os_family }}`.



Dependencies
------------

none


Example Playbook
----------------



License
-------

BSD


Author Information
------------------

https://github.com/dginhoux/
