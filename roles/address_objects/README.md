address_objects
=====================

This role manages address objects on a Palo Alto Firewall.

Requirements
------------

ansible-galaxy collection install paloaltonetworks.panos

Note: Installing collections with ansible-galaxy is only supported in ansible-core>=2.13.9

Requires Ansible >=2.15.0

Role Variables
--------------
The role will fetch the Variables from file: "{{ inventory_dir }}/group_vars/objects/address_objects.yml" 

address_objects:
  - name: "PA_Remote_Access"
    value: "10.3.10.129/27"
    address_type: "ip-netmask"
    description: null
    tag: null
    state: present

  - name: "opnsense_edge_mgmt"
    value: "192.168.18.9/32"
    address_type: "ip-netmask"
    description: "test push 101 handling tags?"
    tag: ['POC']
    state: merged

  - name: "traefik-proxy"
    value: "10.3.10.38/32"
    address_type: "ip-netmask"
    description: null
    tag: null
    state: present


Example Playbook
----------------

Include the role in your playbook:

- name: Manage Palo Alto Firewall Tags
  hosts: prod-firewall01
  connection: local
  gather_facts: false
  roles:
    - role: address_objects

License
-------

Apache 2.0 License

Author Information
------------------
MHElnour

