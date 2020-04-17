# Bitwardenrs

Builds, installs and configures [Bitwarden_RS](https://github.com/dani-garcia/bitwarden_rs) (without Docker).

Currently, only sqlite3 backend is supported.
Also, not all configuration can be done via role variables yet.

*Only tested on Debian 10*

## Requirements
* Requirements for the [unarchive](https://docs.ansible.com/ansible/latest/modules/unarchive_module.html)-module
* Requirements for the [package](https://docs.ansible.com/ansible/latest/modules/package_module.html)-module
* Systemd (option to disable will be added in the future)
* SQLite3

## Role Variables
```yaml
# Role settings
bitwardenrs_systemd: yes

# Installation settings
bitwardenrs_directory: /opt/bitwarden_rs
bitwardenrs_version: 1.14.1
bitwardenrs_webvault_version: 2.13.2

# Configuration settings
bitwardenrs_admin_token: ''
bitwardenrs_admin_token_disabled: no
bitwardenrs_port: 8000
bitwardenrs_signup: yes
bitwardenrs_signup_domains: []
bitwardenrs_smtp: no
bitwardenrs_smtp_host: "{{ bitwardenrs_domain }}"
bitwardenrs_smtp_from: "bitwarden-rs@{{ bitwardenrs_domain }}"
bitwardenrs_smtp_from_name: Bitwarden_RS
bitwardenrs_smtp_port: 587
bitwardenrs_smtp_ssl: yes
bitwardenrs_smtp_username: ''
bitwardenrs_smtp_password: ''
```

## Example Playbook
```yaml
- hosts: servers
  roles:
      - role: dmaes.bitwardenrs
        bitwardenrs_signup: no
```

## License
GPL-3.0
