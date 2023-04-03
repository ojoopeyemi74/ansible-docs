# you can use tags in your playbook to target a specific task to run or refresh and not the others
by specifiying a tag will make your playbook run faster as it will only refresh that specified task
even if you have 100 tasks in your playbook

#example of tags

```
---
- hosts: all
  become: true
  pre_tasks:

  - name: install updates (centOS)
    tags: always
    ansible.builtin.yum:
     update_only: yes
     update_cache: yes
    when: ansible_distribution == "CentOS"

  - name: install updates ( Debian)
    tags: always
    ansible.builtin.apt:
     upgrade: dist
     update_cache: yes
    when: ansible_distribution == "Debian"
 
- hosts: web_servers
  become: true
  tasks:
    - name: install apache and php for Debian servers
      tags: apache,apache2,debian
      ansible.builtin.apt:
        name: 
         - apache2
         - libapache2-mod-php
        state: latest
      when: ansible_distribution == "Debian"

    - name: install httpd and php for CentOS servers
      tags: centos,httpd
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
      tags: mariadb,centos,db
      ansible.builtin.yum:
       name: mariadb
       state: latest
      when: ansible_distribution == "CentOS"

    - name: install mariadb package on (Debian)
      tags: db,mariadb,debian
      ansible.builtin.apt:
       name: mariadb-server
      when: ansible_distribution == "Debian"

- hosts: file_servers
  become: true
  tasks:
    - name: install samba package
      tags: samba
      package: 
       name: samba
       state: latest

```
# to run the tags you use the below 

with this only the tasks with debian will run or refresh
```
ansible-playbook filename.yaml --tags debian -i inventory
```

# you can specify 2 or more tags 
with this example it will run on the specified tasks

```
ansible-playbook filename.yaml --tags "debian,httpd" -i inventory
```
# you can list all your tags using
```
ansible-playbook site.yml --list-tags -i inventory 
```