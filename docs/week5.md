# Week 5 Advanced Security and Monitoring Infrastructure

# Introduction

In this phase 5, I am focusing on strengthening the security and monitoring of my Linux server. All configuration and management tasks will be performed remotely from my workstation using SSH. The goal is to implement advanced security controls, enable automated security updates, detect potential intrusion attempts, and set up basic remote monitoring to better understand the server’s performance.

# 1.Implement Access Control using AppArmor
# Objective:
The main purpose of this task is to implement mandatory access control on the server using AppArmor and to demonstrate how access control policies can be viewed, tracked and reported.
AppArmor Enforcement and Loggin 
 
 <img width="1280" height="800" alt="week5 1 2" src="https://github.com/user-attachments/assets/f75b4e60-0e6a-40e6-ac93-0503b36f0366" />

 <img width="1280" height="249" alt="week5 1 3" src="https://github.com/user-attachments/assets/3046c739-6797-4dba-883f-0d4af4ba7f40" />

<img width="1280" height="800" alt="week5 1 4" src="https://github.com/user-attachments/assets/651628b5-a622-42dd-abe5-afbc40e1697e" />

# Explanation:

AppArmor status and enforcement were verified using the aa-status and aa-enabled commands. Available security profiles were viewed from the /etc/apparmor.d directory. AppArmor activity was monitored using system logs accessed through journalctl, confirming that access control events are tracked and reported.

# 2. Configure Automatic Security Updates

# Objective

The objective of this task is to configure the server to automatically install security updates so that critical vulnerabilities are patched without manual intervention.

# configuration verification, logging and monitoring:

<img width="1280" height="800" alt="week5 2" src="https://github.com/user-attachments/assets/f6f6cc89-7b8a-4110-926e-26cb0e6e72ab" />

<img width="1280" height="800" alt="week5 2 1" src="https://github.com/user-attachments/assets/80cc2793-60d2-4c90-92c9-85f7ec53f91c" />

# Explanation:
This apt update command was used to refresh the server’s package list and confirm internet connectivity, followed by apt install apparmor apparmor-utils to install AppArmor and its tools for improving system security. Automatic security updates were configured using dpkg-reconfigure unattended-upgrades so important updates are applied automatically. The command systemctl status unattended-upgrades was then used to confirm that the update service is running correctly, while cat /etc/apt/apt.conf.d/20auto-upgrades verified that automatic updates are enabled. Finally, tail /var/log/unattended-upgrades/unattended-upgrades.log was used to check update logs and confirm that security updates are being applied successfully, demonstrating a secure and well-maintained server system. 

# 3. Configure fail2ban for enhanced intrusion detection
Fail2ban was implemented on the server to enhance intrusion detection and prevent brute-force attacks, particularly against the SSH service. Fail2ban works by monitoring system log files for repeated failed authentication attempts and automatically blocking the source IP address when a defined threshold is exceeded. This provides an additional layer of automated security by detecting suspicious activity and responding without manual intervention.

# Fail2ban Installation

<img width="1280" height="800" alt="week5 3" src="https://github.com/user-attachments/assets/ba7b1964-4fef-465c-9c7e-ad4b8dd78e9b" />

I installed fail2ban on the server using the apt install fail2ban command, which also installed the required supporting packages automatically. The installation completed successfully, confirming that fail2ban is now available on the system and ready to be configured for intrusion detection.

<img width="1146" height="185" alt="week5 3 1" src="https://github.com/user-attachments/assets/2aa2ba11-4228-4900-bbd8-dca39a1b3888" />

I used the command systemctl enable --now fail2ban to start the fail2ban service immediately and configure it to run automatically at system startup. The output confirms that the service was successfully enabled and started, ensuring continuous intrusion protection without requiring manual intervention after a reboot.

<img width="1236" height="432" alt="week5 3 3" src="https://github.com/user-attachments/assets/7af4f706-9dd7-4419-9523-ce6ff064887e" />

