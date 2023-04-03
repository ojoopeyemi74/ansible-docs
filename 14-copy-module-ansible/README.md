# you can use copy module to copy file from your local source to a remote target server

for example, we have a file in /home/admin/webpage/default_site.html on our local system
and we want to copy to /var/www/html/index.html on our remote server

```
- hosts: web_servers
  become: true
  tasks:
   - name: copy default html file for site
     tags: apache,apache2,httpd
     ansible.builtin.copy:
       src: /home/admin/webpage/default_site.html
       dest: /var/www/html/index.html
       owner: root
       group: root
       mode: 0644
       
```
