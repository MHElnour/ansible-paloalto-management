fw_rules
=====================

This role manages firewall rules on a Palo Alto Firewall.

Requirements
------------

ansible-galaxy collection install paloaltonetworks.panos

Note: Installing collections with ansible-galaxy is only supported in ansible-core>=2.13.9

Requires Ansible >=2.15.0

Role Variables
--------------
The role will fetch the Variables from file: "{{ inventory_dir }}/group_vars/rules/combined_firewall_rules.yml" this file will automatically be created and updated based on changes done to:

- {{ inventory_dir }}/group_vars/applications_rules # defines rules apps eg : app1_rules.yml
- {{ inventory_dir }}/group_vars/categories_rules # defines rules apps eg : generic_allow.yml
- {{ inventory_dir }}/group_vars/all.yml # define the apps and cat you want to include

in group_vars/all.yml define the following variables to specify which application and category rule files to be include:

applications_rules:
  - app1_rules
categories_rules:
  - "generic_allow"

Example Playbook
----------------
```yml
- name: Push All Objects to Palo Alto Firewall
  hosts: prod-firewall01
  connection: local
  gather_facts: false
  become: false
  roles:
    - role: fw_rules
```

License
-------

Apache 2.0 License

Author Information
------------------
MHElnour

