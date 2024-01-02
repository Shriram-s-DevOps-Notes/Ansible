AD-HOCK COMMANDS:
----

### What is Ad Hock command ?
* Ad Hoc Commands are commands that you run from the command line without creating a playbook. They are useful for tasks that you need to perform quickly or for tasks that don't warrant the creation of a full playbook.

### 1.  Ping-module:To ping the servers

Syntax: ansible -i <inventory-file name> all -m ping
```
ansible -i host.txt all -m ping
```

If Inventory file is in /etc/ansible then

Syntax: 
```
ansible all -m ping
```
If you want to ping one group of server

Syntax: 
```
ansible -i host.txt <group-name> -m ping
```
Ex:
```
ansible -i host.txt web-server -m ping
```

To check the playbook weather it is syntactically correct

Syntax: 
```
ansible-playbook <playbook name> --syntax-check
```

### 2. Shell module: Using shell modules we can run all type of linux commands
- **This will display the partition details and IP address of the server**

```
ansible all -m shell -a "df -h && ip addr |grep inet" 
```          
- **This will list the details of /tmp folder**
```
ansible all -m shell -a "ls -ltr /tmp                            
```
### **3. File module:** File modules are used to run the file related opperations in client server.
*  "--become" = This will give root user privilage to ansible

* **To create new file in ansible remote machines**
```
ansible  all -m file -a "dest=/tmp/sunil.txt state=touch mode=755" --become 
```            
* **To delete the file from the remote servers**
``` 
Ex-2: ansible  all -m file -a "dest=/tmp/sunil.txt state=absent" --become                     
``` 
* **To create new directory in ansible remote machines** 
``` 
ansible all -m file -a "dest=/tmp/sunil state=directory mode=755" --become  
```          

### 4. Copy module: Copy module will copy the files from client server to remote server

* **To copy file from control machine to remote machine**

```
ansible all -m copy -a "src=/tmp/shriram.txt dest=/tmp" --become  
```                    

### 5. yum module: yum module is used to manage the packages in servers

* **This command will used to install nginx package in remote server's"**
```
ansible all -m yum -a "name=nginx state=present" 
```   
* **This command will used to Un-install nginx package in remote server's"**
``` 
ansible all -m yum -a "name=httpd state=absent" 
```     

### 6. Service module: Service module is used to run the service, to inspect the status of services

```
ansible all -m service -a "systemctl status nginx"
```

### 7. User module: User module is used to manage the users in server
* **To create users in servers**
```
ansible all -m user -a "name=jsmith home=/home/jsmith shell=/bin/bash state=present"  
``` 
* **To add a user to a different group**
```
ansible all -m user -a "name=jsmith group=iafzal"
```                                      
* **Deleting a user on remote clients**
```
ansible all -m user -a "name=jsmith home=/home/jsmith shell=/bin/bash state=absent"  
```              

### 8. Getting system information from remote clients
```
ansible all -m setup
```
