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

  ansible-galaxy collection install paloaltonetworks.panos

**Clone the Repository:**

   ```bash
   git clone https://github.com/MHElnour/ansible-paloalto-management.git
   cd ansible-paloalto-management

### 1. Prepare Your Inventory
   Prepare Inventory: hosts.ini / host_vars
### 2. Encrypt Sensitive Variables with Ansible Vault
   ansible-vault encrypt host_vars/prod-firewall01.yml
### 3. Run the Playbook
   ansible-playbook playbook.yml --ask-vault-pass
```


