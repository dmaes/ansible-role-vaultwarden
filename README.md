# Bitwardenrs

[![Build Status](https://travis-ci.com/dmaes/ansible-role-bitwardenrs.svg?branch=master)](https://travis-ci.com/dmaes/ansible-role-bitwardenrs)

Builds, installs and configures [Bitwarden_RS](https://github.com/dani-garcia/bitwarden_rs) (without Docker).

*Only tested on Debian 10 and CentOS 8*

## Requirements
* Requirements for the [unarchive](https://docs.ansible.com/ansible/latest/modules/unarchive_module.html)-module
* Requirements for the [package](https://docs.ansible.com/ansible/latest/modules/package_module.html)-module
* wget or curl
* Systemd (optional)

## Role Variables
| Variable | Description | Default value |
| --- | --- | --- |
| `bitwardenrs_directory` | Where to install Bitwarden_RS | `/opt/bitwarden_rs` |
| `bitwardenrs_version` | Which version to install | `1.17.0` |
| `bitwardenrs_webvault` | Install the patched webvault | `true` |
| `bitwardenrs_webvault_version` | Version of the webvault to install | `2.16.1` |
| `bitwardenrs_build_backend` | The database-type to compile for | *bitwardenrs_version-specific(\*)* |
| `bitwardenrs_force_recompile` | Force recompile binary, (e.g. you switched backends on same server | `false` |
| `bitwardenrs_config` | Key-value environment variables for the Bitwarden_RS `.env` file | `{ DOMAIN: "https://{{ ansible.fqdn }}/" }` |
| `bitwardenrs_datadir` | Bitwarden_RS data directory (does not configure, only create and used for e.g. keys) | `{{ bitwardenrs_directory }}/data` |
| `bitwardenrs_encryption_key` | RSA key to use for encryption (content, not file), empty string to not copy, Bitwarden_RS should generate one if non-existing | `""` |
| `bitwardenrs_force_encryption_key` | Force changing encryption key if it already exists (DANGEROUS!) | `false` |
| `bitwardenrs_systemd` | Manage systemd service | `{{ ansible_service_mgr == 'systemd' }}` |
*(\*)Starting from `bitwardenrs_version: 1.17.0`: defaults to `sqlite,mysql,postgresql`, before: defaults to `sqlite`*

## Example Playbook
```yaml
- hosts: servers
  roles:
    - dmaes.bitwardenrs
```

## License
MIT
