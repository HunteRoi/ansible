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
