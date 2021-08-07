
Ansible Role: KeyDB Active Replication
=========

![CI](https://github.com/v0112358/ansible-role-keydb-active-replication/actions/workflows/main.yml/badge.svg) ![Ansible Role](https://img.shields.io/ansible/role/d/55920) [![GitHub license](https://img.shields.io/github/license/v0112358/ansible-role-keydb-active-replication)](https://github.com/v0112358/ansible-role-keydb-active-replication/blob/master/LICENSE.md)

Install and configure KeyDB Active Replication on your system.

Example Inventory
------------
```
[keydb_active_replication:children]
keydb_active_replication_infra
keydb_active_replication_shopping

[keydb_active_replication_infra]
vm-dev-keydb-infra-0
vm-dev-keydb-infra-1

[keydb_active_replication_shopping]
vm-dev-keydb-shopping-0
vm-dev-keydb-shopping-1
vm-dev-keydb-shopping-2
```
Example Playbook
------------

```
- name: Deploy KeyDB Active Replication
  hosts: keydb_active_replication
  pre_tasks:
    - name: Verify Ansible meets KeyDB requirements.
      assert:
        that: "ansible_version.full is version_compare('2.10.0', '>=')"
        msg: >
          "You must update Ansible to at least 2.10.0 to use this playbook"
  roles:
    - { role: keydb-active-replication, tags: keydb-active-replication }
```

Role Variables
--------------

These variables are set in defaults/main.yml.
```
---
######### KeyDB config
keydb_active_replication_conf:
  port: "6379"
  maxmemory: "64mb"
  rename_commands:
    - FLUSHDB
    - FLUSHALL
    - KEYS
    - SHUTDOWN
....
```

Requirements
------------

pip packages listed in requirements.txt.

License
-------

MIT

Author Information
------------------
v0112358
