# ROLE dginhoux.pxe_init_syslinux



## DESCRIPTION

This ansible role install all necessary to built a PXE install server (isc-dhcp, tftp, nginx).<br />
<br />
In files/syslinux/, are provided version of syslinux for bios and efi64 systems. To upgrade them, theses files must be updated (like this role).



## REQUIREMENTS

#### SUPPORTED PLATFORMS

This role require a supported platform.<br />
It will skip process with unsupported platform to avoid any compatibility problem.<br />
This behaviour can be bypassed by settings the following variable `asserts_bypass=True`.

| Platform | Versions |
|----------|----------|
| Debian | buster, bullseye |
| Fedora | 33, 34, 35, 36, 37, 38 |
| EL | 7, 8 |

#### ANSIBLE VERSION

Ansible >= 2.13

#### DEPENDENCIES

None.



## INSTALLATION

#### ANSIBLE GALAXY

```shell
ansible-galaxy install dginhoux.pxe_init_syslinux
```
#### GIT

```shell
git clone https://github.com/dginhoux/ansible_role.pxe_init_syslinux dginhoux.pxe_init_syslinux
```


## USAGE

#### EXAMPLE PLAYBOOK

```yaml
- hosts: all
  roles:
    - name: start role dginhoux.pxe_init_syslinux
      ansible.builtin.include_role:
        name: dginhoux.pxe_init_syslinux
```


## VARIABLES

#### DEFAULT VARIABLES

Defaults variables defined in `defaults/main.yml` : 

```yaml
pxe_nginx_config_file: /etc/nginx/nginx.conf

pxe_dir_base: /srv/tftp

pxe_dir_structure:
  - os
  - sysprep/bios
  - sysprep/efi64
  - syslinux/bios
  - syslinux/efi64
  - menu/bios
  - menu/efi64

pxe_tftp_symlinks:
  - src: "../../os"
    dest: "{{ pxe_dir_base }}/syslinux/bios/os"
  - src: "../../os"
    dest: "{{ pxe_dir_base }}/syslinux/efi64/os"
  - src: "../../menu/bios"
    dest: "{{ pxe_dir_base }}/syslinux/bios/pxelinux.cfg"
  - src: "../../menu/efi64"
    dest: "{{ pxe_dir_base }}/syslinux/efi64/pxelinux.cfg"
```

#### DEFAULT OS SPECIFIC VARIABLES

Those variables files are located in `vars/*.yml` are used to handle OS differences.<br />
One of theses is loaded dynamically during role runtime using the `include_vars` module and set OS specifics variable's.


* Debian family : 

```yaml
pxe_packages:
  - isc-dhcp-server
  - tftpd-hpa
  - tftp-hpa
  # - pxelinux
  # - syslinux
  # - syslinux-efi
  # - syslinux-common
  - nginx

pxe_services:
  - isc-dhcp-server
  - tftpd-hpa
  - nginx

pxe_tftp_config_file: /etc/default/tftpd-hpa

pxe_tftp_config: |
  # Ansible managed
  TFTP_USERNAME="tftp"
  TFTP_DIRECTORY="/srv/tftp"
  TFTP_ADDRESS="0.0.0.0:69"
  TFTP_OPTIONS="--secure -v"
```

* RedHat family : 

```yaml
pxe_packages:
  - tftp-server
  - dhcp-server
  # - pxelinux
  # - syslinux
  # - syslinux-efi64
  # - syslinux-tftpboot
  - nginx

pxe_services:
  - dhcpd
  - tftp
  - nginx

pxe_tftp_config_file: /etc/systemd/system/tftp.service

pxe_tftp_config: |
  # Ansible managed
  [Unit]
  Description=Tftp Server
  Requires=tftp.socket
  Documentation=man:in.tftpd
  [Service]
  ExecStart=/usr/sbin/in.tftpd --secure -v /srv/tftp
  StandardInput=socket
  [Install]
  Also=tftp.socket
```



## AUTHOR

Dany GINHOUX - https://github.com/dginhoux



## LICENSE

MIT
