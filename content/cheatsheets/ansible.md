+++
author = "null.co"
title = "Ansible Cheatsheet"
date = "2024-10-24"
description = ""
tags = [
    "cheatsheet",
    "ansible",
]
categories = [
    "cheatsheet"
]
aliases = ["cheatsheet"]
+++

## Ad-hoc commands

```bash
ansible all -m ping               # test ssh connection to all hosts in inventory
ansible all -m gather_facts       # Gather information about each host in inventory
```

```bash
ansible all -m apt -a update_cache=true --become --ask-become-pass        # like doing apt update
ansible all -m apt -a upgrade=dist --become --ask-become-pass             # like doing apt dist-upgrade
```

## Playbooks

We define the desired state of our hosts in a yaml file called playbook. A playbook is escentially a collection of tasks that are executed on each host to get to that desired state. Tasks should be idempotent.

```yaml
---
- hosts: all    # Runs on all hosts on inventory
  become: true  # For sudo-like extra permissions. --ask-become-pass will need to be specified
  tasks:
    - name: Update index    # This is the name of the play
      tags: always          # This will always runs, no matter what tags we use.
      apt:   # This is the name of the module that is gonna be used, there are many available modules
        update_cache: true
      changed_when: false   # We don't care about cache updates, so we don't consider it as a change
      when: ansible_distribution == "Ubuntu"   # We can have conditionals for plays
      
- hosts: web-servers    # Runs on web-servers hosts group only
  become: true
  tasks:
    - name: Install apache
      tags: apache                # We can also associate some tags to a play.
      apt:
        name: true
        state: present
      when: ansible_distribution == "Ubuntu"
        
```

Some useful playbook commnds

```bash
ansible-playbook --ask-become-pass <playbook-name>.yml     # To run a playbook (If contains plays with "becomes")
ansible-playbook --list-tags <playbook-name>.yml           # To list available tags in a playbook
ansible-playbook -t "t1,t2,t3" <playbook-name>.yml           # To only run plays/tasks with such tags
```

### Roles

Roles allow us to organize and reuse automation tasks into a modular way. Each role can represent a specific functionality or component of a system, such as installing and configuring a web server, managing users, or setting up a database.

```yaml
---
- hosts: all
  become: true
  roles:
    - base              # We can define what set of roles to include
      
- hosts: web-servers
  become: true
  roles:
    - web-servers
        
```

Roles should be defined as directories inside the `role` directory

```bash
...
roles
├── base
└── web-servers
...
```

Each of the roles should have the following structure
```
role    # Name of the role
└── tasks
    └── main.yml    # Here's where the role taskbook is placed. 
└── files           # For referencing files for copying, etc inside the role.
```

The taskbook looks almost like a playbook, but only contains tasks.

```yaml
- name: Install apache
  tags: apache
  apt:
    name: true
    state: present
  when: ansible_distribution == "Ubuntu"
  
- name: Copy html file for site
  tags: apache
  copy:
    src: index.html
    dest: /var/www/html/index.html
    owner: root
    group: root
    mode: 0644
  when: ansible_distribution == "Ubuntu"
```

