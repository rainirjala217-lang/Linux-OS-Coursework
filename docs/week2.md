# Week 2. Security Planning and Testing Methodology

# 1) Performance Testing Plan
   
* Remote monitoring Methodology

The system is monitored remotely to make sure it is working properly and safely. Monitoring tools like top, htop, and vmstat are used to check CPU capacity, memory capacity and disk activity. Network tools like iftop or nload are used to see how much internet bandwidth is being used and to spot unsual network activity.

System logs are checked using journalctl or syslog to find errors, show performance or strange system behaviour. All monitoring is done through secure SSH connectins, which is I didn’t have to open extra ports and risk weaking the system’s security.

* Testing Approach

Performance teasting starts by creating a baseline basically a 
snapshot of normal activity like CPU load and memory usage, and 
disk performance. This baseline is used to compare future test 
results.

Then after, stress testing is done by creating heavy traffic using tools 
like ApacheBench (ab) or inperf. This helps to show how the system 
behaves when it’s under high load. After that, scalability teasting is 
performed by showly increasing the number of users or 
connections. This checks whether the system can handle more
demand without showing down.

Lastly, recovery tasting is done by restarting services or simulating
system failures. This helps to checks how fast and safe the system
can recover. All test results are written down to compared with the 
baseline to find performance problems.

# 2) Security Configuration Checklist

* SSH Hardening:

SSH access is protect remote access to the system and I focused
on securing this, and i disabled root login so no one can directly
access the system as an administrator. I set up SSH keys instead of
using passwords, which are much safer and harder to break. Its
limited SSH access to specific users and made sure inactive
session close automatically. These steps help prevent unauthorized
access and reduce the risk of attacks.

* Firewall Configuration:

I configured the firewall to block all income traffic by default and
Only allow the ports that the system actually needs. This includes
ports for SSH and web services. Blocking useless traffic, the system
is less exposed to attacks. So, firewall logging is also enabled and I
can review any block connection attempts when needed.

* Mandatory Access Control (MAC):

It add another layer of security, I enabled mandatory access
control using SELinux or AppArmor. This helps control what
programs and services are allowed to do on the system. Even if a
service is compromised, it cannot access files or system resources
it does not need. Keeping this feature in enforcing mode helps
reduce damage from potential attacks.

* Automatic Updates:
In automatic updates to make sure the system always has latest
security patches. This helps to reduces attackers from using known
system weaknesses. Important updates for the operating system
and services are installed automatically, and reboots are planned
when required. This keeps the system secure without needing
constant manual updates.

* User Privilege Management:
  
User accounts are managed carefully to ensure security. Each user is given only the permissions they need to do their work. Administrative task are done using sudo instead of full root access. Unused accounts are removed, and strong password rules are applied to protect user accounts from being compromised.

* Network Security:

Network security is improved by using intrusion detection 
systems such as Snort or Suricata. Network separation is 
used where is possible, and TLS encryption is enforced to 
protect data sent over the network.

# 3) Threat Model

* Brute Force SSH Attack:

One of the threats I thought about was a brute-force attack on SSH. When somebody trying to keeps different passwords to get into the system and this can become a problem when if login is not secured properly. To deal with this, I turned off password login and started using SSH keys instead. I also limited which users are allowed to use SSH and blocked repeated failed login attempts. Doing this makes it much harder for someone who is not allowed to get access to the system.

* Privilege Escalation:

Privilege Escalation is the one of the possible treats and its happens when a normal user or server tries to take higher access, like administrator right. If this happen, System causes the serious problem to reduce this risk, I made sure users only have to permissions they need and use sudo when admin access is required. I also enabled SELinux or AppArmor and kept the system updated so known security issues are fixed. These help to protect the system from being taken over.

* Denial of Service Attack:

A denial-of-service attack is also something I considered. This type of attack sends lots of traffic to the server at one time, and which can slow down or make it stop working. Its help to prevent this, I added limited rate and kept eye on the traffic for anything usual. I made sure the has basic protections so it can handle normal traffic without crashing. 

# Conclusion:

In this week, I focused on planning system performance testing and improving overall security. I created a performance testing plan that uses remote monitoring and different testing methods to understand how the system behaves under normal and high load conditions. I also developed a security configuration checklist that covers SSH hardening, firewall setup, access control, automatic updates, user permission management, and network security to reduce system weaknesses. In addition, I identified key security threats such as SSH brute-force attacks, privilege escalation, and denial-of-service attacks, and applied mitigation step to reduce these risks. This phase helped establish a secure and reliable system that is ready for the future deployment.

# Reference:
1. NIST Special Publication 800-53 – Security and Privacy Controls
 
https://csrc.nist.gov/publications/detail/sp/800-53/rev-5/final

2. NIST Special Publication 800-41 – Guidelines on Firewalls and Network Security

https://csrc.nist.gov/publications/detail/sp/800-41/rev-1/final

3. OWASP – Threat Modeling 
 
https://owasp.org/www-community/Threat_Modeling

4. OpenSSH-Security Best Practices
 
https://www.ssh.com/academy/ssh

5. Red Hat Enterprise Linux-Monitoring and Managing System Performance
 
https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/9/html/monitoring_and_managing_system_status_and_performance/

6. SELinux Project-Official Documentation
 
https://selinuxproject.org/page/Main_Page










