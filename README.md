Ansible role EnvFiles
=========

A simple role to create `.env` files.

Requirements
------------

None.

Role Variables
--------------

None

Dependencies
------------

None

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

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

License
-------

GPL-2.0

Author Information
------------------

Martin Kruták <devklingac@gmail.com>

