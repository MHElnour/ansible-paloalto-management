address_groups
=====================

This role manages address objects groups on a Palo Alto Firewall.

Requirements
------------

ansible-galaxy collection install paloaltonetworks.panos

Note: Installing collections with ansible-galaxy is only supported in ansible-core>=2.13.9

Requires Ansible >=2.15.0

Role Variables
--------------
The role will fetch the Variables from file: "{{ inventory_dir }}/group_vars/objects/address_objects_group.yml" 

address_groups:
  - name: 'Web_Servers'
    static_value: ['dev-jumphost']
    description: 'Group of web servers'
    tag: null
    state: 'replaced'

  - name: 'Web_Servers_2'
    static_value: ['dev-jumphost', 'remote_snet']
    description: 'Group of web servers'
    tag: null
    state: 'absent'
    
  - name: 'Obsolete_Group'
    static_value: ['dev-jumphost', 'remote_snet', 'home-allnets']
    description: 'test 12 merged'
    tag: ['POC']
    state: 'merged'


Example Playbook
----------------

Include the role in your playbook:

- name: Manage Palo Alto Firewall Tags
  hosts: prod-firewall01
  connection: local
  gather_facts: false
  roles:
    - role: address_groups

License
-------

Apache 2.0 License

Author Information
------------------
MHElnour

