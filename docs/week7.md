# Week 7: Security Audit and System Evaluation
# 1.Introduction:

In this week, I conducted a security audit and overall system evaluation of my Ubuntu Server. The goal of this assessment was to check the system’s security posture, identify potential vulnerabilities, verify access control, and review running services. Several security tools and commands were used to analyse firewall status, SSH configuration, network exposure, and system services.

# 2. System Environment:

The security audit was performed on an Ubuntu Server, which was accessed remotely using SSH from an Ubuntu Desktop. All commands were executed on the server itself, ensuring that the assessment accurately reflects the server’s real security configuration.

# 3. Security Audit Using Lynis

Lynis was used to perform a full system security audit and configuration review.

Command I Used

sudo apt install lynis

sudo lynis audit system

 <img width="1135" height="285" alt="week7" src="https://github.com/user-attachments/assets/bc22d711-6a21-4a4e-9583-e5f04ccd2bce" />

The command sudo apt install lynis was used to install the Lynis security auditing tool. The output shows that Lynis was already installed and up to date on the system, so no new installation was required. This confirms that the system is ready to perform a security audit.

 <img width="1280" height="800" alt="week7 2" src="https://github.com/user-attachments/assets/8e01dac0-cd75-4c38-8087-6500091757fd" />
<img width="1280" height="800" alt="week7 4" src="https://github.com/user-attachments/assets/90b39865-5c13-44e4-9d69-1a2815599e57" />

The sudo lynis audit system command is used to perform a full security audit of the Ubuntu server. Lynis first detected the operating system, kernel version, hardware platform, and hostname, confirming that the scan was running on Ubuntu 24.04. The tool then checked system profiles and started auditing different security areas such as firewall configuration, system services, and vulnerability checks.

The output shows that the firewall is enabled, core security audit modules are active, and the scan completed successfully without errors. Lynis also created log and report files (/var/log/lynis.log and /var/log/lynis-report.dat) for later review. This audit helps identify security weaknesses and confirms that the system follows basic security best practices.

# 4. Firewall Configuration Verification:
   
The firewall status was checked to ensure that only required ports are open.

The command I used:

sudo ufw status

 <img width="1270" height="212" alt="week7 7" src="https://github.com/user-attachments/assets/666a699d-9fab-44aa-9218-bffac735f13d" />

The command was used to check the firewall status on the system. The output shows that the firewall is active, which means UFW is running and protecting the server.

Port 22/tcp (SSH) is allowed only from 192.168.56.1, which is the trusted client machine. This confirms that SSH access is restricted and not open to everyone, improving system security.

# 5. Network Security Assessment:

Network scanning was performed to identify exposed services and open ports on the server.

i used command:

sudo apt install nmap

<img width="1280" height="800" alt="week7 5" src="https://github.com/user-attachments/assets/caf9f7eb-4b99-4385-8f71-489df510975c" />

sudo nmap -sS 192.168.56.101 

<img width="1260" height="148" alt="week7 6" src="https://github.com/user-attachments/assets/67274dff-88c3-4321-a0dc-cf375e1a7b34" />
 
This command is used to perform a SYN scan on the target system to check for open network ports. However, the scan did not run because this type of scan requires administrator (root) privileges. Nmap stopped the scan and displayed a message saying that root access is required.

This means the command must be run with sudo to work correctly. No scan results were produced at this stage because the required permissions were not provided.


# 6. SSH Security Verification:

The SSH service was checked to ensure it is running securely and correctly.

 <img width="1280" height="800" alt="week7 3" src="https://github.com/user-attachments/assets/32cafa40-7117-4a5e-a856-d25a6fbe19b2" />

In this screenshot, I checked that SSH is correctly set up and running on the Ubuntu Server. The system shows that OpenSSH Server is already installed, so no new installation was required. I used the command sudo systemctl status ssh to confirm that the SSH service is active and running, which means the server is listening on port 22 and can accept secure remote connections. I also ran the ip addr command to view the network configuration, which shows that the server has valid IP addresses assigned. This confirms that both the SSH service and network connectivity are working properly.

# 7. Server Audit and Justification

A review of running services was conducted to ensure only required services are active.

This command I used:

systemctl list-units -type=service –state=running

  <img width="1280" height="800" alt="week7 8" src="https://github.com/user-attachments/assets/8590bf44-263d-4367-b50f-952775f68a76" />

I used the command systemctl list-units --type=service --state=running to view all active services. The results show only essential services running, such as SSH, system logging, networking, and Fail2Ban. This confirms that the system is running only necessary services, reducing the attack surface and improving overall security.


# 8. Access Control Verification:

User access was verified through SSH authentication. Only authorised users were able to access the system, and SSH access was restricted using firewall rules. This ensures that unauthorised access to the server is prevented

# 9. Remaining Risk Assessment:

Although the server is well secured, some improvement areas remain. Lynis warnings indicate that additional hardening steps, such as stricter SSH configuration and enhanced logging, could further improve security. These are considered low-risk issues and can be addressed in future updates.

# 10. Conclusion:

In this week, a security audit was performed to evaluate the overall configuration and security of the Ubuntu Server. Tools such as Lynis were used to review system security, while firewall rules, SSH access, and running services were checked to confirm that only required services are active. The audit showed that the system is securely configured with appropriate access controls in place. Although a few minor improvement recommendations were identified, no critical security issues were found. Overall, the server is well secured and ready for continued use.

# 11. Reference:

1. Lynis -Security Auditing tools
   
https://cisofy.com/lynis/

2.OpenSSH Manual page

https://www.openssh.com/manual.html

3.Nmap Network Scanning 

https://nmap.org/book/man.html



