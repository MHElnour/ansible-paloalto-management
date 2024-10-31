# ansible-paloalto-management



# Firewall Automation with Ansible

## Overview

This repository contains Ansible roles and playbooks designed to automate the management of Palo Alto Firewall configurations. It streamlines the process of pushing objects, services, groups, and tags to your firewall, ensuring consistency and efficiency.
Ideal for automating tasks like firewall rules creation , and managing address objects and groups with Ansibl

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

