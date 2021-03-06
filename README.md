# User

[![Ansible Galaxy][galaxy_image]][galaxy_link]
[![Latest tag][tag_image]][tag_url]
[![Build Status][travis_image]][travis_link]

A role for managing users.

## Requirements

- Hosts should be bootstrapped for ansible usage (have python,...)
- Root privileges, eg `become: yes`
- `useradd`, `userdel` and `usermod` should be available on the host

## Role Variables

| Variable | Description | Default value |
|----------|-------------|---------------|
| `user_list` | List of users **(see details!)** | `[]` |
| `user_list_host`| List of users **(see details!)**  | `[]` |
| `user_list_group` | List of users **(see details!)** | `[]` |
| `user_append` | Default value for `append` | `no` |
| `user_createhome` | Default value for `createhome` | `yes` |
| `user_force` | Default value for `force` | `no` |
| `user_generate_ssh_key` | Default value for `generate_ssh_key` | `no` |
| `user_move_home` | Default value for `move_home` |`no` |
| `user_none_unique` | Default value for `none_unique` | `no` |
| `user_remove` | Default value for `remove` | `no` |
| `user_shell` | Default value for `shell` | '/bin/sh' |
| `user_ssh_key_bits` | Default value for `ssh_key_bits` | 4096 |
| `user_ssh_key_file` | Default value for `ssh_key_file` | '.ssh/id_rsa' |
| `user_state` | Default user `state` | `present` |
| `user_system` | Default value for `system` | `no` |
| `user_update_password` | Default value for `update_password` | `always` |

#### `user_list` details

`user_list`, `user_list_host` and `user_list_group` are merged when
managing the users. You can use the host and group lists to specify
users per host or group off hosts.

The user list allows you to define which users must be managed. Each item in
the list can have following attributes:

| Variable | Description | Required | Default |
|----------|-------------|----------|---------|
| `append` | Only append to groups? | no | `user_append` |
| `comment` | User description (aka GECOS) | no | / |
| `createhome` | Create home directory? | no | `user_createhome` |
| `expires` | Expiry data | no | / |
| `force` | Use --force option when deleting a user | no | `user_force` |
| `generate_ssh_key` | Generate ssh key?  | no | `user_generate_ssh_key` |
| `group` | Users primary group | no | / |
| `groups` | List of groups for the user | no | / |
| `home` | Home directory for the user | no | / |
| `login_class` | Login class for BSD systems | no | / |
| `move_home` | Move home directory | no | `user_move_home` |
| `name` | User name | yes | / |
| `non_unique` | Allow none unique uid | no | `user_none_unique` |
| `password` | Password for the user | no | / |
| `remove` | Use --remove option when deleting a user | no | `user_remove` |
| `shell` | Users shell | no | `user_shell` |
| `ssh_key_bits` | SSH key size | no | `user_ssh_key_bits` |
| `ssh_key_comment` | SSH key comment | no | / |
| `ssh_key_file` | SSH key file | no | `user_ssh_key_file` |
| `ssh_key_passphrase` | SSH key passphrase | no | / |
| `ssh_key_type` | SSH key type | no | rsa |
| `state` | User state | no | `user_state` |
| `system` | System account? | no | `user_system` |
| `uid` | User id | no | / |
| `update_password` | Update password if changed? | no | `user_update_password` |

###### Example `user_list`

```yaml
user_list:
  - name: user1
  - name: user2
    uid: 1001
    groups:
      - testgrp
      - sudo
  - name: user3
    uid: 1002
    state: absent
```

## Dependencies

None.

## Example Playbook

```yaml
---
- hosts: servers
  roles:
  - { role: infrausr.user, become: yes }
```

Inside `group_vars/servers.yml`:

```yaml
user_list_group:
  - name: user
    uid: 1001
  - name: testgrp
    state: absent
```

## Author
By [Prabhakaran V]

[galaxy_image]:         https://img.shields.io/badge/galaxy-prabhakaran2304.ansible--role--user--linux-orange.svg?style=flat
[galaxy_link]:          https://galaxy.ansible.com/prabhakaran2304/ansible-role-user-linux
[tag_image]:            https://img.shields.io/github/tag/prabhakaran2304/ansible-role-user-linux.svg
[tag_url]:              https://github.com/prabhakaran2304/ansible-role-user-linux/tags
[travis_image]:         https://travis-ci.org/prabhakaran2304/ansible-role-user-linux.svg?branch=master
[travis_link]:          https://travis-ci.org/prabhakaran2304/ansible-role-user-linux


