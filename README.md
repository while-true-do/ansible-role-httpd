[![Build Status](https://travis-ci.org/while-true-do/ansible-role-httpd.svg?branch=master)](https://travis-ci.org/while-true-do/ansible-role-httpd)

# Ansible Role: httpd
| A role to install and configure [Apache HTTP Server](https://httpd.apache.org/).

This role can provide (in its default settings) a Webserver, which delivers the content of `/var/www/html`. Nevertheless, it should be best practice to have a separate VirtualHost Configuration located in `/etc/httpd/conf.d/`. 

This role can:

- Configure some Modules
- Enabling some Best Practices for a Webserver
- Setting some well known security parameter
- Install mod_ssl and mod_security

## Motivation

[Apache HTTP Server](https://httpd.apache.org/) is used for multiple websites. It is the approach to provide a secure, efficient and extensible server that provides HTTP services in sync with the current HTTP standards.

## Installation

Install from [Ansible Galaxy](https://galaxy.ansible.com/while-true-do/httpd)

```
ansible-galaxy install while-true-do.httpd
```

Install from [Github](https://github.com/while-true-do/ansible-role-httpd)

```
git clone https://github.com/while-true-do/ansible-role-httpd.git while-true-do.httpd
```

## Requirements

Used Modules:

-   [module1](link)
-   [module2](link)

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
wtd_httpd_httpd_conf_ServerName: "{{ inventory_hostname }}"
wtd_httpd_httpd_conf_ServerAdmin: "root@localhost"
wtd_httpd_httpd_conf_ServerRoot: "/etc/httpd"
wtd_httpd_httpd_conf_User: "apache"
wtd_httpd_httpd_conf_Group: "apache"
wtd_httpd_httpd_conf_PidFile: "run/httpd.pid"

wtd_httpd_httpd_conf_ServerTokens: "prod"
wtd_httpd_httpd_conf_ServerSignature: "off"
wtd_httpd_httpd_conf_UseCanonicalName: "on"
wtd_httpd_httpd_conf_AddDefaultCharset: "UTF-8"
wtd_httpd_httpd_conf_TraceEnable: "Off"

wtd_httpd_httpd_conf_Listen: "127.0.0.1:80"

wtd_httpd_httpd_conf_Timeout: "20"
wtd_httpd_httpd_conf_MaxRequestWorkers: "100"

wtd_httpd_httpd_conf_ModulesPath: "conf.modules.d/*.conf"

wtd_httpd_httpd_conf_ErrorLog: "logs/error.log"
wtd_httpd_httpd_conf_LogLevel: "warn"
wtd_httpd_httpd_conf_LogFormatCombined: '"%h %l %u %t \"%r\" %>s %b \"%{Referer}i\" \"%{User-Agent}i\"" combined'
wtd_httpd_httpd_conf_LogFormatCommon: '"%h %l %u %t \"%r\" %>s %b" common'
wtd_httpd_httpd_conf_AccessLog: "logs/access.log combined"

wtd_httpd_httpd_conf_DocumentRoot: "/var/www/html"

wtd_httpd_httpd_conf_ConfigPath: "conf.d/*.conf"

# Configure Default Modules
## Built-in Modules
## https://httpd.apache.org/docs/2.4/mod/mod_cache.html
wtd_httpd_mod_cache: True
wtd_httpd_mod_autoindex: False
wtd_httpd_mod_include: False
wtd_httpd_mod_info: False

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
    - { role: while-true-do.httpd }
```

Advanced Example:

You can enable the server to listen on all addresses and provide a welcome page this way.

```yaml
- hosts: servers 
  roles:
    - { role: while-true-do.httpd, wtd_httpd_httpd_conf_listen: "*:80", wtd_httpd_welcome_page: True }
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

Blog: [blog.while-true-do.org](https://blog.while-true-do.org)

Mail: [hello@while-true-do.org](mailto:hello@while-true-do.org)
