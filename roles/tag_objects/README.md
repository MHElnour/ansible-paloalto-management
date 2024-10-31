tag_objects
=========

This role manages tag objects on a Palo Alto Firewall.

Requirements
------------

ansible-galaxy collection install paloaltonetworks.panos

Note: Installing collections with ansible-galaxy is only supported in ansible-core>=2.13.9

Requires Ansible >=2.15.0

Role Variables
--------------
The role will fetch the Variables from file: "{{ inventory_dir }}/group_vars/objects/tags.yml" 
- `tags`:
  - `name`: Name of the tag.
  - `color`: Color of the tag.
  - `comments`: Description or comments about the tag.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Include the role in your playbook:

- name: Manage Palo Alto Firewall Tags
  hosts: prod-firewall01
  connection: local
  gather_facts: false
  roles:
    - role: tag_objects

License
-------

Apache 2.0 License

Author Information
------------------
MHElnour
