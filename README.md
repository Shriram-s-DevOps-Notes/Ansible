# ANSIBLE 

# Configuration Management:
* Configuration Management refers to the process of systematically handling changes to a system rather than manually.

* A configuration management tool is a software solution designed to automate managing and maintaining the configuration of software applications and infrastructure components. 
* It helps ensure consistency, reliability, and efficiency in the deployment and operation of IT systems. The primary goals of configuration management tools include:

Example:
* Ansible
*  Puppet
* Chef
*  Saltstack

**Advantages:**
- Increasing up time.
-  Improve performance.
- Prevent errors.
- Cost Reduction and Risks.
- Improve software/hardware ownership knowledge and reliability
- Proactively identify the high-risk failure points
- Execute documentation management solutions for operational systems
- Better understanding of change windows without the need to research each from scratch

Push Based Vs Pull Based
------

![Screenshot 2023-12-19 164008](https://github.com/Shriram-s-DevOps-Notes/Ansible/assets/110009356/30474acb-dac8-432a-bf78-088d09504003)


**Pull Based**: Agents on the server periodically check for the configuration information from the central server (Master).

 **Push Based:** Central server pushes the configuration information on target servers. Control when the changes are made on the servers.

| Feature                       | Push-based tools (e.g., Ansible,Saltstack)                | Pull-based tools (e.g., Puppet, Chef)      |
|-------------------------------|-------------------------------------------------|--------------------------------------------|
| **Architecture**              | Agentless, central controller pushes changes    | Master-agent, nodes pull changes from server |
| **Communication**             | SSH or other protocols                          | Agent daemon                                |
| **Performance**               | Faster, simpler, more flexible                  | More scalable, reliable, consistent        |
| **Complexity**                | Lower, easier to learn and use                  | Higher, require more programming knowledge |
| **State Management**          | No built-in state management                    | Maintain state file to track resources     |
| **Idempotency**               | Optional, depends on the tasks                  | Mandatory, ensure desired state            |
| **Use Cases**                 | Configuration management and automation         | Infrastructure provisioning and management |
- Saltstack

# ANSIBLE 
### What is ansible?
-------
- Ansible is an open-source automation tool that simplifies various IT tasks, including configuration management, application deployment, and task automation. 
- It is designed to be simple, consistent, and agentless, allowing for easy configuration and management of systems. 
- Ansible uses declarative language to describe the desired state of the system, making it easy to understand and maintain.

### How Ansible works?
*  Ansible works on existing SSH connections.
* Ansible doesn't require to open any network port or no need required any agent installation.
* We need to enable password-less authentication (Key exchanging)

### Use of Ansible:
------
**Configuration Management:** 
Ansible is widely used for  configuring and managing the state of systems. It enables you to define the desired configuration of servers, ensuring consistency across your infrastructure.

**Application Deployment:** Ansible automates the deployment of applications, making the process more reliable and efficient. It can handle tasks such as copying files, installing dependencies, and restarting services.

**Task Automation:** With Ansible, you can automate repetitive tasks and workflows, saving time and reducing the chance of human error. This is particularly useful for routine maintenance, backups, and system updates.

**Orchestration:** Ansible facilitates the orchestration of complex workflows involving multiple systems. It allows you to coordinate tasks and manage dependencies, ensuring a smooth execution of processes.

**Infrastructure as Code (IaC):** Ansible supports Infrastructure as Code, enabling you to define and manage infrastructure using code. This enhances the reproducibility, scalability, and version control of your infrastructure.

***Integration with Cloud Services:** Ansible seamlessly integrates with cloud platforms like AWS, Azure, and Google Cloud. This makes it a valuable tool for managing cloud resources and deploying applications in cloud environments.

----
Ansible Vs Chef vs Puppet
-------------------------------------
| Feature                 | Ansible                                        | Puppet                                      | Chef                                      |
|-------------------------|------------------------------------------------|---------------------------------------------|-------------------------------------------|
| **Language**            | YAML                                           | Puppet DSL (Declarative)                     | Ruby DSL (Declarative and Procedural)      |
| **Agent-Based**         | No                                             | Yes                                         | Yes                                       |
| **Master-Node Setup**    | Not required                                   | Required                                    | Required                                  |
| **Learning Curve**       | Low                                            | Moderate to High                            | Moderate to High                          |
| **Ease of Use**          | Easy                                           | Moderate                                    | Moderate                                  |
| **Architecture**         | Agentless                                      | Master-Slave (Client-Server)                | Master-Slave (Client-Server)              |
| **Community Support**    | Large and Active                               | Large and Active                            | Large and Active                          |
| **Configuration Syntax** | YAML                                           | Puppet DSL                                  | Ruby DSL                                  |
| **Flexibility**          | Broad range of modules and integrations        | Rich set of modules and Puppet Forge        | Broad range of cookbooks and resources   |
| **Scalability**          | Scales well for managing large infrastructures | Scales well for large environments         | Scales well for large environments 
---------------------
Terraform VS Ansible
-----------------------------------------



| Feature                       | Terraform                                       | Ansible                                    |
|-------------------------------|-------------------------------------------------|--------------------------------------------|
| **Purpose**                   | Infrastructure provisioning and management     | Configuration management and automation   |
| **Declarative/Imperative**    | Declarative                                     | Imperative                                |
| **Language**                  | HashiCorp Configuration Language (HCL)          | YAML                                       |
| **Agent Requirement**         | No agents required                             | Agentless, communicates over SSH           |
| **Target Scope**              | Infrastructure resources                        | Software configuration and application deployment |
| **Multi-Cloud Support**       | Yes, cloud-agnostic                            | Yes, can manage diverse infrastructure    |
| **Execution Model**           | Plan and apply                                 | Playbook execution                        |
| **State Management**          | Yes, maintains state file to track resources    | No built-in state management              |
| **Resource Lifecycle**        | Create, update, delete resources                | Configure and manage existing resources  |
| **Use Cases**                 | Provisioning virtual machines, networks, etc.  | Configuring servers, deploying applications|
| **Learning Curve**            | Moderate to high for complex scenarios          | Generally lower due to simpler syntax    |
| **Community and Ecosystem**   | Large and active community, extensive provider support | Large community, rich module ecosystem    |
