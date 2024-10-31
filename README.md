# Firewall Automation with Ansible

## Overview

This repository contains Ansible roles and playbooks designed to automate the management of Palo Alto Firewall configurations. It streamlines the process of pushing objects, services, groups, and tags to your firewall, ensuring consistency and efficiency.
Ideal for automating tasks like firewall rules creation , and managing address objects and groups with Ansible.

### Logic for Address Object
The logic starts by maintaining a clean repository. When the build validation starts, it first
validates the repository itself as it holds the data that will be pushed to the firewall. Ansible
will flag any duplicate names or values. The objective is to maintain a source of truth for
address objects, object groups, services, and service groups, as these will just be referenced
in the rules. This source of truth will be maintained and checked by the build validation
checks to always be clean, and will flag any errors and halt the execution of the playbook.

### Objectives
- Automatethedetection of duplicate address objects in the source configuration.
- Validate that address objects defined in the inventory are correctly configured on the firewall.
- Identify missing address objects and automatically push them to the firewall if necessary.
- Ensure aconsistent and synchronized state between the source inventory and firewall.

### Role Structure
- Tasks were organized within the `address_objects` role, including validation
 (`validate_address_objects.yml`) and pushing (`push_address_objects.yml`) address objects.
- The modular structure allows new tasks to be added easily without impacting existing
 tasks.

### Success Criteria
- Validation Completion: Address objects are checked for duplicate names and values. If no duplicates are found, the validation passes.
- MismatchedObjects Identification: Successfully identifying and reporting mismatched address objects between the source and firewall configurations.
- PushTaskExecution: Missing address objects are successfully pushed to the firewall.

### Failure Criteria
- Duplicate Objects Detected: The presence of duplicate address object names or values in the source configuration.
- MismatchWithoutResolution: The mismatch between the source and the firewall that could not be resolved by pushing missing address objects.
- PushFailures: Failures in pushing missing address objects to the firewall.

![dup_objects](https://github.com/user-attachments/assets/0e519be5-e83a-4c19-92a7-c6338627c225)
![dup_values](https://github.com/user-attachments/assets/8c782fde-cebf-48b1-9575-cd0d75924a98)

![all_match](https://github.com/user-attachments/assets/ab54c363-40e7-4bc7-bd06-f74abe1635b1)
![push_new_only](https://github.com/user-attachments/assets/62e0f024-7bfe-48d6-bbad-2e03da9750b6)


## Features

- **Service Objects Management:** Define and manage individual service objects.
- **Service Groups Management:** Group service objects for streamlined policy application.
- **Address Objects Management:** Define and manage individual address objects.
- **Address Groups Management:** Group address objects for organized network segmentation.
- **Tag Objects Management:** Create and manage tags to categorize and describe firewall objects.


## Current Status

🚧 **Under Development**

This project is actively being developed. The following functionalities are currently implemented and operational:

- **Pushing Objects:** Automates the creation and updating of address objects.
- **Pushing Services:** Manages service objects and ensures they are correctly configured.
- **Pushing Groups:** Handles the creation and updating of service and address groups.
- **Pushing Tags:** Automates the management of tag objects for better organization.

**Note:** The workflow is not yet complete. Future updates will include enhanced features, error handling, and support for additional firewall configurations.

## Installation

### Prerequisites

- **Ansible 2.9+**: Ensure Ansible is installed on your control machine.
  
  ```bash
  ansible --version
  git --version

- Palo Alto Networks PAN-OS Collection: Install the necessary Ansible collection.

  ```bash
  ansible-galaxy collection install paloaltonetworks.panos
  # Please make sure to visit https://github.com/PaloAltoNetworks/pan-os-ansible/blob/develop/requirements.txt and make sure you have all the requirements for the Collection to function.

**Clone the Repository:**
```bash
   git clone https://github.com/MHElnour/ansible-paloalto-management.git
   cd ansible-paloalto-management
```
## Usage Guidelines

- Modular Role Structure: Organize your master playbook to invoke only the roles needed for each task. For example, if you’re adding address objects or service groups, include only the corresponding roles.
- Handling the Absent State: This role also supports resource removal from the firewall using the absent state. To delete a resource, structure your playbook carefully:
  - Example: Removing a Service Object
    - If the service object you want to remove is part of a service group, first update the group by setting its state to merged and removing the service from it.
    - Then, set the service object's state to absent and include the role to ensure the object is removed from the firewall.
    - Follow the correct order: update the group first, then delete the service object.

    ```bash
    - name: Removing service object
      hosts: prod-firewall01
      connection: local
      gather_facts: false
      become: false
      roles:
         - role: service_groups
         - role: service_objects

By following a logical structure, you ensure that all resources are created, updated, or removed in the correct order, preventing issues related to dependencies, such as undefined tags. This flexible setup allows for easy management and customization according to the needs of your Palo Alto environment.



