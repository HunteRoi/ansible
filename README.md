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
To retrieve the uptime for all machines, one can do the following :
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

### Step 5
To simplify again their playbooks, one could use group_vars folder.

## Tags

### Step 1
It is possible to tag tasks, blocks and playbooks. For that, one can use the "tags" property.

### Step 2
To install glances on all machines, one should play with services, pip and distro's package manager
as well as firewall rules.
It is also important to remember proxy modules for Apache/HTTPD and SELinux on Fedora that prevents interaction
from applications that are not authorized.

### Step 3 - optional & unrecommended
Protecting one's glances app on one's machine is quite a trick if not known beforehand.
The documentation says to use `--username` and `--password` to generate a password for a specific username.
Once this step is done, you can use the `-u <username>` option to start the application with that user required for
authentication.

For a playbook to work, one can provide the password directly into a file named with the username
and update the glances.conf file to point to the location where the .pwd file is copied.

NB: especially for Fedora, it is important to check firewall rules and SELinux restrictions.

As a generated password on Fedora does not work on Debian/Archlinux, neither is one generated on Debian/Archlinux working on Fedora,
 it does unfortunately prevents to generate a single password file on a machine and export it to several others.

This means that the step one's supposed to do is to generate the password on the machine.

## Roles

### Step 1
Roles can be imported from Ansible Galaxy using the `ansible-galaxy install <name> -p <path>` command.

e.g. : `ansible-galaxy install vincentclee.glances -p ./roles`

As one's probably using a custom roles path, the `ansible.cfg` file should be updated to have a new variable `roles_path=./roles` 
so that the role can be discovered.

### Step 2
One can create custom roles by following a simple guide:
1. create a folder in `./roles` with your role's name
2. add the following tree :
```
- defaults
-- main.yml
- files
-- main.yml
- handlers
-- main.yml
- library
-- custom_module.py
- meta
-- main.yml
- tasks
-- main.yml
- templates
-- main.yml
- vars
-- main.yml
```

