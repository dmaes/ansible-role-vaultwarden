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
# Admin settings
## Sets the admin token
bitwardenrs_admin_token: ''
## Disables admin token (unsafe, use with external protection (e.g. BasicAuth))
bitwardenrs_admin_token_disabled: no

# Directory to install
bitwardenrs_directory: /opt/bitwarden_rs

# Port to run on
bitwardenrs_port: 8000

# Sign-up settings
## Enable sign-up
bitwardenrs_signup: yes
## Limit sign-up to list of domains (ignores public sign-up setting)
bitwardenrs_signup_domains: []

# SMTP settings
## Enable SMTP
bitwardenrs_smtp: no
## SMTP server
bitwardenrs_smtp_host: "{{ bitwardenrs_domain }}"
## Mail from this address
bitwardenrs_smtp_from: "bitwarden-rs@{{ bitwardenrs_domain }}"
## Mail with this name
bitwardenrs_smtp_from_name: Bitwarden_RS
## SMTP server port
bitwardenrs_smtp_port: 587
## Use SSL for SMTP
bitwardenrs_smtp_ssl: yes
## SMTP auth username
bitwardenrs_smtp_username: ''
## SMTP auth password (plain-text)
bitwardenrs_smtp_password: ''

# Version settings
## Version to install
bitwardenrs_version: 1.14.1
## Webvault version to install
bitwardenrs_webvault_version: 2.13.2
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
