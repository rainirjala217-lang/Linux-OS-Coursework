# Week 4 Initial System Configuration and security
# Implementation Journal

# Introduction

In this phase of the assessment, I focused on deploying my Ubuntu Server and applying basic security configurations. I used an Ubuntu Desktop virtual machine as my workstation and an Ubuntu Server virtual machine as the target server. Both systems were created using VirtualBox and connected on the same internal network.

All configuration tasks on the server were performed remotely using SSH from my Ubuntu Desktop workstation. I did not perform any configuration directly on the server console. This approach follows the administrative constraint provided in the assignment.

# 1.SSH Configuration with Key-Based Authentication

# Server SSH Setup and Verification

<img width="1280" height="800" alt="week4" src="https://github.com/user-attachments/assets/59fc099e-d190-40a5-9c73-9f856ce614a7" />
<img width="1280" height="800" alt="week4 1" src="https://github.com/user-attachments/assets/f756f273-4e9c-48e1-8ea9-3c49074d62ba" />

The SSH service was set up on the Ubuntu server to allow secure remote access. The system was first updated using sudo apt update, and the OpenSSH server package was installed using sudo apt install openssh-server -y, which confirmed that SSH was already installed. The SSH service was then enabled using sudo systemctl enable ssh so it would start automatically. Finally, the status was checked using sudo systemctl status ssh, which showed that the SSH service was active and running on the server.

# SSH Key-Based authentication In Workstation:

<img width="1280" height="800" alt="dweek4 1" src="https://github.com/user-attachments/assets/544cf2d8-3739-4037-bc74-52cc90178c35" />

<img width="1280" height="800" alt="dweek4 1 1" src="https://github.com/user-attachments/assets/1b10e9be-4581-44e1-a7c2-4b2ba268d7e3" />

<img width="1280" height="800" alt="dweek4 1 2" src="https://github.com/user-attachments/assets/10cce5cd-e94b-4414-9f8b-a0864a87196f" />

<img width="1280" height="800" alt="dweek4 1 3" src="https://github.com/user-attachments/assets/cf39a57e-58b5-456b-9afb-64e15fcbea1b" />

From the workstation, I first generated an SSH key pair using the ssh-keygen -t ed25519 command, which created a private key on the workstation and a public key for authentication. After that, I used the ssh-copy-id nirjala@192.168.56.101 command to copy the public SSH key to the server, allowing key-based authentication. I then connected to the server from the workstation using the ssh nirjala@192.168.56.101 command to confirm that the SSH connection was working correctly. Once logged in to the server through SSH, I created a backup of the SSH configuration file using sudo cp /etc/ssh/sshd_config /etc/ssh/sshd_config.bak before making any changes. I opened the SSH configuration file using sudo nano /etc/ssh/sshd_config to update the security settings. After editing the file, I checked the configuration for errors using sudo sshd -t. Finally, I restarted the SSH service using sudo systemctl restart ssh so that the new configuration changes could take effect.

# 2. Configure a Firewall Permitting SSH from One Specific Workstation Only

Improve the security of the server, a firewall was configured to restrict SSH access so that only one specific workstation is allowed to connect. This helps prevent unauthorized access while still allowing secure remote administration. All firewall configuration was completed remotely by connecting to the server via SSH from the workstation.

<img width="1280" height="800" alt="week4 2" src="https://github.com/user-attachments/assets/b3e192b6-bb2e-44db-bc31-83d34ea91878" />

<img width="1280" height="800" alt="week4 2 1" src="https://github.com/user-attachments/assets/6e9cb9ae-4359-4deb-9329-b152802b5456" />

<img width="1280" height="800" alt="week4 2 2" src="https://github.com/user-attachments/assets/b7b25288-c647-45e1-89f1-ffa6659c6131" />

<img width="1280" height="800" alt="week4 2 3" src="https://github.com/user-attachments/assets/27742f46-5337-40b3-a0fa-3f3cc0288ec9" />

After logging into the server using SSH, I configured the firewall using UFW to improve security. I set the default firewall policy to block all incoming connections and allow outgoing traffic. Then, I added a rule to allow SSH access only from my workstation IP address on port 22. After enabling the firewall, I verified the configuration using UFW status commands. The results confirmed that the firewall was active and SSH access was restricted to the specified workstation only.

