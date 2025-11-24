A role to set up djbdns (aka tinydns). The installation process was taken
directly from https://cr.yp.to/djbdns/install.html

# Variables

See defaults/main.yml for the variables and an explanation as to what they do.

# Examples
## Playbook
Here's an example of a playbook to install djbdns on the local machine. It does
not require you have SSH running.

```yaml
- hosts: localhost
  connection: local
  become: true
  roles:
    - role: hax0rbana_adam.djbdns
```

A more realistic playbook to run this role on a remote host:

```yaml
- hosts: all
  remote_user: root
  roles:
    - role: hax0rbana_adam.djbdns
      djbdns_bind_ip_address: 192.168.1.53
      djbdns_transfers: :allow,AXFR=""
      djbdns_data: |
        Z{{ ansible_domain }}:ns1.{{ ansible_domain }}:admin.{{ ansible_domain }}
        &{{ ansible_domain }}:1.2.3.53:ns1.{{ ansible_domain }}
        &{{ ansible_domain }}:3.2.1.53:ns2.{{ ansible_domain }}
        @{{ ansible_domain }}:100.100.200.200:mail.{{ ansible_domain }}
        '{{ ansible_domain }}:v=spf1 mx -all
        '_dmarc.{{ ansible_domain }}:v=DMARC1; p=none
        A{{ ansible_domain }}:100.100.100.100
        Cwww.{{ ansible_domain }}:{{ ansible_domain }}
```

The latter example allows anyone to query the nameserver, and nobody is
allowed to do zone transfers. 

# Official repo location
All activity takes place on the official GitLab instance:
[https://gitlab.hax0rbana.org/public-repos/ansible/ansible-role-djbdns](https://gitlab.hax0rbana.org/public-repos/ansible/ansible-role-djbdns)

Any other hosting providers, such as GitHub.com and GitLab.com, are just mirrors
and we do not monitor the issue trackers over there.

# Support
## Matrix channel
You can also join our Matrix channel: #ansible:hax0rbana.org

This is a good place to ask questions or make requests without having to sign
up for another account.

# Contributing
See [contributor guidelines](CONTRIBUTING.md).

# License
This project is licensed under MIT License. See [LICENSE](LICENSE) for more details.
