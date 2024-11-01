service_groups
=====================

This role manages service objects groups on a Palo Alto Firewall.

Requirements
------------

ansible-galaxy collection install paloaltonetworks.panos

Note: Installing collections with ansible-galaxy is only supported in ansible-core>=2.13.9

Requires Ansible >=2.15.0

Role Variables
--------------
The role will fetch the Variables from file: "{{ inventory_dir }}/group_vars/objects/service_objects_group.yml" 

service_groups:
  - name: 'Web_Services'
    value:
      - 'prox-mgmt'
      - 'tcp-3000'
    tag: null
    state: 'present'

  - name: 'DNS_Services'
    value:
      - 'DNS'
      - 'DNS-256'
      - 'DNS-5353'
    tag: null
    state: 'replaced'


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

