## Create and Inventory file in the controller
## if you dont by default it will be created in /etc/ansible/hosts 
```
create an Inventory file on the controller
mkdir test-project 
touch inventory.txt
```

# inside the inventory file specify the targets e.g , inventory.txt 
```
target1 ansible_host=172.31.43.43
target2 ansible_host=172.31.42.5
```

# to make a group
```
[group-name]
target1 ansible_host=172.31.43.43
target2 ansible_host=172.31.42.5
```

# Run ansible-playbook
```
ansible-playbook playbook.yaml -i inventory.txt
```

# different inventory parameters such as 
```
ansible_connection     - for ssh/winrm/localhost
ansible_port           - 22/6986
ansible_user           - root/admin
ansible-ssh_pass       - password
```

# to text connectivity
```
ansible all -m ping -i inventory.txt
or 
ansible <target-name> -m ping -i inventory.txt
```


