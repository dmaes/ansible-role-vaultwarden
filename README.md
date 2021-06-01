# Vaultwarden

[![Build Status](https://travis-ci.com/dmaes/ansible-role-vaultwarden.svg?branch=master)](https://travis-ci.com/dmaes/ansible-role-vaultwarden)

Builds, installs and configures [Vaultwarden](https://github.com/dani-garcia/vaultwarden) (without Docker).

*Only tested on Debian 10 and CentOS 8*

## Requirements
* Requirements for the [unarchive](https://docs.ansible.com/ansible/latest/modules/unarchive_module.html)-module
* Requirements for the [package](https://docs.ansible.com/ansible/latest/modules/package_module.html)-module
* wget or curl
* jinja => v2.11 
* Systemd (optional)

## Role Variables
| Variable | Description | Default value |
| --- | --- | --- |
| `vaultwarden_directory` | Where to install Vaultwarden | `/opt/vaultwarden` |
| `vaultwarden_version` | Which version to install | `1.17.0` |
| `vaultwarden_webvault` | Install the patched webvault | `true` |
| `vaultwarden_webvault_version` | Version of the webvault to install | `2.16.1` |
| `vaultwarden_build_backend` | The database-type to compile for | *vaultwarden_version-specific(\*)* |
| `vaultwarden_force_recompile` | Force recompile binary, (e.g. you switched backends on same server | `false` |
| `vaultwarden_config` | Key-value environment variables for the Vaultwarden `.env` file | `{ DOMAIN: "https://{{ ansible_fqdn }}/" }` |
| `vaultwarden_datadir` | Vaultwarden data directory (does not configure, only create and used for e.g. keys) | `{{ vaultwarden_directory }}/data` |
| `vaultwarden_encryption_key` | RSA key to use for encryption (content, not file), empty string to not copy, Vaultwarden should generate one if non-existing | `""` |
| `vaultwarden_force_encryption_key` | Force changing encryption key if it already exists (DANGEROUS!) | `false` |
| `vaultwarden_systemd` | Manage systemd service | `{{ ansible_service_mgr == 'systemd' }}` |
*(\*)Starting from `vaultwarden_version: 1.17.0`: defaults to `sqlite,mysql,postgresql`, before: defaults to `sqlite`*

## Example Playbook
```yaml
- hosts: servers
  vars:
    vaultwarden_configure: yes
    vaultwarden_domain: https://vaultwarden.example.com/
    vaultwarden_port: "443"
    vaultwarden_build_backend: "sqlite,postgresql"
    admin_token: !vault | 
      $ANSIBLE_VAULT;1.1;AES256
      ...
    vaultwarden_config:
      DOMAIN: "https://example.com/"
      ADMIN_TOKEN: "{{ admin_token }}"
      DATABASE_URL: "postgresql:///vaultwarden?host=/run/postgresql/"
      SIGNUPS_ALLOWED: 'false'
      SIGNUPS_VERIFY: 'true'
      SIGNUPS_DOMAINS_WHITELIST: 'example.com'
      INVITATIONS_ALLOWED: 'true'
      SMTP_HOST: 'mail.example.com'
      SMTP_FROM: 'vaultwarden@example.com'
      SMTP_FROM_NAME: 'vaultwarden'
  roles:
    - dmaes.vaultwarden
```

## License
MIT