I edited the fail2ban configuration file using nano to apply the SSH protection settings, then restarted the fail2ban service to apply the changes. I checked the service status again to confirm that fail2ban restarted successfully and is running with the updated configuration.

<img width="1280" height="800" alt="week5 3 5" src="https://github.com/user-attachments/assets/0bfb11ed-a02a-416d-9fc7-91d9df30b381" />

Here, I edited the /etc/fail2ban/jail.local file to configure fail2ban settings and enable SSH protection. The configuration limits failed login attempts and automatically bans IP addresses that show suspicious activity, improving the server’s security.

<img width="1257" height="255" alt="week5 3 4" src="https://github.com/user-attachments/assets/9a5beb49-1886-4485-9d8f-2a41492e8bcb" />

I checked the status of the SSH jail using fail2ban-client status sshd to confirm that fail2ban is actively monitoring SSH login attempts. The output shows that the SSH jail is enabled and running correctly, with no failed attempts or banned IP addresses at this time, confirming that intrusion detection for SSH is functioning as expected.

# 4. Security Baseline Verification Script (security-baseline.sh)

A security baseline verification script was created to check that all previously configured security controls are active and working correctly. The script verifies key services such as AppArmor, automatic updates, fail2ban, SSH protection, and firewall status, and is run via SSH to confirm secure remote administration.

<img width="1280" height="800" alt="week5 4 2" src="https://github.com/user-attachments/assets/b8747c15-55cd-414a-8234-e57fd7123020" />

<img width="1280" height="800" alt="week5 4" src="https://github.com/user-attachments/assets/92610ae5-4655-4f05-bbee-19620900b4db" />

<img width="1280" height="278" alt="week5 4 1" src="https://github.com/user-attachments/assets/1d2ba89c-70c1-46b7-b114-2ba719ed5162" />

I created the security-baseline.sh script on the server and edited it using Nano to check the security settings that were configured in earlier phases. After saving the script, I ran it with sudo to make sure it could check system services correctly. The output showed that AppArmor is enabled, unattended upgrades are active, fail2ban is running with SSH protection enabled, and the firewall is active with the correct rule applied. This confirms that the main security controls on the server are working as expected.

# 5. Remote Monitoring Script

# Introduction
In the monitor the server remotely, I created a script on the workstation that connects to the server using SSH and collects basic system performance information. The purpose of this script is to check the server’s current status without logging in manually each time. The script gathers information such as system uptime, CPU usage, memory usage, and disk usage, allowing the server’s performance to be monitored from the workstation.

<img width="524" height="43" alt="week5 5 2" src="https://github.com/user-attachments/assets/58971d5f-8239-4017-922b-fb53fbd426bb" />

I opened the monitor-server.sh file using Nano to create and edit the remote monitoring script. After saving the script, I used the chmod +x command to give the file execute permissions, which allows the script to be run as a program from the terminal.

<img width="1280" height="800" alt="week5 5" src="https://github.com/user-attachments/assets/bf646c60-a92b-4a93-9003-f01cb3599e17" />

I edited the monitor-server.sh script to set the server user and IP address and added SSH commands to collect uptime, CPU load, memory usage, and disk usage from the server.

<img width="1280" height="800" alt="week5 5 1" src="https://github.com/user-attachments/assets/44e40a56-ee14-4859-bcc2-13ab9c867d55" />

I made the monitor-server.sh script executable and then ran it from the workstation. During execution, the script connected to the server via SSH and prompted for authentication before collecting system uptime, CPU load, memory usage, and disk usage. The output confirmed that remote monitoring is working correctly and that live performance information can be retrieved from the server.

# Reference:
1.AppArmor Ubuntu Documentation:

https://ubuntu.com/server/docs/security-apparmor

2. Fail2ban official Documentation:

https://www.fail2ban.org/wiki/index.php/Main_Page