# 3. User Management and Privilege Management

The purpose of this task was to manage users securely by creating a non-root administrative user and assigning appropriate privileges. This reduces the need to use the root account directly and follows best practices for system security. All commands were executed on the server after connecting remotely via SSH from the workstation

<img width="1280" height="800" alt="week4 3" src="https://github.com/user-attachments/assets/fc15b6ec-9c00-48e0-8c71-360c3958e1e2" />

In here, I created a new user on the server using the adduser command, which also set up the user’s home directory and password. After creating the user, I added the user to the sudo group using the usermod -aG sudo command so that the user can run administrative commands when needed. Finally, I used the groups command to confirm that the new user was successfully added to the sudo group, which verifies that the user has administrative privileges on the system

# 4. SSH Access Evidence

To verify SSH access, I connected to the server remotely from my workstation using the SSH command. The successful login confirmed that the SSH service was running correctly and that secure remote access was properly configured. This also demonstrated that the server could be accessed remotely using SSH after completing the required configuration and security steps.

Here is screenshot evidence of SSH access:

<img width="1280" height="800" alt="nin" src="https://github.com/user-attachments/assets/850b0500-7db8-4dfc-930d-99ef60802ee6" />

To verify SSH access, I connected to the server remotely from my workstation using the SSH command. The successful login and server prompt confirmed that SSH access was working correctly and that the server could be accessed securely.

# 5. Configuration Files with before and after comparisons:
   
Before editing:

<img width="1280" height="800" alt="config1" src="https://github.com/user-attachments/assets/70f4f8e3-7e9b-4c8a-aeff-f3e1876e7a86" />

<img width="1280" height="800" alt="config2" src="https://github.com/user-attachments/assets/9142d3ff-1757-46ed-92d7-8142a256eeb2" />

The SSH configuration file, the server was using the default SSH settings. In this state, password authentication was enabled, and some important security options such as restricting root login and enforcing secure authentication methods were not explicitly configured. This meant that the SSH service was functional but not fully hardened against unauthorized access.

After Editing:
<img width="1280" height="800" alt="config8" src="https://github.com/user-attachments/assets/759d48d2-d9bd-47a0-8cc9-a7579b53961a" />


<img width="1280" height="800" alt="week4 5" src="https://github.com/user-attachments/assets/47301260-3565-4079-a415-27f3e671afcf" />

<img width="1280" height="800" alt="week4 5 1" src="https://github.com/user-attachments/assets/07e9698a-e908-4668-8053-735b24ffdde9" />

The /etc/ssh/sshd_config file, I improved the security of the SSH service by disabling root login and controlling how users authenticate. I set PermitRootLogin no to prevent direct root access, enabled public key authentication, and restricted password-based authentication. After saving the changes, I tested the configuration to ensure there were no errors and restarted the SSH service successfully. Finally, I verified the active SSH settings to confirm that the security changes were applied correctly.

# 6. Firewall documentation complete ruleset:

<img width="1280" height="800" alt="week4 6" src="https://github.com/user-attachments/assets/b192d594-058c-4387-ada2-16d4eeef7eef" />

To document the firewall configuration, I verified the active rules using UFW status commands. The ufw status verbose command confirmed that the firewall is active, with all incoming connections denied by default and outgoing connections allowed. It also showed that SSH access on port 22 is permitted only from my workstation IP address (192.168.56.1). The ufw status numbered command displayed the firewall rules in a numbered format, clearly showing the single allowed SSH rule. Finally, the ufw show added command confirmed the exact rule that was added to allow SSH access from one specific workstation. This documentation verifies that the firewall is correctly configured and securely restricting access.

# 7. Remote Administration Evidence demonstrating commands executed via SSH

All the server configuration and administrative work was done remotely from my workstation using SSH. After connecting to the server through SSH, I carried out different administrative tasks such as setting up and checking the firewall, managing users and privileges, verifying the SSH service, and updating configuration files. I did not access the server directly at any point, and all tasks were completed through the SSH session. This shows that the server was securely managed using remote administration as required for Week 4.

# Reference:
SSH SERVER:
https://ubuntu.com/server/docs/service-openssh

UFW Uncomplicated Firewall:
https://ubuntu.com/server/docs/security-firewall


