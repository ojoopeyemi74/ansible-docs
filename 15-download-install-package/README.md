# In this section we will be downloading and installing a package on a server using ansible( installing terraform as an example)
firstly the package we are dowlinging might be a zip package
so we are going to first install unzip

```
- hosts: workstations
  become: true
  tasks:
    - name: install unzip
      package:
        name: unzip
```

# we will search for the package we want to download from the internet, right click on the software and copy the address and paste it in the src section 
 
we will specifyy the destination on our target server in this case we want terraform to be stored on /usr/local/bin

```
  - name: install terraform
      unarchive:
        src: https://releases.hashicorp.com/terraform/1.4.4/terraform_1.4.4_linux_amd64.zip
        dest: /usr/local/bin
        remote_src: yes
        mode: 0755
        owner: root
        group: root

```