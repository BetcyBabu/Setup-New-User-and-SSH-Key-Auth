# Setup-New-User-and-SSH-Key-Auth

[root@ip-172-31-2-114 useradd]# cat user.var
---
user: betcybabu12345
publickey: "mykey.pub"
[root@ip-172-31-2-114 useradd]#
[root@ip-172-31-2-114 useradd]#
[root@ip-172-31-2-114 useradd]# cat useradd.yaml
---
- name: "Setup New User and SSH Key Auth"
  hosts: amazon
  become: true
  vars_files:
    - user.var
  tasks:
    - name: "Adding new user"
      user:
        name: "{{ user }}"
        create_home: true

    - name: "Adding SSH authorized key for the user account"
      authorized_key:
        user: "{{ user }}"
        key: "{{ lookup('file', '{{ publickey }}') }}"


[root@ip-172-31-2-114 useradd]#
