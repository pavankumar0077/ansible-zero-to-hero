# Inventory 

Ansible inventory file is a fundamental component of Ansible that defines the hosts (remote systems) that you want to manage and the groups those hosts belong to. The inventory file can be static (a simple text file) or dynamic (generated by a script). It provides Ansible with the information about the remote nodes to communicate with during its operations.

![image](https://github.com/pavankumar0077/ansible-zero-to-hero/assets/40380941/4459471c-d674-4565-b565-065d954cb91d)

![image](https://github.com/pavankumar0077/ansible-zero-to-hero/assets/40380941/8935cbdd-3f84-444b-91dd-b4eef05bd244)

- RECOMMENDED WAY IS TO USE .INI FILE IN THE INVENTORY, IF IT IS NOT THERE THEN IT WILL PEAK /etc/ansible.hosts -- file present here.

```
ubuntu@ip-172-31-7-237:~$ cat inventory.ini
ubuntu@65.2.140.150
ubuntu@65.2.183.204
ubuntu@ip-172-31-7-237:~$ ansible -i inventory.ini -m ping all
ubuntu@65.2.183.204 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
```
- HERE WE HAVE CREATED INVENTORY.INI FILE
- USED COMMAND LIKE -m == is a module and ping -- is the command and all means all the servers present in the INVENTORY.INI file

![image](https://github.com/pavankumar0077/ansible-zero-to-hero/assets/40380941/dac830c5-5a07-4eb9-b29b-e3173ddcdc00)

## ANSIBLE ADHOC COMMAND LINK : ``` https://docs.ansible.com/ansible/latest/command_guide/intro_adhoc.html ```

## GROUPING
```
ubuntu@ip-172-31-7-237:~$ cat inventory.ini
[app]
ubuntu@65.2.140.150

[db]
ubuntu@65.2.183.204
```
```
ubuntu@ip-172-31-7-237:~$ ansible -i inventory.ini -m ping db
ubuntu@65.2.183.204 | SUCCESS => {
    "ansible_facts": {
        "discovered_interpreter_python": "/usr/bin/python3"
    },
    "changed": false,
    "ping": "pong"
}
ubuntu@ip-172-31-7-237:~$ ansible -i inventory.ini -m ping app
ubuntu@65.2.140.150 | UNREACHABLE! => {
    "changed": false,
    "msg": "Failed to connect to the host via ssh: ssh: connect to host 65.2.140.150 port 22: Connection timed out",
    "unreachable": true
}
```

## Static Inventory

A static inventory file is typically a plain text file (usually named hosts or inventory) and is structured in INI or YAML format. Here are examples of both formats:

### INI Format

```
# inventory file: hosts

[webservers]
web1.example.com
web2.example.com

[dbservers]
db1.example.com
db2.example.com

[all:vars]
ansible_user=admin
ansible_ssh_private_key_file=/path/to/key
```

### YAML

```
# inventory file: hosts.yaml

all:
  vars:
    ansible_user: admin
    ansible_ssh_private_key_file: /path/to/key
  children:
    webservers:
      hosts:
        web1.example.com:
        web2.example.com:
    dbservers:
      hosts:
        db1.example.com:
        db2.example.com:
```

![image](https://github.com/pavankumar0077/ansible-zero-to-hero/assets/40380941/63b89930-7a49-4c6f-b0ff-b207d3f4e4ab)


```
ansible -i inventory.ini -m shell -a "sudo ls /etc/" all

- Here -m is used to use modules here module is "shell" -a == is called arugment and "command" all == is all server, if can mention like db, app server like that as well

ansible -i inventory.ini -m shell -a "sudo apt install nginx" all
ansible -i inventory.ini -m shell -a "sudo apt install openjdk-17" db
```


## Dynamic Inventory

A dynamic inventory is generated by a script or plugin and can be used for environments where hosts are constantly changing (e.g., cloud environments). The script or plugin fetches the list of hosts from a source like AWS, GCP, or any other dynamic source.

Here is an example of a dynamic inventory script for AWS EC2:

```
#!/usr/bin/env python

import json
import boto3

def get_aws_ec2_inventory():
    ec2 = boto3.client('ec2')
    instances = ec2.describe_instances()
    inventory = {
        'all': {
            'hosts': [],
            'vars': {
                'ansible_user': 'ec2-user',
                'ansible_ssh_private_key_file': '/path/to/key'
            }
        },
        '_meta': {
            'hostvars': {}
        }
    }

    for reservation in instances['Reservations']:
        for instance in reservation['Instances']:
            if instance['State']['Name'] == 'running':
                public_ip = instance['PublicIpAddress']
                inventory['all']['hosts'].append(public_ip)
                inventory['_meta']['hostvars'][public_ip] = {
                    'ansible_host': public_ip
                }

    print(json.dumps(inventory, indent=2))

if __name__ == '__main__':
    get_aws_ec2_inventory()
```

## Usage

```
ansible-playbook -i inventory <Adhoc command or Playbook.yml>
```
