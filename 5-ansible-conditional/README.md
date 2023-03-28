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
