ansible all -m apt -a update_cache=true --become --ask-become-pass

--become is for the sudo 

-m  - for the module
-a - for the argurment to the module 

ansible all -m apt -a name=vim-nox --become # for installing vim on a debian or ubuntu servers

# to see the packages that were installed
cd /var/log/apt  and cat the history.log

# to update all the server 
ansible all -m apt -a "upgrade=dist" --become -i inventory 

# to gather facts about your servers 
ansible all -m gather_facts -i inventory 
ansible all -m gather_facts -i inventory --limit <target-name or target-ip or group-name>

# we can gather facts of a particular detail by using grep |
example 

ansible all -m gather_facts -i inventory --limit 13.42.103.154 | grep ansible_distribution

ansible all -m gather_facts -i inventory --limit 13.42.103.154 | grep ansible_virtualization_type

# we use state: latest to get the latest version of our package installation 
example 
 - name: install apache2 package
    ansible.builtin.apt:
      name: apache2  
      state: latest     # latest for the latest version

# we use state: absent to remove/ uninstall packages from our servers
example

- name: install apache2 package
    ansible.builtin.apt:
      name: apache2  
      state: absent    # absent to uninstall packages

# we use state: present for current installation, and present is default even if not specified
example

- name: install apache2 package
    ansible.builtin.apt:
      name: apache2  
      state: present   # you can decide not to specify present as it is default anyway

