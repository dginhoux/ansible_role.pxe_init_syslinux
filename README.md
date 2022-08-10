ginhouxnet.pxe_init_syslinux
=========

This ansible role install all necessary to built a PXE install server (isc-dhcp, tftp, nginx).

In files/syslinux/, are provided version of syslinux for bios and efi64 systems. To upgrade them, theses files must be updated (like this role).



Requirements
------------

This ansible role will only run on identified OS defined on meta/main.yml


Role Variables
--------------

View defaults/main.yml and vars/{{ ansible_os_family }}



Dependencies
------------




Example Playbook
----------------



License
-------

BSD


Author Information
------------------

Dany GINHOUX
