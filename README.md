
## dnsmasq

[![Build Status](https://travis-ci.org/Oefenweb/ansible-dnsmasq.svg?branch=master)](https://travis-ci.org/Oefenweb/ansible-dnsmasq) [![Ansible Galaxy](http://img.shields.io/badge/ansible--galaxy-dnsmasq-blue.svg)](https://galaxy.ansible.com/Oefenweb/dnsmasq/)

Set up [Dnsmasq](http://www.thekelleys.org.uk/dnsmasq/doc.html) in Debian-like systems.

#### Requirements

None

#### Variables

* `dnsmasq_service_state`: [default: `started`]: The state of th service (e.g. `stopped`)
* `dnsmasq_service_enabled`: [default: `true`]: Whether the service should start on boot

* `dnsmasq_etc_default_domain_suffix`: [optional]: Specifies the domain which hosts read from the DHCP leases file must have to be legal (e.g. `dnsdomainname`)
* `dnsmasq_etc_default_dnsmasq_opts`: [optional]: Options to pass to the `dnsmasq` daemon (e.g. `--conf-file=/etc/dnsmasq.alt`)
* `dnsmasq_etc_default_config_dir`: [default: `/etc/dnsmasq.d,.dpkg-dist,.dpkg-old,.dpkg-new`]: Searches this drop directory for configuration options (leave empty to comment out)
* `dnsmasq_etc_default_ignore_resolvconf`: [optional]: If the `resolvconf` package is installed, `dnsmasq` will use its output rather than the contents of `/etc/resolv.conf` to find upstream nameservers (e.g. `true`)

* `dnsmasq_etc_default`: [see: `defaults/main.yml`]: List of lines to be added to `/etc/default/dnsmasq`

* `dnsmasq_dnsmasq_conf`: [default: `[]`]: List of lines to be added to `/etc/dnsmasq.conf`

* `dnsmasq_dnsmasq_d_files_present`: [default: `{}`]: Declaration of specific configuration files (to add)
* `dnsmasq_dnsmasq_d_files_present.key`: [required]: The name of the configuration file (e.g. `hosts`)
* `dnsmasq_dnsmasq_d_files_present.key.{n}`: [default: `[]`]: List of lines of the configuration file
  
* `dnsmasq_dnsmasq_d_files_absent`: [default: `{}`]: Specific configuration files to remove
* `dnsmasq_dnsmasq_d_files_absent.key`: [required]: The name of the configuration file (e.g. `hosts`)

## Dependencies

None

#### Example

```yaml
---
- hosts: all
  roles:
    - dnsmasq
```

#### Example with configuration (force domain to an IP address)

```yaml
---
- hosts: all
  roles:
    - dnsmasq
  vars:
    dnsmasq_dnsmasq_d_files_present:
      example-com:
        - address=/mail.example.com/192.168.0.8
        - address=/www.example.com/192.168.0.9
```

#### Example with configuration (caching)

```yaml
---
- hosts: all
  pre_tasks:
    - name: create resolv-file for dnsmasq
      copy:
        content: |
          nameserver 8.8.8.8
          nameserver 8.8.4.4
        dest: /etc/resolv.dnsmasq
  roles:
    - ../../
  vars:
    dnsmasq_dnsmasq_conf:
      - |
        port=53
        listen-address={{ ansible_lo['ipv4']['address'] }}
        bind-interfaces
    dnsmasq_dnsmasq_d_files_present:
      cache:
        - |
          domain-needed
          bogus-priv
          no-hosts
          dns-forward-max=150
          cache-size=1000
          neg-ttl=3600
          resolv-file=/etc/resolv.dnsmasq
          no-poll
```

#### License

MIT

#### Author Information

* Mark van Driel
* Mischa ter Smitten

#### Feedback, bug-reports, requests, ...

Are [welcome](https://github.com/Oefenweb/ansible-dnsmasq/issues)!
