Ansible role: EnvFiles
=========

[![CI](https://github.com/klingac/ansible_role_envfiles/actions/workflows/ci.yml/badge.svg?branch=main)](https://github.com/klingac/ansible_role_envfiles/actions/workflows/ci.yml)

A simple role to create `.env` files.

Requirements
------------

No special requirements.

Role Variables
--------------

Possible default values for one ENV file are:

```
envfile_path_default: /etc/environment
envfile_template_src_default: env.j2
envfile_owner_default: root
envfile_group_default: root
envfile_mode_default: 600
envfile_has_secrets_default: false
envfile_config_default: {}
```

This will define dictionary that represents ENV file;

```
_envfile_default:
  path: "{{ envfile_path_default }}"
  template_src: "{{ envfile_template_src_default }}"
  owner: "{{ envfile_owner_default }}"
  group: "{{ envfile_group_default }}"
  mode: "{{ envfile_mode_default }}"
  has_secrets: "{{ envfile_has_secrets_default }}"
  config: "{{ envfile_config_default }}"
```

This role accepts list of these dictionaries
```
envfiles_list:
  - "{{ _envfile_default }}"
```

This is the way, we can pass multiple env files at once, e.g.  like this
```
envfile1:
  path: /etc/env1
  config:
    key1: value1
    key2: value2

envfile2:
  path: /etc/env2
  config:
    key3: value3
    key4: value4

envfiles_list:
  - "{{ _envfile_default | combine(envfile1, recursive=true) }}"
  - "{{ _envfile_default | combine(envfile2, recursive=true) }}"
```

Dependencies
------------

No dependencies

Example Playbook
----------------

```
    - hosts: servers
      vars:
        envfiles_list:
          - name: "My custom env file"
            owner: root
            group: root
            mode: 0644
            path: /etc/environment
            config:
	      key1: val1
	      key2: val2
            has_secrets: false
      roles:
         - role: klingac.ansible_role_envfiles
```

License
-------

GPL-2.0

Author Information
------------------

Martin Kruták <devklingac@gmail.com>

