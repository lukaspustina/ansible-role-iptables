iptables
========

Installs UFW and configures iptables firewall rules.

Requirements
------------

None.

Role Variables
--------------

`_iptables` containes the rules and general settings.

Dependencies
------------

None.

Example Playbook
----------------

```
    - hosts: servers
      vars:
        IPTABLES:
          default_policy:
            incoming: reject
          state: enabled
          rules:
            - interface: eth0
              ip: "{{ ansible_eth0.ipv4.address }}"
              ports:
                - { name: ssh, port: 22, proto: tcp, direction=in, rule=allow, delete: no }
                - { name: http, port: 80 }
                - { name: https, port: 443 }
            - interface: eth0
              ip: "{{ ansible_eth0.ipv6[0].address }}"
              ports:
                - { name: ssh, port: 22, proto: tcp, direction=in, rule=allow, delete: no }
      roles:
        - { role: iptables, tags: ['iptables'], _iptables: "{{ IPTABLES }}" }
```

License
-------

See LICENSE file.

Author Information
------------------

Initially created by Lukas Pustina [@drivebytesting](https://twitter.com/drivebytesting).

