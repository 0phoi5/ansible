# Ansible
A collection of useful, Linux administration related Ansible playbooks.

Most of these will require;
- an ansible.cfg
- an inventory file called 'inventory'
- an ssh_to_dmz.cfg file, if DMZ servers are relevant
  
  
Ansible.cfg
---
<pre>
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
</pre>
  
ssh_to_dmz.cfg
---
<pre>
# Written by Jack Collins
# See https://blog.scottlowe.org/2015/12/24/running-ansible-through-ssh-bastion-host/
  
# Host to jumpbox relationships, amend as required. Make sure SSH keys are in place first.
Host host1 host2 host3 gba71299
  ProxyCommand ssh -W %h:%p host123
Host host4 host5 host6
  ProxyCommand ssh -W %h:%p host456

# Universal settings for each jumpbox, including multiplexing
Host *
  User edit_me
  ControlMaster auto
  ControlPath ~/.ssh/ansible-%r@%h:%p
  ControlPersist 1m
</pre>
