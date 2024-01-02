
## Ansible Playbooks

- The Ansible playbook is a YAML (Yet Another Markup Language) document, which is a set of plays. A play is a specific task. It uses the /usr/bin/ansible-playbook command to execute the playbooks.

* Ansible playbooks are a way to send commands to remote computers in a scripted way.

* Each playbook
function. Ansible does this through something called tasks, which are module calls. A task can be anything like

1. Execute a command

2. Run a script

3. Install a package

4. Shutdown/Restart
---
### Ad hoc command Vs Playbook
* Ansible can be used in either Ad-Hoc or Playbook mode.
* The ad-hoc mode allows direct management of your hosts by executing single-line commands and leveraging Ansible modules. 
* Each Ansible playbook contains one or more plays to help you perform functions on different hosts.
---
### Playbook Sections
Ansible playbooks are divided into 4-sections. 

1. **Target Section:** In this section we have defined hosts against which the playbook task has to execute.
2. **Variable Section:** In this section we have defined the variables used by plays.
3. **Task Section:** In this section we can list all modules that we need to run in the order.
4. **Handler Section:** Handlers are ansible plays that are executed only when someone notifies.

Example:

```
---
# Target Section
- name: Playbook For Installing httpd service
  hosts: all
  become: yes
  become_user: root
  gather_facts: False

# Variable Section:
  vars:
    pkg_name: httpd

# Task Section:
  tasks:
  - name: Ensure Apache is at the latest version
    yum:
     name: ' {{ pkg_name }} '
     state: latest
     notify: restart httpd

# Handler Section:
handlers:
  - name: restart httpd
    service:
    name: httpd
    state: restarted
```
* As we discussed earlier yum, service..etc are called modules.
---
#### hosts:
* In the "hosts" section you have to specify in which host you want to run this playbook
* For example if I want to run this playbook locally I will set the host as **"localhost"**
* If you want to run the playbook on all the hosts then set the hosts to **"all"**
* You can set the host to a particular group also.
---
#### become:
*  Become Word will allow Ansible playbook root privileges.
* become method can also be set to **"su"** or **"sudo"** or **"root"**
--- 
#### gather_facts
* When you run the playbook you may notice that even if you didn't mention there will be a section called gathering facts.
* gather_fact will collect all the details like IP address, DNS server details, server architecture, and many more details from all the servers that you mentioned in your hosts section.
* **Note: Fact gathering will only collect the facts from the servers that we mentioned in the "hosts" section.**
```
[root@ip-172-31-32-49 playbooks]# ansible-playbook test_1.yml

PLAY [all] ************************************************************************************************************************************

TASK [Gathering Facts] ************************************************************************************************************************
ok: [ubuntu]
[WARNING]: Platform linux on host ec2-user is using the discovered Python interpreter at /usr/bin/python, but future installation of another
for more
ok: [ec2-user]
```
---
#### ignore_errors: yes 
* **The ignore_errors: yes** directive is set at the playbook level. This means that if any task fails (raises an error), Ansible will continue executing subsequent tasks rather than stopping the playbook. 

---

* To list all the modules in Ansible run the below command.
```
ansible-doc -l
```

* To run the playbook execute the command
```
ansible-playbook <playbook file name>
```
---
### How to Verify Playbooks in Ansible?

* Imagine you are running a playbook directly on 10 servers and due to some error in your playbook, all 10 servers got shut down.
* To overcome this problem we have an option in Ansible to check whether the playbook is going to work as we planned.
* There are 2 types of verification
1. Check Mode
2. Diff Mode

1. Check mode:
* Ansible's "dry run" where no actual changes are made on hosts.
* Allows preview of playbook changes without applying them
* Use the --check option to run a playbook in check mode
* Syntax:
```
ansible-playbook <playbook-name> --check
```

2. Diff Mode: 
* Provides a before-and-after comparison of playbook changes
* Understand and verify the impact of playbook changes before applying them
* Utilize the --diff option to run a playbook in diff mode
* Syntax:
```
ansible-playbook <playbook-name> --check --diff
```

* Other than diff and check we have another mode that will check syntax check.
* Syntax mode ensures playbook syntax is error-free

```
ansible-playbook <playbook-name> --syntax-check
```

## Variables in Ansible:
* In Ansible, variables provide much-needed flexibility in Playbooks, templates, and inventories.

1. **String variables** 
* String variables in Ansible are sequences of characters.
* They can be defined in a playbook, inventory, or passed as command line arguments.

Ex:
```
username: "admin"
```
2. **Number variables** 
* Number variables in Ansible can hold integer or floating-point values.

* They can be used in mathematical operations.
```
max_connections: 100
```
3. **Boolean Variables**

* Boolean variables in Ansible can hold either true or false.
* They are often used in conditional statements.

Certainly! Here's the information in a two-row format with the rest as columns:

| Valid Values                         | Truthy Values                          |
|--------------------------------------|----------------------------------------|
| True, 'true', 't', 'yes', 'y', 'on', '1', 1, 1.0 | False, 'false', 'f', 'no', 'n', 'off', '0', 0, 0.0 |

Ex:
```
debug_mode: true
```
---
* **Ansible variables can be classified into two categories:**

1. System-defined variables (built-in variables):
```
hostvars, groups, group_names, etc.
```
2.  User-defined variables (custom variables):
```
myvar, var, var200, tune_01 etc.
```
-----
### Using Variables in Ansible:
* Variable names can have letters (alphabets), numbers & underscores. 
* Variable names should always start with letters, not with number(s).
* There shouldn't be any spaces or - present in variable names.
Examples  of **acceptable variable names** include:
```
turntable, turn_table, turntable01, turntable_01
```
The names below **do not qualify as valid variable names:**
```
turn table, turn-table, 01turntable
```

