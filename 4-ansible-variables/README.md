# we use variables to store information that varies with each hosts

# example
```
web1 ansible_host=server1.company.com ansible_connection=ssh ansible_ssh_pass=Puw@
web2 ansible_host=server1.company.com ansible_connection=ssh ansible_ssh_pass=Puw@
```
# another example
```
-
  name: Add DNS server to resolv.conf
  hosts: localhost
  vars:                       # variable defined
    dns_server: 10.0.2.0.4
  tasks:
    - lininfile:
        path: /etc/reslov.conf
        line: 'nameserver 10.0.2.0.4'
```
# to use the variable having the variable in the play
```
-
  name: Add DNS server to resolv.conf
  hosts: localhost
  vars:                       # variable defined
    dns_server: 10.0.2.0.4
  tasks:
    - lininfile:
        path: /etc/reslov.conf
        line: 'nameserver {{ dns_server }}'  # replace the varrible in a {{}}
```
# another example, having the variable in the play
```
---
- hosts: localhost
  tasks:
  vars:
   car_model: BMW M3
   country_name: USA
   title: 'Systems Engineer'
   tasks:
    - command: 'echo "My car is {{ car_model }}"'
    - command: 'echo "I live in the {{ country_name }}"'
    - command: 'echo "I work as a {{ title }}"'

```
# another example
```
- 
 name: Setfirewall configuration
 hosts: web
 tasks:
  - firewalld:
     service: https
     permanent: true
     state: enabled

 - firewalld:
     port: '{{ http_port }}'/tcp
     permanent: true
     state: disabled

 - firewalld:
     port: '{{ snap_port }}'/udp
     permanent: true
     state: disabled

 - firewalld:
     port: '{{ inter_ip_range }}'/24
     permanent: true
     state: enabled
```
# we can have the variables in the inventory file
```
web http_port=8081 snap_port=161-162 inter_ip_range=19.02.20.3
```
# Or we can move the varibale to a file names - web.yaml
```
http_port: 8081
snap_port: 161-162
inter_ip_range: 19.02.20.3


# this format is called jinja2 Templating {{ }} you should enclose it with ' ' '{{  }}'
but when its between sentence there is no need to enclose it with ''

```




