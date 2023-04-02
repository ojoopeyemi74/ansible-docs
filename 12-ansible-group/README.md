# using groups in ansible to target different servers
for example you have a webserver group , database server groups and file server groups

in the inventory file you should have something like this 
```
[web_servers]
13.41.194.243 ansible_user=admin

[db_servers]
13.42.39.183 ansible_user=admin

[file_servers]
13.41.201.250 ansible_user=centos
```

# in this example we have been able to use pre_tasks to make sure this particular task runs first in our playbook

# we have also been able to use the group to target the specific host in our already definned inventory
```
---
- hosts: all
  become: true
  pre_tasks:

  - name: install updates (centOS)
    ansible.builtin.yum:
     update_only: yes
     update_cache: yes
    when: ansible_distribution == "CentOS"

  - name: install updates ( Debian)
    ansible.builtin.apt:
     upgrade: dist
     update_cache: yes
    when: ansible_distribution == "Debian"
 
- hosts: web_servers
  become: true
  tasks:
    - name: install apache and php for Ubuntu servers
      ansible.builtin.apt:
        name: 
         - apache2
         - libapache2-mod-php
        state: latest
      when: ansible_distribution == "Debian"

    - name: install httpd and php for CentOS servers
      ansible.builtin.yum:
        name: 
         - httpd
         - php
        state: latest
      when: ansible_distribution == "CentOS"

- hosts: db_servers
  become: true
  tasks:
    - name: install mariadb package (CentOS)
      ansible.builtin.yum:
       name: mariadb
       state: latest
      when: ansible_distribution == "CentOS"

    - name: install mariadb package on (Debian)
      ansible.builtin.apt:
       name: mariadb-server
      when: ansible_distribution == "Debian"

- hosts: file_servers
  become: true
  tasks:
    - name: install samba package
      package: 
       name: samba
       state: latest

```