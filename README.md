# Ansible
A collection of useful, Linux administration related Ansible playbooks.

Most of these will require;
- an ansible.cfg
- an inventory file called 'inventory'
- an ssh_to_dmz.cfg file, if DMZ servers are relevant


Ansible.cfg
---
[defaults]
remote_user: root
inventory: inventory
deprecation_warnings: false

[privilege_escalation]
become: false
become_user: root
become_method: sudo
become_ask_pass: false

[ssh_connection]
ssh_args = -F ./ssh_to_dmz.cfg -o ControlMaster=auto -o ControlPersist=30m
control_path = ~/.ssh/ansible-%%r@%%h:%%p
