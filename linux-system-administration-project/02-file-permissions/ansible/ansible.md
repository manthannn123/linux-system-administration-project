User Management - Ansible Automation
1) Objective

Recreate the manual user-management configuration using Ansible

2) Requirement

The automation must:
- Create groups
- Create users
- Assign Users to groups
- Configure Login shells
- Configure sudo access where requried
- Ensure home directories exit

3) Environment
- control node: 192.168.0.18
- Managed node: 192.168.0.20

4) Files

- inventory - Defines the managed servers
- user-management.yml - Ansible playbook for user and group management

