# Loops in Ansible
lets take an example of using the user module to create  users in a target node
e.g
```
-
  name: create users
  hosts: localhosts
  tasks:
   - user: name= joe              state=present
   - user: name=ralph             state=present
   - user: name=ope               state=present
```
# loop examples
this is not a very elegant way of creating multiple users in your play as there is a lot of duplication

A better way of doing this is having loop

loop is a looping directive that execute multiple numbers of time

example:
```
 -
  name: create users
  hosts: localhosts
  tasks:
   - user: name= '{{ item }}'       state=present
     loop:
       - joe
       - ralph
       - ope
```
# we can easily visialize the {{item}} and the loop in this way
```
- var: item=joe
  user: name= "{{ item}}"         state=present

- var: item=ralph
  user: name= "{{ item}}"         state=present

- var: item=ope
  user: name= "{{ item}}"         state=present
```
# what is we want to specify user ID as well in our tasks
```
e.g name=joe  , name=ralph , name=ope    and the uid=101 , uid=102 , uid=103
 -
  name: create users
  hosts: localhosts
  tasks:
   - user: name= '{{ item.name }}'  state=present  uid='{{item.uid}}'
     loop:
      - name: joe
        uid: 101
      - name: ralph
        uid: 102
      - name: ope
        uid: 103

    OR

 -
  name: create users
  hosts: localhosts
  tasks:
   - user: name= '{{ item.name }}'  state=present  uid='{{item.uid}}'
     loop:
      - {name: joe, uid:101}
      - {name: ralph, uid:102}
      - {name: ope, uid:103}
```
# we could also another way to create loops in playbook using with_*

as the loop derective is newly added in asible

exaples:
```
         with_items:
         with_file:
         with_url:
         with_mongodb:
```
you can always have a lookup plugins which can be with the with_* directive