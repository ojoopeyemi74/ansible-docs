# In this section we will be using the service module 
in the previous sections we have been able to install httpd on our CentOD server, and we have manually 
started httpd
```
sudo systemctl start httpd

sudo systemctl status httpd
```
# when installing httpd on CentOS, it requires you to add the port you want you web to run on 
```
sudo firewall-cmd- list-all   ( we use this to list all)

sudo firewall-cmd --zone=public --add-port=80/tcp   ( we use this to add port 80)

```


# But in this section we will be starting the httpd using ansible service module

```
- name: install httpd and php for CentOS servers
      tags: centos,httpd
      ansible.builtin.yum:
        name: 
         - httpd
         - php
        state: latest
      when: ansible_distribution == "CentOS"

    - name: start httpd ( CentOS)
      tags: apache,centos,httpd
      service: 
       name: httpd
       state: started
       enabled: yes   # we set enabled to yes because we want httpd to always start whenever our system reboot
      when: ansible_distribution == "CentOS"

```
