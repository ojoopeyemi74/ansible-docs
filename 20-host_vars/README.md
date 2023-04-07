# we created a host_vars folder in the root 

and we have created few file with either the <ip-address>.yaml , that is the ip address in our inventory
or we could use the hostname.yaml if we have hostname instead or we could use the dnsname.yaml

```
nano 172.31.37.191.yml
```

# we created some variables in above inside the 172.31.37.191.yml file

this variables has to do with the ubuntu OS 

```
apache_package_name: apache2
apache_service: apache2
php_package_name: libapache2-mod-php
```

# and for the CentOS host_vars 

this variables has to do with the CentOS
```
apache_package_name: httpd
apache_service: https
php_package_name: php
```

# we have refreneced to the variables in our play, d example below is for CentOS
```
- name: install httpd and php for CentOS servers
  tags: centos,httpd
  ansible.builtin.yum:
        name: 
         - "{{ apache_package_name }}"
         - "{{ php_package_name }}"
        state: latest
  when: ansible_distribution == "CentOS"

- name: start httpd ( CentOS)
  tags: apache,centos,httpd
  service: 
       name: "{{ apache_service }}"
       state: started
       enabled: yes
  when: ansible_distribution == "CentOS"
```
# we have refrenced to the variables from the host_vars to the Debian play
```
- name: install apache and php for Debian servers
  tags: apache,apache2,debian
  ansible.builtin.apt:
    name: 
    - "{{ apache_package_name }}"
    - " {{ php_package_name }}"
    state: latest     
  when: ansible_distribution == "Debian"

```