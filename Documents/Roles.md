## Roles

- Roles simplifies long playbooks by grouping tasks into smaller playbooks
OR
- The role are the way of breaking a playbook into multiple playbook files. This simplifies writing complex playbooks, and it makes them easier to reuse
- Writing ansible code to manage the same service for multiple environments creates more complexity and it becomes difficult to manage everything in one ansible playbook. Also sharing code among other teams become difficult. That is where Ansible Role helps solve these problems.
- Roles are like templates that are most of the time static and can be called by the playbooks
- Roles allow the entire configuration to be grouped in:
1. Tasks
2. Modules
3. Variables
4. Handlers

### How to create role ?

To create roles
*  Go to ControlNode
```
cd /etc/ansible/roles
```
- Make directory for each role
* ``` mkdir <role-name>```

Example:
```
mkdir apache
```
- Create sub-directory tasks within each directory
* ```mkdir <role-name>/tasks```

Example:

```
mkdir apache/tasks
```
- Create yml files within these sub-directories and write an playbooks for each tasks under below path
* ```touch <role-name>/tasks/<yaml-file>```

Example

```
touch apache/tasks/main.yml
```
main.yml
```
---
 - hosts: all
   become: true
   tasks:
   - name:  Install apache
     yum:
        name: httpd
        state: latest

   - name: Ensure Apache is running
     service:
        name: httpd
        state: started

   - name: Restart Apache
     service:
        name: httpd
        state: restarted
```
- Final format should looks like below under /etc/ansible/roles
```
<role-name>/tasks/<.yaml-file>
```
- Now If you want to use this roles below is the format.
```
---
 - name: Install packages
   hosts: all
   roles:
   - <role-name>
```
- You can add multiple roles at a time.

Example
```
---
 - name: Install packages
   hosts: all
   roles:
   - apache

```
