## dnsmasq

[![Build Status](https://travis-ci.org/Oefenweb/ansible-dnsmasq.svg?branch=master)](https://travis-ci.org/Oefenweb/ansible-dnsmasq) [![Ansible Galaxy](http://img.shields.io/badge/ansible--galaxy-dnsmasq-blue.svg)](https://galaxy.ansible.com/Oefenweb/dnsmasq/)

Set up [Dnsmasq](http://www.thekelleys.org.uk/dnsmasq/doc.html) in Debian-like systems.

#### Requirements

None

#### Variables

 * `dnsmasq_port`: [optional]: Listen on this specific port instead of the standard DNS port (53).

 * `dnsmasq_dnsmasqd_present`: [default: `{}`]: Declaration of specific configuration files
 * `dnsmasq_dnsmasqd_present.key`: [required]: The name of the configuration file (e.g. `hosts`)
 * `dnsmasq_dnsmasqd_present.key.{n}`: [default: `[]`]: List of lines of the configuration file
  
 * `dnsmasq_dnsmasqd_absent`: [default: `{}`]: Specific configuration files to remove
 * `dnsmasq_dnsmasqd_absent.key`: [required]: The name of the configuration file (e.g. `hosts`)

## Dependencies

None

#### Example

```yaml
---
- hosts: all
  roles:
    - dnsmasq
```

#### Example with configuration

```yaml
---
- hosts: all
  roles:
    - dnsmasq
  vars:
    dnsmasq_dnsmasqd_present:
      example-com:
        - address=/mail.example.com/192.168.0.8
        - address=/www.example.com/192.168.0.9
```

#### License

MIT

#### Author Information

* Mark van Driel
* Mischa ter Smitten

#### Feedback, bug-reports, requests, ...

Are [welcome](https://github.com/Oefenweb/ansible-dnsmasq/issues)!
