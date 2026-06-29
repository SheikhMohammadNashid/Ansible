
The **Ansible configuration file** (`ansible.cfg`) is the control center for Ansible's behavior. It tells Ansible how to operate, where to find key files, and how to connect to your managed servers.

Instead of passing dozens of flags (like `-u username` or `-i inventory`) every time you run a command, you define those settings once in this file.

  How Ansible Finds the Config File (The Order of Precedence)

Ansible doesn't just look in one place. It searches for a configuration file in a specific order and **stops at the first one it finds**.

1. **`ANSIBLE_CONFIG`**: An environment variable pointing directly to a file (highest priority).
    
2. **`./ansible.cfg`**: A config file located in your current working directory (where you run the command).
    
3. **`~/.ansible.cfg`**: A config file in the user's home directory.
    
4. **`/etc/ansible/ansible.cfg`**: The default global system configuration file (lowest priority).

![[Screenshot_20260627_102128.png]]

when run the play it will shows error:


[WARNING]: log file at '/var/log/ansible.log' is not writeable and we cannot create it, aborting

![[Screenshot_20260627_102330.png]]


This happens because this directory is qownd by the root user. we have to change its ownership:

use these commands:

sudo touch /var/log/ansible.log

chown ubuntu:ubuntu  /var/log/ansible.log
![[Screenshot_20260627_102857.png]]

now will make the logs



![[Screenshot_20260627_103320.png]]

