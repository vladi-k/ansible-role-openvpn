ansible-role-openvpn
=========

Install and configure OpenVPN client/server.

Requirements
------------

* YUM repository with openvpn (like EPEL)
* SSL certificates (including CA)

Role Variables
--------------

* `openvpn_packages` - list of packages to install
* `openvpn_type` - client or server
* `openvpn_cert_dirs` - list of certificate directories
* `openvpn_certs` - list of certificates, example:

```yaml
openvpn_certs:
  - content: "{{ lookup('file', inventory_dir+'/../files/client1/openvpn/client1.crt') }}"
    dest: /etc/openvpn/client/secure/client1.crt
  - content: "{{ lookup('file', inventory_dir+'/../files/client1/openvpn/client1.key') }}"
    dest: /etc/openvpn/client/secure/client1.key
```

* `openvpn_chroot_dir` - directory for chroot jail
* `openvpn_chroot_user` - OS user for chroot directory
* `openvpn_user` - openvpn OS user
* `openvpn_ccd_dir` - path for ccd directory
* `openvpn_ccd_configs` - list of ccd configs, example:

```yaml
openvpn_ccd_configs:
  - file: client1
    content: ifconfig-push 10.7.0.29 10.7.0.1
```

* `openvpn_configs` - list of openvpn configs, example:

```yaml
openvpn_configs:
  - name: vpn.example.com
    settings:
      - server 10.7.0.0 255.255.255.0
      - port 1194
      - proto udp
      - dev tun
```

* `openvpn_restart` - boolean to restart openvpn on config changes

Dependencies
------------

Collections:

* `ansible.builtin`

Example Playbook
----------------

```yaml
- hosts: servers
  roles:
    - ansible-role-openvpn
```

License
-------

GPLv3

Author Information
------------------

Vladimir Vasilev
