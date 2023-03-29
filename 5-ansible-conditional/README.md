## Ansible conditionals
for example we have 2 playbooks that does the same thing which is install nginx on a host
but as we know different OS uses different package manager, e.g Debian uses apt while RedHat uses yum

```
- name: install NGINX
  hosts: debian_hosts
  tasks:
    - name: Install Nginx on Debian
      apt: 
       name: nginx
       state: present 
      when: ansible_os_family == "Debian" # use the  == when checking for equal statement 

    - name: Install Nginx on Redhat
      apt: 
       name: nginx
       state: present 
      when: ansible_os_family == "ReHat" or
            ansible_os_family == "SUSE"  # we use the or sign to specify either of the statements

    - name: Install Nginx on Debian
      apt: 
       name: nginx
       state: present 
      when: ansible_os_family == "Debian" and 
            ansible-distribution_version == "16.04" # we use the and to satisfy both conditions

```
# Example of when- install nginx when the tasks is node02

```
#inventory.txt file

node01 ansible_host=node01 ansible_ssh_pass=caleston123
node02 ansible_host=node02 ansible_ssh_pass=caleston123
[web_nodes]
node01
node02
```

# playbook
```
---
-  name: 'Execute a script on all web server nodes'
   hosts: all
   become: yes
   tasks:
     -  service: 'name=nginx state=started'
        when: 'ansible_host=="node02"'

```
# when example
#print i am a child when age is <18 and print i am an adult when age is >=18
```
---
- name: 'Am I an Adult or a Child?'
  hosts: localhost
  vars:
    age: 25
  tasks:
    - name: I am a Child
      command: 'echo "I am a Child"'
      when: 'age < 18'
    - name: I am an Adult
      command: 'echo "I am an Adult"'
      when: 'age >= 18'

```


