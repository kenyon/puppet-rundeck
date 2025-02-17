# Rundeck module for Puppet

[![Build Status](https://github.com/voxpupuli/puppet-rundeck/workflows/CI/badge.svg)](https://github.com/voxpupuli/puppet-rundeck/actions?query=workflow%3ACI)
[![Code Coverage](https://coveralls.io/repos/github/voxpupuli/puppet-rundeck/badge.svg?branch=master)](https://coveralls.io/github/voxpupuli/puppet-rundeck)
[![Puppet Forge](https://img.shields.io/puppetforge/v/puppet/rundeck.svg)](https://forge.puppetlabs.com/puppet/rundeck)
[![Puppet Forge - downloads](https://img.shields.io/puppetforge/dt/puppet/rundeck.svg)](https://forge.puppetlabs.com/puppet/rundeck)
[![Puppet Forge - endorsement](https://img.shields.io/puppetforge/e/puppet/rundeck.svg)](https://forge.puppetlabs.com/puppet/rundeck)
[![Puppet Forge - scores](https://img.shields.io/puppetforge/f/puppet/rundeck.svg)](https://forge.puppetlabs.com/puppet/rundeck)

## Table of Contents

1. [Overview](#overview)
2. [Module Description - What the module does and why it is useful](#module-description)
3. [Setup - Requirements and beginning with rundeck](#setup)
4. [Usage - Configuration options and additional functionality](#usage)
5. [Reference - Module references](#reference)
6. [Limitations - OS compatibility, etc.](#limitations)
7. [Development - Guide for contributing to the module](#development)

## Overview

The rundeck puppet module for installing and managing [Rundeck](http://rundeck.org/)

### Supported Versions of Rundeck

| Rundeck Version  | Rundeck Puppet module versions |
| ---------------- | -------------------------------|
| 2.x   - 3.0.X    | v5.4.0 and older               |
| 3.1.x - 3.3.x    | v8.0.1 until v6.0.0            |
| 3.4.x - up       | v9.0.0 and newer               |

## Module Description

This module provides a way to manage the installation and configuration of rundeck and plugins.

## Setup

### Requirements

You need a compatible version of Java installed.
You can use [puppetlabs/java](https://github.com/puppetlabs/puppetlabs-java) module if there isn't already a suitable version.

On systems that use apt, there's a soft dependency on the [puppetlabs/apt](https://github.com/puppetlabs/puppetlabs-apt) module.

### Beginning with rundeck

To install a server with the default options:

```puppet
include rundeck
```

## Usage

### Configure rundeck to connect to a MySQL database

To use an external MySQL database, the `database_config` hash must be set to
override the default values which result in a local file based storage.  To
enable `key` and `project` storage in the database, you must also set the two
associated parameters.

```puppet
class { 'rundeck':
  key_storage_config => [
    {
      'type' => 'db',
      'path' => 'keys',
    },
  ],
  database_config    => {
    'url'             => 'jdbc:mysql://myserver/rundeck',
    'username'        => 'rundeck',
    'password'        => 'verysecure',
    'driverClassName' => 'com.mysql.jdbc.Driver',
  },
}
```

### Configure SSL for rundeck

```Puppet
class { 'rundeck':
  ssl_enabled       => true,
  ssl_certificate   => '/path/to/cert',
  ssl_private_key   => '/path/to/key',
}
```

### Configure HashiCorp vault as keystorage

An additional [Rundeck Vault plugin](https://github.com/rundeck-plugins/vault-storage/) is required.

```Puppet
class { 'rundeck':
  key_storage_config => [
    {
      'type'   => 'vault-storage',
      'path'   => 'keys',
      'config' => {
        'prefix'           => 'rundeck',
        'address'          => 'https://vault.example.com',
        'storageBehaviour' => 'vault',
        'secretBackend'    => 'rundeck',
        'engineVersion'    => '2',
        'authBackend'      => 'approle',
        'approleAuthMount' => 'approle',
        'approleId'        => 'xxx-xxx-xxx-xxx-xxx',
        'approleSecretId'  => 'xxx-xxx-xxx-xxx-xxx',
      },
    },
  ],
}
```

### Configure multiple keystorage types

```Puppet
class { 'rundeck':
  key_storage_config => [
    {
      'type'   => 'file',
      'path'   => 'keys',
      'config' => {
        'baseDir => '/path/to/dir',
      },
    },
    {
      'type' => 'db',
      'path' => 'keys/database',
    },
  ],
}
```

### Configure shared authentication credentials

To perform LDAP authentication and file authorization following code can be used.

```puppet
class { 'rundeck':
  auth_config => {
    'file' => {
      'auth_flag'    => 'sufficient',
      'jaas_config'  => {
        'file' => '/etc/rundeck/realm.properties',
      },
      'realm_config' => {
        'admin_user'     => 'admin',
        'admin_password' => 'admin',
        'auth_users'     => [
          {
            'username' => 'testuser',
            'password' => 'password',
            'roles' => %w[user deploy]
          },
          {
            'username' => 'anotheruser',
            'password' => 'anotherpassword',
            'roles' => ['user']
          },
        ],
      },
    },
    'ldap' => {
      'jaas_config' => {
        'debug' => 'true',
        'providerUrl' => 'ldap://server:389',
        'bindDn' => 'cn=Manager,dc=example,dc=com',
        'bindPassword' => 'secret',
        'authenticationMethod' => 'simple',
        'forceBindingLogin' => 'false',
        'userBaseDn' => 'ou=users,ou=accounts,ou=corp,dc=xyz,dc=com',
        'userRdnAttribute' => 'sAMAccountName',
        'userIdAttribute' => 'sAMAccountName',
        'userPasswordAttribute' => 'unicodePwd',
        'userObjectClass' => 'user',
        'roleBaseDn' => 'ou=role based,ou=security,ou=groups,ou=test,dc=xyz,dc=com',
        'roleNameAttribute' => 'cn',
        'roleMemberAttribute' => 'member',
        'roleObjectClass' => 'group',
        'nestedGroups' => 'true'
      },
    },
  },
}
```

## Reference

See [REFERENCE.md](https://github.com/voxpupuli/puppet-rundeck/blob/master/REFERENCE.md)

## Limitations

This module is tested on the following platforms:

- CentOS 6
- CentOS 7
- Debian 8
- RedHat 8
- Ubuntu 16.04

It is tested with the OSS version of Puppet only.

## Development

### Contributing

This module is maintained by [Vox Pupuli](https://voxpupuli.org/). Vox Pupuli
welcomes new contributions to this module, especially those that include
documentation and rspec tests. We are happy to provide guidance if necessary.

Please see [CONTRIBUTING](.github/CONTRIBUTING.md) for more details.
