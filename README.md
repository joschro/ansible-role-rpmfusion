ansible-role-rpmfusion
======================
Install RPMfusion repository for Fedora based systems

Requirements
------------

None.

Role Variables
--------------

A description of the settable variables for this role should go here, including any variables that are in defaults/main.yml, vars/main.yml, and any variables that can/should be set via parameters to the role. Any variables that are read from other roles and/or the global scope (ie. hostvars, group vars, etc.) should be mentioned here as well.

Dependencies
------------

A list of other roles hosted on Galaxy should go here, plus any details in regards to parameters that may need to be set for other roles, or variables that are used from other roles.

Example Playbook
----------------

Create a file called ```ansible-playbook-rpmfusion.yml``` with following content:
```
---
# Ansible Playbook to enable RPMfusion repositories
- name: Set up RPMfusion repositories
  gather_facts: no
  tasks:
    - name: Make sure that an empty requirements.yml file exists
      file:
        path: requirements.yml
        state: touch

    - name: Create requirements.yml
      blockinfile:
        path: requirements.yml
        create: yes
        block: |
          # Install a role from the Ansible Galaxy
          #- src: joschro.rpmfusion
          
          # Install a role from GitHub
          - src: https://github.com/joschro/ansible-role-rpmfusion
            name: joschro.rpmfusion

    - name: Install required packages
      become: yes
      package:
        name: git
        state: present

    - name: Source required roles
      command: ansible-galaxy install -r requirements.yml
      # (add parameter --force to update role on succeeding runs of playbook)

    - name: Execute role
      include_role:
        name: joschro.rpmfusion
```

You can now run the appropriate of the following commands for your distribution on the command line to install the Ansible tools:
```
sudo dnf install ansible
```
or
```
sudo yum install ansible
```
or
```
sudo apt install ansible
```

Finally, run the playbook with
```
ansible-playbook -i 192.168.178.123 -u ansibleuser ansible-playbook-rpmfusion.yml
```
with the IP address and username being replace by the ones for your target system.


License
-------

GPLv3

Author Information
------------------

joschro
