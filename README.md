# Bitwardenrs

[![Build Status](https://travis-ci.com/dmaes/ansible-role-bitwardenrs.svg?branch=master)](https://travis-ci.com/dmaes/ansible-role-bitwardenrs)

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
### Installation settings
| Variable | Description | Default value |
| --- | --- | --- |
| `bitwardenrs_directory` | Where to install Bitwarden_RS | `/opt/bitwarden_rs` |
| `bitwardenrs_version` | Which version to install | `1.41.2` |
| `bitwardenrs_systemd` | Setup systemd service | `true` |
| `bitwardenrs_webvault` | Install the patched webvault | `true` |
| `bitwardenrs_webvault_version` | Version of the webvault to install | `2.13.2b` |

### Configuration settings
#### Configuration template
A configuration template can be specified.
This file will be templated using Ansible's `template` module.
When set, configuration by variables will be skipped.
```yaml
bitwardenrs_config_template: ''
```

#### Configuration variables
If a template is not defined, Bitwarden_RS can be configured using the following available variables:<br>

***General settings***
| Variable | Description | Default value |
| --- | --- | --- |
| `bitwardenrs_configure` | Create configuration file using variables | `true` |
| `bitwardenrs_domain` | The domain that Bitwarden_RS will be accessed on | `https://{{ ansible_fqdn }}/` |
| `bitwardenrs_port` | Port for Bitwarden_RS to listen on | `8000` |

***Admin settings***
| Variable | Description | Default value |
| --- | --- | --- |
| `bitwardenrs_admin_token` | Admin token required to access the admin interface | `''`
| `bitwardenrs_admin_token_disable` | Disable admin token (use with caution and external auth) | `false` |

***Sign-up settings***
| Variable | Description | Default value |
| --- | --- | --- |
| `bitwardenrs_signup` | Allow public sign-up | `true` |
| `bitwardenrs_signup_domains` | Allow sign-up using an email-address from these domains, even if public sign-up is disabled | `[]` |

***SMTP settings***
| Variable | Description | Default value |
| --- | --- | --- |
| `bitwardenrs_smtp` | Configure SMTP settings (ignore all others when disabled) | `false` |
| `bitwardenrs_smtp_host ` | The SMTP host to connect with | `{{ bitwardenrs_domain|urlsplit('hostname') }}` |
| `bitwardenrs_smtp_from ` | The SMTP From-address | `bitwarden-rs@{{ bitwardenrs_domain|urlsplit('hostname') }}` |
| `bitwardenrs_smtp_from_name ` | The SMTP From-name| `Bitwarden_RS` |
| `bitwardenrs_smtp_port ` | The SMTP port to connect to | `587` |
| `bitwardenrs_smtp_ssl ` | Use SSL when connecting to the SMTP server | `true` |
| `bitwardenrs_smtp_username ` | The username used to authenticate with the SMTP server | `''` |
| `bitwardenrs_smtp_password ` | The password used to authenticate with the SMTP server| `''` |

## Example Playbook
```yaml
- hosts: servers
  vars:
    bitwardenrs_configure: no
  roles:
    - dmaes.bitwardenrs
```

## License
MIT