* Variables can be stored in inventory files also

```
web1 ansible_host=172.20.1.100
web2 ansible_host=172.20.1.101  dns_server=10.5.5.4
web3 ansible_host=172.20.1.102
```
or 

```
/etc/ansible/hosts
web1 ansible_host=172.20.1.100
web2 ansible_host=172.20.1.101  dns_server=10.5.5.4
web3 ansible_host=172.20.1.102

[web_servers]
web1
Web2
web3

[web_servers:vars]
dns_server=10.5.5.3
```
 ----
### Variables with Arrays

From the below examples we are using variables with arrays

Ex-1:
```
---
 - hosts: all
   become: yes
   vars:
    students:
      - Dboss
      - DSboss
   tasks:
    - name: Greetings
      debug:
        msg: "Welcome {{ students }} "
```
We can call a single array element if want. The 1st array number start with **0**

Ex-2:
```
---
 - hosts: all
   become: yes
   vars:
    students:
      - Dboss
      - DSboss
   tasks:
    - name: Greetings
      debug:
        msg: "Welcome {{ students[1] }} "
```
---
### Variables with Dictionary
* In Ansible, dictionaries are defined using YAML syntax.
* Dictionary's are key-value pairs 
```
---
 - name: Access Dictionary Variable Playbook
   hosts: web_servers
   vars:
    user:
     name: "admin"
     password: "secret"
   tasks:
   - name: Display the entire user dictionary variable
     debug:
      var: user
   - name: Access specific values in the dictionary
     debug:
       msg: "Username: {{ user.name }}, Password: {{ user.password}}"
```
* Suppose you want to call 1st value.
```
---
 - hosts: all
   become: yes
   vars:
    students:
      Dboss: 'katera'
      DSboss: 'martin'
   tasks:
    - name: Greetings
      debug:
        msg: " {{ students['Dboss'] }} "
```
----
### Register Variables

* If a user wants to store the variable then use Register
Ex:
```
---
 - name: Check /etc/hosts file
   hosts: all
   tasks:
   - shell: cat /etc/hosts
     register: result

   - debug:
     var: result
```
* The 1st play will cat the /etc/hosts in all the remote servers and it will store the output in the **result** variable.

* The 2nd play will display the output stored in the register module.

* The second method of capturing the output 
```
ansible-playbook <playbook-name> -v
```
-v = verbose

----
### Command line variable

*  Variables can be passed through the command line also. This is also called as **GLOBAL VARIABLE**
```
ansible-playbook <playbook-name> -e <variable's>
```
or
```
ansible-playbook <playbook-name> --extra-vars <variable's>
```
---
### Conditionals Ansible

In Ansible, conditions are used to control the flow of tasks and playbooks based on certain criteria. One common way to use conditions is through the "when" statement. The "when" statement allows you to execute a task only if a specified condition is true.

Here's a basic example:

```yaml
---
- name: Example playbook with condition
  hosts: all
  tasks:
    - name: Ensure a directory exists
      file:
        path: /path/to/your/directory
        state: directory
      when: not directory_exists.stat.exists
```

In this example:
- The task creates a directory only if the specified path doesn't exist.
- The condition (`when: not directory_exists.stat.exists`) checks whether the directory already exists.

You can use various conditions in Ansible, such as comparing values, checking the presence of a file, or validating the output of a command. Here's a more complex example using a variable:

```yaml
---
- name: Example playbook with variable condition
  hosts: all
  vars:
    environment: production
  tasks:
    - name: Ensure a task runs in the production environment
      debug:
        msg: "This task runs in the production environment"
      when: environment == 'production'
```

In this example, the task will only execute if the variable "environment" is set to "production."

You can use **or**, **and** conditions.
```
 ---
 - name: Install NGINX 
   hosts:
   tasks:

   - name: Install NGINX on Debian
     apt: 
        name: nginx
        state: present
    when: ansible_os_family == “Debian”  and ansible_distribution_version == “16.04”

   - name: Install NGINX on Debian
     yum: 
        name: nginx
        state: present
    when: ansible_os_family == “RedHat”  or ansible_os_family == “SUSE”

```
---
### LOOPS 
*  Ansible loops are a powerful feature that allows you to iterate over a set of items in a playbook.
* We can execute the same task repeatedly we can go for loops.
* Ansible loop provides a lot of methods to repeat certain tasks until a condition.
- with_list
- with_items
- with_indexed_items
- with_flattened
- with_together
- with_dict
- with_sequence
- with_subelements
- with_nested/with_cartesian
- with_random_choice

Example:
```
---
 - hosts: localhost 
   become: yes
   tasks:
   - name: Install yum package in Ansible example
     yum:
      name: "{{ item }}"
      state: present
     with_items:
        - git
        - httpd
```
### IMPORTANT_NOTE:
- **After Ansible version 2.9 Red-Hat replaced "with_items" with "loop"**

**Ansible loop with Index**

* In some scenarios knowing the index value might come in handy. We can use the
“with indexed_items” for this. 
* The loop index will be available at item 0 and the
value will be available at item 1. The index value starts at zero as usual.

Example:
```
---
 - hosts: localhost
  tasks:
  - name: Ansible loop with index example
    debug:
      msg: "echo loop index at {{ item.0 }} and value at {{item.1}}"
    with_indexed_items:
    - "hello1"
    - "hello2"
    - "hello3"
```
