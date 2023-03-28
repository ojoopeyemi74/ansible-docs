```
# using the SERVICE module
you can manage start, stop, restart in a partticular order 

---
- name: hosts
  hosts: all
  become: yes
  tasks:
    - name: Execute a script
      script: /tmp/install_script.sh
    - name: Start httpd
      service:
        name: httpd
        state: started

```

```
# command module

the comman module is used to exect a comman on a remote node

---
- name: hosts
  hosts: all
  tasks:
    - name: execute comman `date`     # to run the date command on the host
      command: date
    - name: Execute resolv.conf contents
      command: cat /etc/resolv.conf
    - name: Display resolv.conf contents
      command: cat resolv.conf chdir=/etc   # to change directory before executing the command
    - name: Display resolv.conf contents
      command: mkdir /folder creates=/folder  # to used to create a folder if the folder doesnt exit

    - name: Copy file from source to destination
      command: src=/source_file dest=/destination   # to copy file from source to destination
```

```
## script 

runs a local script on a remote node after transferring it 

    - name: Run a script on remote server
      command: /some/local/script.sh -arg1 -arg2

```
```
### lineinfile
used to find a line in file and replace it or add it if it doesnt exist
- 
  name: Add DNS server to reslv.conf
  hosts: all
  tasks:
    - lineinfile:
        path: /etc/resolv.conf
        line: 'nameserver 10.0.25.10'

```


