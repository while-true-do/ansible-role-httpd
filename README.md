[![Build Status](https://travis-ci.org/while-true-do/ansible-role-httpd.svg?branch=master)](https://travis-ci.org/while-true-do/ansible-role-httpd)

# Ansible Role: httpd
| A role to install and configure [Apache HTTP Server](https://httpd.apache.org/).

This role can provide (in its default settings) a Webserver, which delivers the content of `/var/www/html`. Nevertheless, it should be best practice to have a separate VirtualHost Configuration located in `/etc/httpd/conf.d/`. 

This role can:

- Enabling some a minimal configuration like https://wiki.apache.org/httpd/Minimal_Config
- Setting some well known security parameter
- Install mod_ssl and mod_security

SSL configuration is derived from:

- https://cipherli.st/
- https://wiki.mozilla.org/Security/TLS_Configurations#Apache

## Motivation

[Apache HTTP Server](https://httpd.apache.org/) is used for multiple websites. It is the approach to provide a secure, efficient and extensible server that provides HTTP services in sync with the current HTTP standards.

## Installation

Install from [Ansible Galaxy](https://galaxy.ansible.com/while_true_do/httpd)

```
ansible-galaxy install while_true_do.httpd
```

Install from [Github](https://github.com/while-true-do/ansible-role-httpd)

```
git clone https://github.com/while-true-do/ansible-role-httpd.git while_true_do.httpd
```

## Requirements

Used Modules:

-  [service_module](http://docs.ansible.com/ansible/latest/service_module.html)
-  [template_module](http://docs.ansible.com/ansible/latest/template_module.html)
-  [package_module](http://docs.ansible.com/ansible/latest/package_module.html)
-  [include_tasks_module](https://docs.ansible.com/ansible/latest/include_tasks_module.html)

## Dependencies

None.

## Role Variables

```yaml
# defaults/main.yml for httpd
#
# You can set the state to ["present"|"absent"|"latest"]
wtd_httpd_state: "present"
wtd_httpd_packages: "httpd"

# Special Pages
wtd_httpd_welcome_page: False
wtd_httpd_autoindex_page: False
wtd_httpd_userdir_page: False
wtd_httpd_userdir_path: "public_html"

# Configure httpd Configs
## https://httpd.apache.org/docs/2.4/configuring.html
wtd_httpd_ServerRoot: "/etc/httpd"
wtd_httpd_User: "apache"
wtd_httpd_Group: "apache"
wtd_httpd_PidFile: "run/httpd.pid"

wtd_httpd_ServerTokens: "prod"
wtd_httpd_ServerSignature: "off"
wtd_httpd_UseCanonicalName: "on"

wtd_httpd_Listen: "80"

wtd_httpd_Timeout: "20"
wtd_httpd_MaxRequestWorkers: "100"

wtd_httpd_ModulesPath: "conf.modules.d/*.conf"

wtd_httpd_ErrorLog: "logs/error.log"
wtd_httpd_LogLevel: "warn"

wtd_httpd_ConfigPath: "conf.d/*.conf"

# Install / Configure Additional Modules
## http://www.modssl.org/
wtd_httpd_mod_ssl_state: "present"
wtd_httpd_mod_ssl_packages: "mod_ssl"

## https://modsecurity.org/
wtd_httpd_mod_security_state: "present"
wtd_httpd_mod_security_packages: "mod_security"
```

## Example Playbook

Simple Example:

```yaml
- hosts: servers
  roles:
    - { role: while_true_do.httpd }
```

Advanced Example:

You can enable the server to listen on all addresses and provide a welcome page this way.

```yaml
- hosts: servers
  roles:
    - { role: while_true_do.httpd, wtd_httpd_listen: "*:80", wtd_httpd_welcome_page: True }
```

## Testing

All tests are located in [test directory](./tests/).

Basic testing:

```
bash ./tests/test-spelling.sh
bash ./tests/test-ansible.sh
```

## Contribute / Bugs

Thank you so much for considering to contribute. Every contribution helps us.
We are really happy, when somebody is joining the hard work. Please have a look
at the links first.

-   [Code of Conduct](./docs/CODE_OF_CONDUCT.md)
-   [Contribution Guidelines](./docs/CONTRIBUTING.md)
-   [Create an issue or Request](https://github.com/while-true-do/ansible-role-httpd/issues)
-   [See who was contributing already](https://github.com/while-true-do/ansible-role-httpd/graphs/contributors)

## License

This work is licensed under a [BSD License](https://opensource.org/licenses/BSD-3-Clause).

## Author Information

Site: [while-true-do.org](https://while-true-do.org)

Mail: [hello@while-true-do.org](mailto:hello@while-true-do.org)
