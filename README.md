Ansible InfluxDB
=========

This role installs, manages and configures InfluxDB. Including Databases and Users. Most major distribution should be supported. 
Pull-Requests and Issues are welcome :)

Requirements
------------

Two requirements need to be in place at first, the influxdb python client should be installed, the role does take care of that. 
And second, pip needs to be installed in order to install influxdb python client. 

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

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

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

    - hosts: influxdb-node1
      roles:
         - { role: mkayontour.influxdb }

License
-------

BSD

Author Information
------------------

An optional section for the role authors to include contact information, or a website (HTML is not allowed).
