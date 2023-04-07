# roles in ansible helos us to better slip up our tasks
and also to start with toles on ansible you should create a folder called roles
next inside the role folder create different roles e.g base folder, web_server folder, db_server folder etc
and next you have to create subfolder called tasks inside each play foler
next inside the each tasks folder you create file named main.yaml

mkdir roles
cd roles 
mkdir base
mkdir web_servers
mkdir db_servers
mkdir file_servers

mkdir web_servers/tasks
mkdir db_servers/tasks

touch web_server/tasks main.yaml
touch db_server/tasks main.yaml

# we can also create files folder in our role play folder if we need to copy a file from the folder

# in our *.yaml file we have specify the roles as we will create the role folder which our yaml file will point to to be able to execute our tasks

```
- hosts: all
  become: true
  roles: 
   - base

- hosts: workstations
  become: true
  roles:
   - workstations

- hosts: web_servers
  become: true
  roles:
   - web_servers

- hosts: db_servers
  become: true
  roles:
   - db_servers

- hosts: file_servers
  become: true
  roles:
   - file_servers

```