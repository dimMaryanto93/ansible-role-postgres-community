`dimmaryanto93.postgres_community`
=========

This ansible role to help you install PostgreSQL Community edition version (`12`, `13`, `14`, `15`, and `16`) for supported platform:

- CentOS 7/8
- Oracle Linux 8.7
- Ubuntu 20.04

There is 2 type version
- standalone
- High Available (HA) required `ha_proxy` and `keeplived` install separatly

Requirements
------------

Untuk menggunakan role ini, kita membutuhkan package/collection

- [ansible.posix](https://github.com/ansible-collections/ansible.posix)
- [community.postgresql](https://github.com/ansible-collections/community.postgresql)

Temen-temen bisa install, dengan cara

```bash
ansible-galaxy collection install ansible.posix community.postgresql --force
```

Atau temen-temen bisa menggunakan `requirement.yaml` file and install menggunakan `ansible-galaxy collection install -r requirement.yaml`, dengan format seperti berikut:

```yaml
---
collections:
  - ansible.posix
  - community.postgresql
  - community.general
```

Role Variables
--------------

Ada beberapa variable yang temen-temen bisa gunakan untuk setting docker daemon, diantaranya seperti berikut:

| Variable name                    | Example value  | Description |
| :---                             | :---           | :---        |
| `postgres_version`               | `15`           | Default PostgreSQL version is `15` but you can try another version such as `12`, `13`, `14`, and `16` |
| `postgres_data_dir`              | `/var/lib/pgsql/{{ postgres_version }}/data/` | Location the data is stored by postgresql |
| `postgres_port`                  | `5432`         | Port default Postgresql connection |
| `postgres_unix_socket`           | `postgres_unix_socket` | Default socket connectionn to modify properties postgresql |
| `update_pg_hba_conf`             | `true`         | Modifikasi default value for files such as `pg_hba.conf`, `postgresql.conf` |
| `enabled_postgresql_ha`          | `false`        | For enable postgresql HA mode set to `true`. When it's enabled ansible will install `patroni`, `etcd`,` python lib patroni` |


Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

For standalone PostgreSQL 15

```yaml
- name: Install PostgreSQL
  hosts: ['all']
  become: true
  vars: 
    postgres_version: 15
    enabled_postgresql_ha: false
  roles: 
    - dimmaryanto93.postgres_community
```

For HA PostgreSQL 15

```yaml
- name: Install PostgreSQL
  hosts: ['all']
  become: true
  vars: 
    postgres_version: 15
    enabled_postgresql_ha: true
  roles: 
    - dimmaryanto93.postgres_community
```

For another version of PostgreSQL

```yaml
- name: Install PostgreSQL 12
  vars: 
    postgres_version: 12
```

License
-------

MIT

