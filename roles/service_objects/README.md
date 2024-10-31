service_objects
=========

This role manages service objects on a Palo Alto Firewall.

Requirements
------------

ansible-galaxy collection install paloaltonetworks.panos

Note: Installing collections with ansible-galaxy is only supported in ansible-core>=2.13.9

Requires Ansible >=2.15.0

Role Variables
--------------
The role will fetch the Variables from file: "{{ inventory_dir }}/group_vars/objects/service_objects.yml" 
services:
  - name: 'DNS-256'
    protocol: 'tcp'
    destination_port: '536'
    description: 'service'
    tag: null
    state: 'present'


Example Playbook
----------------

Include the role in your playbook:

- name: Manage Palo Alto Firewall Tags
  hosts: prod-firewall01
  connection: local
  gather_facts: false
  roles:
    - role: service_objects

License
-------

Apache 2.0 License

Author Information
------------------
MHElnour

