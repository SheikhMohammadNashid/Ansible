
1:Installing

$ sudo apt update
$ sudo apt install software-properties-common
$ sudo add-apt-repository --yes --update ppa:ansible/ansible
$ sudo apt install ansible

use there commands to install the ansible

2: Their are two ways of making inventory files
- Ini
- YAML

ini example:

[webservers]
192.168.x.x ansible_user=ubuntu
192.168.x.x ansible_user=ec2_user


YAML example:

all:  
 hosts:  
   web01:  
     ansible_host: 172.31.33.148  
     ansible_user: ec2-user  
     ansible_ssh_private_key_file: clientkey.pem  
   web02:  
     ansible_host: 172.31.42.37  
     ansible_user: ec2-user  
     ansible_ssh_private_key_file: clientkey.pem  
   webdb:  
     ansible_host: 172.31.36.85  
     ansible_user: ec2-user  
     ansible_ssh_private_key_file: clientkey.pem


make sure the ssh private key is in same directory as inventory.yaml file

3: Make sure that you add these two lines in /etc/ansible/ansible.cfg file

[defaults]
host_key_checking = False

the deals with initial "yes" problem during ssh process other wise you will get this error

[ERROR]: Task failed: Failed to connect to the host via ssh: Host key verification failed.  
Origin: <adhoc 'ping' task>  
  
{'action': 'ping', 'args': {}, 'timeout': 0, 'async_val': 0, 'poll': 15}  
  
web01 | UNREACHABLE! => {  
   "changed": false,  
   "msg": "Task failed: Failed to connect to the host via ssh: Host key verification failed.",  
   "unreachable": true  
}