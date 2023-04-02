# we could imporove our ansible playbook by using list

```
---
- hosts: all
  become: true
  tasks: 
   
  - name: update repository index
    apt: 
     update_cache: yes
    when: ansible_distribution == "Debian"

  - name: install apache2 and php packages
    ansible.builtin.apt:
      name: 
       - apache2  
       - libapache2-mod-php
      state: latest
    when: ansible_distribution == "Debian"
  

  - name: update repository index on CentOS
    yum:
      update_cache: yes
    when: ansible_distribution == "CentOS" 

  - name: Install all the packages
    yum:
       name:
       - httpd
       - php
       state: latest
    when: ansible_distribution == "CentOS"
  
```

  # we can also improve it better 

```
  ---
- hosts: all
  become: true
  tasks: 
 
  - name: install apache2 and php packages
    ansible.builtin.apt:
      name: 
       - apache2  
       - libapache2-mod-php
      state: latest
      update_cache: yes
    when: ansible_distribution == "Debian"
  

  - name: Install all the packages
    yum:
       name:
       - httpd
       - php
       state: latest
       update_cache: yes
    when: ansible_distribution == "CentOS"
  
```