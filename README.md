# Ansible role: MariaDB (server)

[![Build Status](https://travis-ci.org/jodyboucher/ansible-role-mariadb.svg?branch=master)](https://travis-ci.org/jodyboucher/ansible-role-mariadb)

An [Ansible](https://www.ansible.com/) role that installs and configures MariaDB server.

This role is designed for and tested on the following OS distributions:

* Ubuntu 16.04 Xenial
* Ubuntu 18.04 Bionic

## Requirements

* [Ansible](https://docs.ansible.com/ansible/intro_installation.html) >= 2.4 (makes use of new import_tasks module)
* This role requires `root` access so be sure to enable privilege escalation:

```yml
# privilege escalation of play
- hosts: databases
  become: true
  roles:
    -role: mariadb

# escalation of single role only
- hosts: database
  roles:
    - role: mariadb
      become: true
```

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`):

```yml
# The root account name and password
mariadb_root_username: root
mariadb_root_password: changeme

# Prerequisite pacakges
mariadb_require_packages:
  - software-properties-common
  - python-mysqldb

# The version of MariaDB to install
mariadb_version: 10.1
# GPG signing info for MariaDB repository
mariadb_upstream_keyserver: hkp://keyserver.ubuntu.com:80
mariadb_upstream_key_id: "0xF1656F24C74CD1D8"
# Location of the MariaDB repository.
mariadb_upstream_repo: "deb [arch=amd64,i386,ppc64el] http://nyc2.mirrors.digitalocean.com/mariadb/repo/{{ mariadb_version }}/ubuntu {{ ansible_distribution_release }} main"

# Default mysqld config values
mariadb_mysqld_user: mysql
mariadb_mysqld_port: 3306
mariadb_mysqld_pid_file: "/var/run/mysqld/mysqld.pid"
mariadb_mysqld_socket: "/var/run/mysqld/mysqld.sock"
mariadb_mysqld_bind_address: "127.0.0.1"
mariadb_mysqld_max_connections: 50
mariadb_mysqld_connect_timeout: 5
mariadb_mysqld_wait_timeout: 600
mariadb_mysqld_thread_cache_size: 50
mariadb_mysqld_max_allowed_packet: 4M
mariadb_mysqld_sort_buffer_size: 1M
mariadb_mysqld_tmp_table_size: 24M
mariadb_mysqld_read_buffer_size: 1M
mariadb_mysqld_read_rnd_buffer_size: 4M
mariadb_mysqld_join_buffer_size: 256k
mariadb_mysqld_bulk_insert_buffer_size: 16M
mariadb_mysqld_query_cache_type: 1
mariadb_mysqld_query_cache_size: 32M
mariadb_mysqld_query_cache_limit: 256k
mariadb_mysqld_log_warnings: 2
mariadb_mysqld_slow_query_log: 0
mariadb_mysqld_slow_query_log_file: "/var/log/mysql/mariadb-slow.log"
mariadb_mysqld_long_query_time: 10
mariadb_mysqld_log_slow_verbosity: query_plan
mariadb_mysqld_log_slow_rate_limit: 100
mariadb_mysqld_log_queries_not_using_indexes: 1
mariadb_mysqld_general_log: 0
mariadb_mysqld_general_log_file: "/var/log/mysql/mariadb.log"
mariadb_mysqld_max_heap_table_size: 24M
mariadb_mysqld_key_buffer_size: 8M
mariadb_mysqld_innodb_strict_mode: 1
mariadb_mysqld_innodb_buffer_pool_size: 64M
mariadb_mysqld_innodb_buffer_pool_instances: 1
mariadb_mysqld_innodb_file_per_table: 1
mariadb_mysqld_innodb_flush_method: O_DIRECT
mariadb_mysqld_innodb_io_capacity: 500
mariadb_mysqld_innodb_log_buffer_size: 8M
mariadb_mysqld_performance_schema: "off"
mariadb_mysqld_binary_logging_enabled: false

```

## Dependencies

None.

## Example Playbook

```yml
---
- hosts: databases
  become: true
  vars_files:
    - vars/main.yml
  roles:
    - { role: mariadb }
```

Inside `vars/main.yml`:

```yml
---
mariadb_root_password: make*me*secure

mariadb_mysqld_max_connections: 500
```

## Installation

On the command-line:

```bash
ansible-galaxy install git+https://github.com/jodyboucher/ansible-role-mariadb.git
```

or in a role file (requirements.yml):

```yml
- name: mariadb
  src: https://github.com/jodyboucher/ansible-role-mariadb
  version: master
```

## License

MIT

## Author Information

This role was created by [Jody Boucher](https://jodyboucher.com/).
