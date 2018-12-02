# icingaweb2

This role installs and configures an Icingaweb 2 installation with PostgreSQL (both for the Icingaweb 2 database and for the IDO).
Icinga 2 will not be installed.

## Requirements

Debian or Ubuntu with a [web server](https://github.com/stuvusIT/nginx) and [PHP](https://github.com/stuvusIT/php-fpm).

## Role Variables

| Name                                   | Default/Required                | Description                                                                                                 |
|----------------------------------------|:-------------------------------:|-------------------------------------------------------------------------------------------------------------|
| `icingaweb2_unix_group`                | `www-data`                      | Unix group under which your webserver and PHP run (used for file ownership)                                 |
| `icingaweb2_module_path`               | `/usr/share/icingaweb2/modules` | Search path for Icingaweb 2 modules                                                                         |
| `icingaweb2_modules`                   | `[ doc, monitoring ]`           | Icingaweb 2 modules to enable                                                                               |
| `icingaweb2_modules_to_clone`          | `{}`                            | Name-URL dict of modules to clone and automatically enable                                                  |
| `icingaweb2_show_stacktraces`          | `false`                         | Show stacktraces in the UI                                                                                  |
| `icingaweb2_config_backend`            | `ini`                           | Backend to use for user configurations                                                                      |
| `icingaweb2_config_resource`           | (:heavy_check_mark:)            | (Only for db config backend) Database resource to use for user configurations                               |
| `icingaweb2_module_path`               | `/usr/share/icingaweb2/modules` | Search path for Icingaweb 2 modules                                                                         |
| `icingaweb2_log`                       | `syslog`                        | Log target to use                                                                                           |
| `icingaweb2_log_level`                 | `WARNING`                       | Minimum log level to log                                                                                    |
| `icingaweb2_log_file`                  | (:heavy_check_mark:)            | (Only for file log) File path to log to                                                                     |
| `icingaweb2_log_application`           | `icingaweb2`                    | Syslog application to log under                                                                             |
| `icingaweb2_log_facility`              | `user`                          | Syslog facility to log under                                                                                |
| `icingaweb2_theme`                     | `Icinga`                        | Default theme for the Web UI                                                                                |
| `icingaweb2_theme_disabled`            | `false`                         | Prevent users from changing the theme in the Web UI                                                         |
| `icingaweb2_default_domain`            |                                 | Default domain for login                                                                                    |
| `icingaweb2_resources`                 | `[ ]`                           | List of resource configurations (see below)                                                                 |
| `icingaweb2_authentications`           | `[ ]`                           | List of authentications (see below)                                                                         |
| `icingaweb2_roles`                     | `[ ]`                           | List of roles (see below)                                                                                   |
| `icingaweb2_group_configs`             | `[ ]`                           | List of group configurations (see below)                                                                    |
| `icingaweb2_monitoring_backends`       | `[ ]`                           | List of monitoring backends (see below)                                                                     |
| `icingaweb2_monitoring_transports`     | `[ ]`                           | List of command transports (see below)                                                                      |
| `icingaweb2_monitoring_protected_vars` | `[ ]`                           | List of protected variables (will not be shown in the UI)                                                   |
| `icingaweb2_configure_postgres`        | `true`                          | Also configure the PostgreSQL databases (Create user and DB, import schema, optionally grant IDO privileges |
| `icingaweb2_postgres_grant_ido`        | `true`                          | Grant read privileges to the PostgreSQL IDO database                                                        |
| `icingaweb2_postgres_login_host`       | `localhost`                     | PostgreSQL host to connect to for configuring PostgreSQL                                                    |
| `icingaweb2_postgres_login_user`       | `localhost`                     | PostgreSQL user to connect to for configuring PostgreSQL                                                    |
| `icingaweb2_postgres_login_password`   |                                 | PostgreSQL password to connect to for configuring PostgreSQL                                                |
| `icingaweb2_postgres_user`             | `icingaweb2`                    | PostgreSQL user for Icingaweb 2                                                                             |
| `icingaweb2_postgres_database`         | `icingaweb2`                    | PostgreSQL database for Icingaweb 2                                                                         |
| `icingaweb2_postgres_ido_name`         | `icinga2`                       | Name of the IDO database                                                                                    |

### Resources

Each resource consists of:

| Name          | Default/Required     | Description                                                             |
|---------------|:--------------------:|-------------------------------------------------------------------------|
| `name`        | :heavy_check_mark:   | Name of the resource                                                    |
| `type`        | :heavy_check_mark:   | Type of the resource                                                    |
| `db`          | (:heavy_check_mark:) | (Only for db) Database system of the resource                           |
| `host`        | (:heavy_check_mark:) | (Only for db and ldap) Database host to connect to                      |
| `port`        | (:heavy_check_mark:) | (Only for db and ldap) Database port to connect to                      |
| `username`    | (:heavy_check_mark:) | (Only for db and ssh) User to connect with                              |
| `password`    | (:heavy_check_mark:) | (Only for db) Database password to connect with                         |
| `dbname`      | (:heavy_check_mark:) | (Only for db) Database name to connect to                               |
| `persistent`  | `false`              | (Only for db) Use persistent connections                                |
| `charset`     |                      | (Only for db) Charset of the database                                   |
| `ssl_cert`    |                      | (Only for db mysql) Public SSL certificate to connect with              |
| `ssl_key`     |                      | (Only for db mysql) Private SSL key to connect with                     |
| `ssl_ca`      |                      | (Only for db mysql) Path to the CA certificate of the MySQL server      |
| `ssl_capath`  |                      | (Only for db mysql) Directory that is searched for CA certificate files |
| `ssl_cipher`  |                      | (Only for db mysql) Ciphers to use for MySQL SSL connection             |
| `root_dn`     | (:heavy_check_mark:) | (Only for ldap) Base DN of the LDAP tree                                |
| `bind_dn`     |                      | (Only for ldap) DN to connect with                                      |
| `bind_pw`     |                      | (Only for ldap) Password of the DN to connect with                      |
| `encryption`  |                      | (Only for ldap) Encryption type to use for the connection               |
| `private_key` |                      | (Only for ssh) Path to the private key to connect with                  |
| `filename`    | (:heavy_check_mark:) | (Only for file) Path to the file to read                                |
| `fields`      | (:heavy_check_mark:) | (Only for file) Field separator in the file                             |
| `socket`      | (:heavy_check_mark:) | (Only for livestatus) Path of the livestatus socket                     |

### Roles

Each role configuration consists of:

| Name             | Default/Required   | Description                                                 |
|------------------|:------------------:|-------------------------------------------------------------|
| `name`           | :heavy_check_mark: | Name of the role                                            |
| `users`          | `[ ]`              | Users to add to the role                                    |
| `groups`         | `[ ]`              | Groups to add to the role                                   |
| `permissions`    | `[ ] `             | Permissions to grant to the role                            |
| `share_users`    | `[ ]`              | Users this role may share dashboards with (none means all)  |
| `share_groups`   | `[ ]`              | Groups this role may share dashboards with (none means all) |
| `object_filter`  |                    | Filter for the objects this role can see                    |
| `prop_blacklist` |                    | List of attributes this role may not see                    |

### Authentications

Each authentication consists of:

| Name                    | Default/Required     | Description                                                   |
|-------------------------|:--------------------:|---------------------------------------------------------------|
| `name`                  | :heavy_check_mark:   | Name of the authentication                                    |
| `backend`               | :heavy_check_mark    | Authentication backend to use                                 |
| `domain`                |                      | Domain of the authentication                                  |
| `strip_username_regexp` |                      | (Only for external) Regexp to strip the username with         |
| `resource`              | (:heavy_check_mark:) | (Only for db, ldap and msldap) Authentication resource to use |
| `user_class`            |                      | (Only for ldap and msldap) Object class of users              |
| `user_name_attribute`   |                      | (Only for ldap and msldap) LDAP attribute for usernames       |
| `filter`                |                      | (Only for ldap and msldap) LDAP filter                        |

### Groups

Each group configuration consists of:

| Name                     | Default/Required   | Description                                                              |
|--------------------------|:------------------:|--------------------------------------------------------------------------|
| `name`                   | :heavy_check_mark: | Name of the group configuration                                          |
| `resource`               | :heavy_check_mark: | Name of the resource for the group                                       |
| `user_class`             |                    | (Only for ldap and msldap) Object class for users                        |
| `user_name_attribute`    |                    | (Only for ldap and msldap) LDAP attribute for usernames                  |
| `group_class`            |                    | (Only for ldap and msldap) Object class for groups                       |
| `group_name_attribute`   |                    | (Only for ldap and msldap) LDAP attribute for group names                |
| `group_member_attribute` |                    | (Only for ldap and msldap) LDAP attribute for user membership in a group |
| `group_filter`           |                    | (Only for ldap and msldap) LDAP filter for group search                  |
| `nested_group_search`    | `false`            | (Only for ldap and msldap) Also try to query nested groups               |

### Monitoring backends

Each monitoring backend consists of:

| Name         | Default/Required   | Description                      |
|--------------|:------------------:|----------------------------------|
| `resource`   | :heavy_check_mark: | Name of the resource for the IDO |
| `user_class` | `false`            | Whether the backend is disabled  |

### Monitoring command transports

Each command transport consists of:

| Name        | Default/Required     | Description                                |
|-------------|:--------------------:|--------------------------------------------|
| `transport` | `local`              | Type of this transport                     |
| `path`      | :heavy_check_mark:   | Path to the command socket                 |
| `host`      | (:heavy_check_mark:) | (Only for remote) SSH host to connect to   |
| `port`      | `22`                 | (Only for remote) SSH port to connect to   |
| `user`      | (:heavy_check_mark:) | (Only for remote) Username to connect with |

## Example Playbook

```yml
- hosts: icinga
  roles:
  - icingaweb2
     icingaweb2_resources:
       - name: icingaweb_db
         type: db
         db: pgsql
         host: 127.0.0.1
         port: 5432
         dbname: icingaweb2
         username: icingaweb2
         password: secret
         charset: UTF-8
       - name: ido
         type: pgsql
         [...]

     icingaweb2_authentications:
       - name: db
         backend: db
         resource: icingaweb_db

     icingaweb2_group_configs:
       - name: db
         backend: db
         resource: icingaweb_db

     icingaweb2_roles:
       - name: Icinga Administrators
         groups:
           - admins
         permissions:
           - "*"

     icingaweb2_monitoring_backends:
       - name: icinga
         resource: ido

     icingaweb2_monitoring_transports:
       - name: localpipe
         path: /var/run/icinga2/cmd/icinga2.cmd

     icingaweb2_modules_to_clone:
       spring: https://github.com/Mikesch-mp/icingaweb2-theme-spring
```

## License

This work is licensed under a [Creative Commons Attribution-ShareAlike 4.0 International License](https://creativecommons.org/licenses/by-sa/4.0/).

## Author Information

- [Janne Heß](https://github.com/dasJ)
