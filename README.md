[![Build Status](https://travis-ci.org/mkayontour/ansible-influxdb.svg?branch=master)](https://travis-ci.org/mkayontour/ansible-influxdb)
[![Ansible Quality Score](https://img.shields.io/ansible/quality/50067?label=role%20quality)](https://galaxy.ansible.com/mkayontour/influxdb)

Ansible InfluxDB
=========

This role installs, manages and configures InfluxDB. Including Databases and Users. Most major distribution should be supported.
Pull-Requests and Issues are welcome :)

Requirements
------------

Two requirements need to be in place at first, the **influxdb python client** should be installed, the role does take care of that.


And second, **pip needs to be present** in order to install influxdb python client.

Role Variables
--------------

### Defaults

The Default variables are all listed below, for every config section of the
**influxdb.conf** there is its own variable.

Please change the admin password to something more secure then the default:

```
influxdb_admin_username: admin
influxdb_admin_password: admin
```

```
---
influxdb_manage_repository: yes
influxdb_manage_package: yes
influxdb_config_dir: /etc/influxdb
influxdb_config_global:
    reporting-disabled: false
    bind-address: 127.0.0.1:8086
influxdb_config_graphite:
  - enabled: false
    tags:
      - region=us
      - zone=test
influxdb_config_collectd:
  - enabled: false
influxdb_config_udp:
  - enabled: false
influxdb_config_meta:
  dir: /var/lib/influxdb/meta
  retention-autocreate: true
  logging-enabled: true
influxdb_config_http:
  enabled: true
  bind-address: :8086
  auth-enabled: true
  ping-auth-enabled: true
influxdb_config_data:
  dir: /var/lib/influxdb/data
  wal-dir: /var/lib/influxdb/wal
  series-id-set-cache-size: 100
influxdb_admin_username: admin
influxdb_admin_password: admin
```

Please consult the params for every config section from the documentation:

`influxdb_config_global` [global](https://docs.influxdata.com/influxdb/v1.8/administration/config/#global-settings)

`influxdb_config_meta` [meta](https://docs.influxdata.com/influxdb/v1.8/administration/config/#meta)

`influxdb_config_data` [data](https://docs.influxdata.com/influxdb/v1.8/administration/config/#data)

`influxdb_config_http` [http](https://docs.influxdata.com/influxdb/v1.8/administration/config/#http)

`influxdb_config_subscriber` [subscriber](https://docs.influxdata.com/influxdb/v1.8/administration/config/#subscriber)

`influxdb_config_graphite` [graphite](https://docs.influxdata.com/influxdb/v1.8/administration/config/#graphite)

`influxdb_config_monitor` [monitor](https://docs.influxdata.com/influxdb/v1.8/administration/config/#monitor)

`influxdb_config_shard_precreation` [shard-precreation](https://docs.influxdata.com/influxdb/v1.8/administration/config/#shard-precreation)

`influxdb_config_collectd` [collectd](https://docs.influxdata.com/influxdb/v1.8/administration/config/#collectd)

`influxdb_config_continuous_queries`

`influxdb_config_tls`

`influxdb_config_retention`

`influxdb_config_udp`


All Sections which can be defined multiple times, these are defined as array.

Following Example:
```
influxdb_config_graphite:
  - enabled: true
    database: graphite
    tags:
      - region=us
      - zone=test
      - instance=01
  - enabled: true
    database: graphite2
    tags:
      - region=de
      - zone=prod
      - instance=02
```

### Define Databases

To define databases just use following syntax to create multiple:
```
influxdb_databases:
  - name: telegraf-metrics
    state: present
  - name: graphite
    state: present
  - name: icinga
    state: present
```

All params for the databases are listed below:

```
influxdb_databases:
  - name:
    login_password:
    login_username:
    hostname:
    port:
    proxies:
    retries:
    state:
    ssl:
    timeout:
    udp_port:
    use_udp:
    validate_certs:

```

### Define Users

To define users just use following syntax to create multiple:
```
influxdb_users:
  - name: influxadm
    password: influxdbadmpass
    admin: yes
  - name: icinga
    admin: no
    password: icinga
    grants:
      - database: 'icinga'
        privilege: 'WRITE'
```
All params for the users are listed below:

```
influxdb_users:
  - name: foo
    admin: true/false
    state: present/absent
    password: 'password'
    port: 8086
    hostname: localhost
    login_username: admin
    login_password: admin
    ssl: true/false
```



Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: influxdb-node1
      vars:
        influxdb_admin_username: admin
        influxdb_admin_password: admin123
        influxdb_databases:
          - name: telegraf-metrics
            state: present
        influxdb_users:
          - name: telegraf
            password: telegraf
            grants:
              - database: telegraf-metrics
                privilege: "WRITE"
      roles:
         - { role: mkayontour.influxdb }

License
-------

Apache-2.0

Author Information
------------------

Twitter: @mkayontour
