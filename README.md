# php

Role php fully automates control over PHP packages, services and configuration.

## Table of contents

- [Requirements](#requirements)
- [Default Variables](#default-variables)
  - [php_actions](#php_actions)
  - [php_config_owner_group](#php_config_owner_group)
  - [php_config_owner_user](#php_config_owner_user)
  - [php_config_path](#php_config_path)
  - [php_fpm_pools](#php_fpm_pools)
  - [php_fpm_state_action](#php_fpm_state_action)
  - [php_fpm_version](#php_fpm_version)
  - [php_ini_settings](#php_ini_settings)
  - [php_packages](#php_packages)
  - [php_repositories](#php_repositories)
- [Dependencies](#dependencies)
- [License](#license)
- [Author](#author)

---

## Requirements

- Minimum Ansible version: `2.20`

## Default Variables

### php_actions

List of actions the role does, accepts one or more actions.
Use comma without spaces as a delimiter for multiple actions.

**_Required:_** `true`<br />
**_Type:_** String<br />

#### Example usage

```YAML
  php_actions: install
  php_actions: install,deploy_php_config
```

### php_config_owner_group

PHP files group name

**_Type:_** String<br />

#### Default value

```YAML
php_config_owner_group: root
```

### php_config_owner_user

PHP files owner name

**_Type:_** String<br />

#### Default value

```YAML
php_config_owner_user: root
```

### php_config_path

Main PHP configuration directory

**_Type:_** String<br />

#### Default value

```YAML
php_config_path: /etc/php
```

### php_fpm_pools

PHP FPM pool configuration to be applied per version

**_Required:_** `true`, only in case `php_actions: deploy_fpm_pools`<br />
**_Type:_** Dict<br />

#### Example usage

```YAML
php_fpm_pools:
  '8.4':
    pool_1:
      parameter: value
    pool_2:
      parameter: value
  '8.2':
    pool_1:
      parameter: value
```

### php_fpm_state_action

Controls state of PHP FPM process

**_Required:_** `true`, only in case `php_actions: fpm_state_control`<br />
**_Type:_** String<br />

#### Example usage

```YAML
  php_fpm_state_action: restarted
  php_fpm_state_action: stopped
```

### php_fpm_version

PHP FPM version to control

**_Required:_** `true`, only in case `php_actions: fpm_state_control`<br />
**_Type:_** String<br />

#### Example usage

```YAML
  php_fpm_version: 8.4
```

### php_ini_settings

PHP configuration directives to be applied per version and SAPI

**_Required:_** `true`, only in case `php_actions: deploy_php_config`<br />
**_Type:_** Dict<br />

#### Example usage

```YAML
php_ini_settings:
  '8.4':
    fpm:
      PHP:
        post_max_size: 100M
        upload_max_filesize: 100M
```

### php_packages

PHP versions and packages to manage

**_Required:_** `true`, only in case `php_actions: install`<br />
**_Type:_** Dict<br />

#### Example usage

```YAML
php_packages:
  '8.4':
    state: present
    packages:
      - name: fpm
        state: present
      - name: amqp
        state: present
  '8.2':
    state: present
    packages:
      - name: gd
        state: present
      - name: pgsql
        state: present
```

### php_repositories

List of additional PHP apt repositories to add before installing

**_Type:_** List<br />

#### Example usage

```YAML
php_repositories:
  - ppa:ondrej/php
```

## Dependencies

None.

## License

MIT

## Author

freedform
