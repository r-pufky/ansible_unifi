# UniFi
UniFi OS & Legacy service from Ubiquiti release.

## Requirements
[supported platforms](https://github.com/r-pufky/ansible_unifi/blob/main/meta/main.yml)

## Role Variables
[defaults](https://github.com/r-pufky/ansible_unifi/tree/main/defaults/main)

### Ports
All ports and protocols have been defined for the role.

[defaults/ports.yml](https://github.com/r-pufky/ansible_unifi/blob/main/defaults/main/ports.yml)

## Dependencies
**galaxy-ng** roles cannot be used independently. Part of
[r_pufky.srv](https://github.com/r-pufky/ansible_collection_srv) collection.

## Example Playbook
Read defaults documentation. Highly recommend installing UniFi OS.

Install UniFi OS and add specific users to CLI `uosserver` command.

``` yaml
- name: 'UniFi server'
  hosts: 'unifi.example.com'
  become: true
  roles:
     - 'r_pufky.srv.unifi'
  vars:
    unifi_cfg_os_uosserver_users:
      - user: 'test'
      - user: 'remove_user_access_user'
        state: 'absent'
```

Install UniFi Legacy (Network Server / Controller).

``` yaml
- name: 'UniFi server'
  hosts: 'unifi.example.com'
  become: true
  roles:
     - 'r_pufky.srv.unifi'
  vars:
    unifi_srv_legacy_enable: true
    unifi_srv_os_enable: false
```

## Troubleshooting

### UniFi OS: unifi.server failed to connect stdout to journal socket
UniFi OS container is auto configured from host settings on first start.

Set a valid network configuration with default routes.

#### Reinstall UniFi OS container:
``` bash
ansible-playbook site.yml --tags unifi -e '{"unifi_cfg_os_purge_enable": true}'
```

### Adopted device lost (inform to Network Server failed)
Network Server IP changed.

#### Update inform address for device:
``` bash
ssh {USER}@{DEVICE}
set-inform http://{SERVER}:8080/inform
```

## Development
Configure [environment](https://github.com/r-pufky/ansible_collection_docs/blob/main/ansible/environment.md)

Run all unit tests:
``` bash
molecule test --all
```

### Releases
Release format: **{OS}-{APP_OS}-{LEGACY}-{ROLE}**

Each type inherits the versioning system used; defaulting to schematic
versioning.

`12.0.0-4.3.6-9.4.19-1.0.0`

* 12.0.0 - Debian 12 (bookworm).
* 4.3.6 - UniFi OS version.
* 9.4.19 - UniFi Legacy version.
* 1.0.0 - Role version.

Releases are branched on Debian releases:

* **[13.x.x](https://github.com/r-pufky/ansible_unifi)**: 13 Trixie.
* **[12.x.x](https://github.com/r-pufky/ansible_unifi/tree/12.x)**: 12 Bookworm.

## Issues
Create a bug and provide as much information as possible.

Associate pull requests with a submitted bug.

## License
[AGPL-3.0 License](https://www.tldrlegal.com/license/gnu-affero-general-public-license-v3-agpl-3-0)
 [(direct link)](https://github.com/r-pufky/ansible_unifi/blob/main/LICENSE)

## Author Information
PGP Fingerprint: [466EEC2B67516C7117C85CE3A0BC35D16698BAB9](https://keys.openpgp.org/vks/v1/by-fingerprint/466EEC2B67516C7117C85CE3A0BC35D16698BAB9)
| [github gist](https://gist.github.com/r-pufky/a8df36977c55b5bb20829267c4c49d22)
