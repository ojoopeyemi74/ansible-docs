# in this section we will be using the lineinfile module 

we use the lineinfile module to add a line in a file on our target server



```
    - name: change and email address
      tags: apache,apache2,httpd
      lineinfile:
        path: /etc/httpd/conf/httpd.conf # here is the path we would like to add a line on our server
        regexp: '^ServerAdmin'  # we use the regexpresion to specify the line we want to add a new file
        line: ServerAdmin somebody@somewhere.net # and this is the line we want to add
      when: ansible_distribution == "CentOS"
      register: httpdupdate      # we use register the file using the register with the new name, it could be an arbitary name

    - name: restart httpd
      tags: centos,apache,httpd
      service:
       name: httpd    # here we specify the service 
       state: restarted
      when: httpdupdate is changed  # we use the when statement here as when the httpd is changed, as we have changed in up in the previous play in the register

```