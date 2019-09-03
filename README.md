# puppet-orcus

## Overview

manages Orcus - Orchestrator to Consul synchronization tool


## Description

This module installs and configures the
[orcus](https://github.com/MaxFedotov/orcus) package.

## Setup Requirements

This module requires [toml](https://github.com/jm/toml) gem, which is used to translate Hash configuration to Orcus TOML format configuration file.
To install it you need to execute following command on your puppetmaster server:

```bash
sudo puppetserver gem install toml
```

## Usage

```puppet
class { 'orcus':
  override_config => {
    general      => {
      listen_address  => '127.0.0.1:3008',
      log_file        => '/var/log/orcus/orcus.log',
      log_level       => 'info',
      sync_interval   => '10m',
      ssl_skip_verify => true,
      http_timeout    => '5s',
      threads         => 5,
      cache_ttl       => '24h'
    },
    orchestrator => {
      url                      => 'http://localhost:3000',
      force_sync_delay         => '5s',
      submit_masters_to_consul => true,
    },
    consul       => {
      address        => '127.0.0.1:8500',
      acl_token      => '',
      kv_prefix      => 'db/mysql',
      lock_ttl       => '1m',
      retry_interval => '5s',
    }
  },
  version         => '0.3',
}
```
# Reference
<!-- DO NOT EDIT: This document was generated by Puppet Strings -->

## Table of Contents

**Classes**

_Public Classes_

* [`orcus`](#orcus): Installs and configures orcus.

_Private Classes_

* `orcus::config`: Private class for managing orcus config.
* `orcus::install`: Private class for installing orcus.
* `orcus::params`: Private class for setting default orcus parameters.
* `orcus::service`: Private class for managing orcus service.

**Functions**

* [`orcus_config`](#orcus_config): Convert hash to Orcus TOML config.

## Classes

### orcus

Installs and configures orcus.

#### Examples

##### Install orcus.

```puppet
class { 'orcus':
  override_config  => {
    general => {
      listen_address => '127.0.0.1:3008',
    }
  }
}
```

#### Parameters

The following parameters are available in the `orcus` class.

##### `package_name`

Data type: `String`

Package containing orcus. Defaults to 'orcus'.

Default value: $orcus::params::package_name

##### `version`

Data type: `String`

Version of orcus. Defaults to 'latest'.

Default value: $orcus::params::version

##### `manage_service`

Data type: `Boolean`

Specifies whether orcus service should be managed. Defaults to 'true'.

Default value: $orcus::params::manage_service

##### `user`

Data type: `String`

User for orcus. Defaults to 'orcus'.

Default value: $orcus::params::user

##### `group`

Data type: `String`

User for orcus. Defaults to 'orcus'.

Default value: $orcus::params::group

##### `package_install_options`

Data type: `Array[String]`

Array of install options for managed package resources. Appropriate options are passed to package manager.

Default value: $orcus::params::package_install_options

##### `override_config`

Data type: `Hash`

Hash of override configuration options for orcus

Default value: {}

## Functions

### orcus_config

Type: Ruby 3.x API

Convert hash to Orcus TOML config.



## Limitations

For a list of supported operating systems, see [metadata.json](https://github.com/MaxFedotov/puppet-orcus/blob/master/metadata.json)

## Development

Please feel free to fork, modify, create issues, bug reports and pull requests.



See Also
--------

* [orcus](https://github.com/MaxFedotov/orcus)
