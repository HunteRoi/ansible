# ansible

Documentation available at https://docs.ansible.com/ansible/latest/index.html

## Introduction

### Step 1
Starting with a `.ini` inventory, one can test connections with the `ansible all -i ./hosts.ini -m ping` (Linux/UNIX likes) 
and `ansible all -i ./hosts.ini -m win_ping` (Windows) commands.

### Step 2
Some data in the inventory is redundant. One can introduce a general configuration in the form of `ansible.cfg` file to simplify their inventory.
Testable with `ansible all -m [win_]ping`.

### Step 3
To retrieve the uptime for all machines, you can do the following :
- `ansible all -m ansible.builtin.command -a "uptime"` on Linux/UNIX machines
- `ansible all -m ansible.windows.win_command -a "wmic path Win32_OperatingSystem get LastBootUpTime"` on Windows

### Step 4
It is possible to use yaml instead of ini (hosts.yml in place of the hosts.ini file).

### Step 5
To upgrade a debian host, one would run a playbook.
As upgrading requires sudo access, the `-K` (or `--ask-become-pass`) option is necessary on the command : `ansible-playbook ./playbooks/upgrade_debian.yml -K`

### Step 6
To upgrade all their hosts, one would run a playbook.
As upgrading requires sudo access, the `-K` (or `--ask-become-pass`) option is necessary on the command : `ansible-playbook ./playbooks/upgrade.yml -K`

### Step 7
One could upgrade all their hosts, one could also run a playbook with conditional tasks, using ansible_facts.

EDIT: Windows needs to reboot to install the updates properly.

## Groups

### Step 1
In order to install a webserver, groups can be made in the hosts.yml file (to distinguish a set of hosts from others).

### Step 2
To access the webserver on their machine, one should open some ports through the firewall on Fedora.

### Step 3
To simplify their playbooks and inventory, one could use host_vars folder and store their variables in a `<host>.yml` file.

### Step 4
To install the file service and the db service, one should 
- read the docs
- configure both services
- start the services
- and not forget about variables and generic modules.
