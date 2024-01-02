

## Insatalling ansible on **"UBUNTU"**
### Control Machine = Ubuntu
### Remote Machine = Amazon Linux
---
### 1.  Remote Machine**

Update the package list:
   ```bash
   yum update
   ```

Upgrade installed packages:
   ```bash
   yum upgrade
   ```

Add user to sudoers file:
   ```bash
   echo "<user-name> ALL=(ALL) ALL" >> /etc/sudoers
   ```

Allow the user to run sudo without a password:
   ```bash
   echo "<user-name> ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers
   ```

Enable password authentication in SSH:
   ```bash
   sed -ie 's/PasswordAuthentication no/PasswordAuthentication yes/' /etc/ssh/sshd_config
   ```

Restart SSH service:
   ```bash
   systemctl restart sshd
   ```

Set a password for the root user and ansible user:
   ```bash
   passwd root
   ```

   ```bash
   passwd <user-name>
   ```

------
### Control Node (Ubuntu):

Update the package list:
   ```bash
   apt update
   ```

Upgrade installed packages:
   ```bash
   apt upgrade
   ```

Add user to sudoers file:
   ```bash
   echo "<user-name> ALL=(ALL:ALL) ALL" >> /etc/sudoers
   ```

Enable password authentication in SSH:
   ```bash
   sed -ie 's/PasswordAuthentication no/PasswordAuthentication yes/' /etc/ssh/sshd_config
   ```

Reload SSH service:
   ```bash
   service sshd reload
   ```

Install Ansible:
   ```bash
   apt-get install ansible
   ```

Generate an SSH key pair:
   ```bash
   ssh-keygen
   ```

Copy the SSH key to the remote node:
   ```bash
   ssh-copy-id root@<IP-OF-Remote-Node>
   ```

Test the connection:
   ```bash
   ssh root@<IP-OF-Remote-Node>
   ```
Create Password for both root as well as for user which you created

   ```
   passwd root
   ```

   ```bash
   passwd <user-name>
   ```


