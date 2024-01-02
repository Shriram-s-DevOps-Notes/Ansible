Ansible inventory file:
-----------------------
Syntax:

<server-name> ansible_host=<server-IP> ansible_connection=ssh

Ex:
```
ec2-user ansible_host=34.229.92.118 ansible_user=ansadmin
ubuntu   ansible_host=172.31.4.74   ansible_user=ansadmin
``` 
----------------------------------------------     
**Different Inventory Format Types**

1. INI(Initialization) Format
2. YAML Format

If you want to create the group of the servers
1. **The INI format** is the simplest and
most straightforward.

Ex: 

```
ec2-user ansible_host=172.31.38.128 ansible_connection=ssh
ubuntu ansible_host=172.31.4.74 ansible_connection=ssh
 
[web-server]
ec2-user
 
[db-server]
ubuntu

[all-servers:childrens]
web-server
db-server 
```
2. The **YAML format** is more structured and flexible than the INI  format.   
                                      
Ex-1:
```
all:
    children:
        webservers:
            hosts:
                web1.example.com:
                web2.example.com:
        dbservers:
            hosts:
                db1.example.com:
                db2.example.com:
```

Ex-2 
```
all:
    children:
        webservers:
            children:
                webservers_us:
                    hosts:
                        server1_us.com:
                            ansible_host: 19 168.8.101
                        server2_us.com:
                            ansible_host: 192.168.8.102
                webservers_eu:
                    hosts:
                        server1_eu.com:
                            ansible_host: 10.12.0.101
                        server2_eu.com:
                            ansible_host: 10.12.0.102
```
