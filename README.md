Ansible Role : dginhoux.pxe_init_syslinux
=========

This ansible role install all necessary to built a PXE install server (isc-dhcp, tftp, nginx).

In files/syslinux/, are provided version of syslinux for bios and efi64 systems. To upgrade them, theses files must be updated (like this role).



Requirements
------------

This role is built to only run on platforms defined in `meta/main.yml`


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
