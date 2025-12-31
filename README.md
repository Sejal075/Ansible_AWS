# Ansible_AWS

## 📌 Project Overview

This project demonstrates infrastructure automation using Ansible by configuring a master–slave architecture on AWS EC2 (Ubuntu).The Ansible control node (master) is used to automatically install and configure Nginx on a slave node, eliminating the need for manual setup.
The project showcases real-world DevOps practices such as configuration management, SSH automation, and privilege escalation using Ansible.

## 🏗 Architecture

1. Ansible Master (Control Node)
   AWS EC2 (Ubuntu)
   Ansible installed
   Executes playbooks

2. Ansible Slave (Managed Node)
   AWS EC2 (Ubuntu)
   Managed remotely via SSH
   Nginx installed using Ansible playbook

## 🛠 Tools & Technologies Used

1. AWS EC2
2. Ubuntu Linux
3. Ansible
4. SSH
5. Nginx
6. YAML

## 📂 Project Structure
ansible-nginx-project/nginx.yml

## ⚙️ Prerequisites

1. Two EC2 instances (Ubuntu)
   One as Master
   One as Slave
2. SSH access between Master and Slave
3. Python 3 installed on both nodes
4. Ansible installed on Master
5. Passwordless sudo configured for ansible user on Slave

## 🔑 Configuration Steps
1️⃣ Install Ansible on Master
   sudo apt update
   sudo apt install ansible -y

2️⃣ Create ansible User on Both Nodes
   sudo adduser ansible
   sudo usermod -aG sudo ansible

3️⃣ Configure Passwordless SSH
   From Master:
   ssh-keygen
   ssh-copy-id ansible@<slave-private-ip>

4️⃣ Configure Inventory File
   Edit:
   sudo nano /etc/ansible/hosts
   Add:
   [slaves]
   slave1 ansible_host=<slave-private-ip> ansible_user=ansible

5️⃣ Enable Passwordless Sudo on Slave
   On Slave:
   sudo visudo
   Add:
   ansible ALL=(ALL) NOPASSWD:ALL
   Verify:
   su - ansible
   sudo whoami
   Expected output:
   root

## 📜 Ansible Playbook
nginx.yml
---
- name: Install nginx on slave
  hosts: slaves
  become: yes
  tasks:
    - name: Install nginx
      apt:
        name: nginx
        state: present
        update_cache: yes
...

▶️ Run the Playbook
  From Master:
  ansible-playbook nginx.yml
✅ Verification
  On Slave:
  systemctl status nginx
  Or open in browser:
  http://<slave-public-ip>
  You should see the Nginx Welcome Page 🎉

## 🚀 Key Learnings

1. Ansible master–slave architecture
2. SSH key-based authentication
3. Inventory management
4. Privilege escalation using become
5. Automated package installation
6. Real-world DevOps workflow on AWS

## 🧑‍💻 Author

Sejal Umredkar
DevOps | Cloud | Automation

## Output 
Master node:
<img width="1366" height="631" alt="master" src="https://github.com/user-attachments/assets/e2d0ad79-14f2-497f-87ce-20b039b16056" />

Slave node: 
<img width="1366" height="636" alt="slave" src="https://github.com/user-attachments/assets/d84a6bdd-5db2-4048-9d80-40e068bf250a" />

Outcome:
<img width="1366" height="768" alt="outcome" src="https://github.com/user-attachments/assets/e7af2172-392a-467d-8b5f-aa7e632089bd" />

