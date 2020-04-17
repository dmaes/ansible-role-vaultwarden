# Bitwardenrs

Builds, installs and configures [Bitwarden_RS](https://github.com/dani-garcia/bitwarden_rs) (without Docker).

Currently, only sqlite3 backend is supported.
Also, not all configuration can be done via role variables yet.

*Only tested on Debian 10*

## Requirements
* Requirements for the [unarchive](https://docs.ansible.com/ansible/latest/modules/unarchive_module.html)-module
* Requirements for the [package](https://docs.ansible.com/ansible/latest/modules/package_module.html)-module
* Systemd (optional)
* SQLite3

## Role Variables
```yaml
# Role settings
bitwardenrs_configure: yes # Do or do not configure bitwardenrs
bitwardenrs_systemd: yes # Do or do not setup systemd service

# Installation settings
bitwardenrs_directory: /opt/bitwarden_rs # Where to install
bitwardenrs_version: 1.14.1 # Version to install
bitwardenrs_webvault_version: 2.13.2 # Webvault version to install

# Configuration settings (check Bitwarden_RS config file for more information)
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
        bitwardenrs_configure: no
```

## License
GPL-3.0
