Nirjala Ranahocha Chamling Rai


Operating System week1

1) System Architecture Diagram
   
A system architecture diagram is a visual overview of computer system structured and showing the main components and how they connect to each other.

<img width="255" height="281" alt="week1diagram" src="https://github.com/user-attachments/assets/886477b7-4507-4166-84a6-e345d12d2173" />

Here is my diagram, its showing host is laptop and VirtualBox and it has two ubuntu VMs one is server and another one desktop, and the networks (NAT and Host-only) this links them. And this virtual environment shows how data can flow between the part of system. 

2) Distribution Selection Justification:
   
I select Ubuntu Server 24.04 of Server Distribution because it has modern Linux Kenel (6.8) also long-term support through2029. It’s excellent community documentation and strong compatibility with VirtualBox and cloud Platforms, it’s including updated AppArmor Profiles and more efficient installer.

Comparison with Alternative Distributions:

|Feature Category	|Ubuntu Server 24.04 LTS (Chosen)|Ubuntu Server 22.04 LTS|	Debian 12|Fedora Server 40|
|-----------------|----------------|-------------------------|-----------|------------------|
|Release Year |2024-newest LTS	|2022-older LTS |2023	|2024
|Kernel Version |6.8- modern, improved performance and security	|5.15 – stable but aging |6.1 – stable but older |6.x – very modern, experimental features|
|Software Versions |Latest packages: Python 3.12, PHP 8.3, OpenSSL 3 |Slightly older packages |Older versions (stability-focused) |Newest cutting-edge versions|
|Update Frequency |Moderate, well-tested LTS updates |Moderate	Slow and conservative |Very fast updates every few weeks|
|Installer Quality |Modern Subiquity installer (easy) |Subiquity (older version) |Traditional installer, more manual steps| Fedora Installer (advanced, technical)|
|Performance|	High, optimized for new hardware |High |Medium |High (but unstable at times)|
|VirtualBox Compatibility |Excellent	|Excellent	|Excellent	|good|
|Overall Summary |Best balance of stability, modern features, and ease of use |Solid but older version of Ubuntu |Very stable but slow-moving |Cutting-edge but too fast-changing for coursework|

Ubuntu Server 24.04 LTS is the best choice because it’s offering the modern and up-to-date environment while still it’s belonged to LTS version, so it’s remains stable and supported for many years. This server has newest kernel and very compatible with VirtualBox.

3)Workstation Configuration Decision:

I Choose Ubuntu Desktop 24.04.3 LTS for Workstation, which is current LTS version. Tis desktop edition gives me a full graphical environment, so it makes the task like testing server connections, running client applications, and managing files more convenient.

Comparison with Alternatives:

|Feature Category	|Ubuntu Desktop 24.04.3 (chosen)	|Debian Desktop 12|	Fedora work station 40	|Ubuntu Desktop 22.04|
 |-----------------|------------------------|-------------------------|-----------|------------------|
|Pros	|Modern GNOME desktop, long-term support, great compatibility with Server 24.04, updated software |Extremely stable, minimal resource usage	|Cutting-edge features and very modern GNOME version |Very stable, widely used, well-documented|
|Cons	|Requires a bit more RAM than lightweight distros |Older software, less polished desktop experience, fewer GUI tools	|Short support cycle (around 13 months), frequent upgrades needed |Older software versions; less aligned with Server 24.04 packages|

I select Ubuntu Desktop 24.04.3 because it shows the best combination of user-friendly, stability and compatibility with server distribution. Ubuntu Desktop with Ubuntu Server creates a consistent environment where both systems use the same package manager and ecosystem. This reduces troubleshooting time and makes command and documentation easier to follow.

4) Network Configuration Documentation:
   
In the project I’m using two virtual machines, Ubuntu server 24.04 and Ubuntu Desktop 24.04.3, running inside Oracle VirtualBox on my host computer. Each VM has two network adapters so they can both go on the internet and also talk to each other in a private lab network

Adapter 1: NAT means VirtualBox gives them an automatic IP address in the 10.0.2.x range (for example 10.0.2.15) and lets them use the host’s internet connection. I use this for things like sudo apt update and installing software.

Adapter 2: Host-Only network called vboxnet0, which uses the IP range 192.168.56.0/24. On this private network, my Ubuntu Server VM has the address 192.168.56.5 and my Ubuntu Desktop VM has 192.168.56.6. This Host-Only network is only visible to the host and the VMs, and I use it so the desktop can connect to the server (for example using SSH or a web browser) without exposing those services to the outside world.

5)CLI System Specification Documentation:

Ubuntu Server 24.04

<img width="1280" height="800" alt="ubuntu_Server" src="https://github.com/user-attachments/assets/053d512e-3ef0-47e2-bdad-ac6a4fd3c037" />


Explain command:

|command	|Explanation of output|
|-----------------|----------------|
|uname	|Output is Linux confirms that the system is running on the Linux kernel.|
|free	|The system has approximately 4 GB RAM. About 427 MB is used, while the remaining memory is free or used as cache. Swap space of about 2.3 GB is configured and partially used.|
|df -h	|The system returns command not found because there must be a space between df and -h|
|ip addr	|Shows three interfaces: lo (loopback), enp0s3 with IP 10.0.2.15 (NAT network), and enp0s8 with IP 192.168.56.101 (host-only network).|
|lsb_relese -a	|Confirms the system is running Ubuntu 24.04.3 LTS, release 24.04, codename noble.|

Ubuntu desktop 24.04.3

<img width="1075" height="331" alt="ubuntu_desktop1" src="https://github.com/user-attachments/assets/7038153a-ea2f-43c1-8e27-c8537158b930" />

<img width="1083" height="675" alt="ubuntu_desktop 2" src="https://github.com/user-attachments/assets/0bf8ad1a-d8df-4564-946b-b0dd1e91c65d" />



Command Explain:

|command	|Explanation of output|
|-----------------|----------------|
|uname	|Output is Linux indicates that the system is running the Linux kernel.|
|free	|Displays total, used, and available RAM. The system has approximately 6.1 GB RAM with about 1 GB in use and 4 GB swap space available.|
|df -h	|Shows disk usage in human-readable format. The root partition /dev/sda2 has 46 GB total space, with 12 GB used and 32 GB available.|
|ip addr	|Lists all network interfaces and IP addresses. The system has a loopback interface, a NAT interface (10.0.2.15) for internet access, and a host-only interface (192.168.56.102) for host–VM communication.|
 |lsb_release -a	|Shows that the operating system is Ubuntu 24.04.3 LTS with codename noble.|

# Reflection:

In this first assessment week I learned how to setup Ubuntu Server and ubuntu Desktop in VirtualBox and connect them using NAT and Host-only network. Firstly, I found the IP addresses and network settings a bit confusing but I used command like ip addr helped me to see how everything was linked. I also got more confident using basic Linux commands such as uname, free, df -h, and lsb_release to check system information. Overall, I feel like I understand my virtual environment much better and I’m more comfortable working in linux terminal.

# References:
1. Canonical Ltd. Ubuntu Server 24.04 LTS Documentation   https://ubuntu.com/server/docs

2. Canonical Ltd. Ubuntu Destop 24.04 LTS Documentation   https://ubuntu.com/destop

3. canonical Ltd. Ubuntu 24.04 LTS(Noble Numbat) Release Notes
https:// discourse.ubuntu.com/t/ubuntu-24-04-its-noble-numbat-release-notes/

4. Oracle Coroprateion. VirtualBox Networking: NAT and Host-Only Networking
https://www.virtualbox.org/manual/ch06.html

5. Oracal Corporation. Oracal VM VirtualBox User Manual
https://www.virtualbox.org/manual/UserManual.html

6. Linux Foundation. Linux Command Line Basics  
https://www.linuxfoundation.org/resources/linux-command-line-basics

7. Shotts, W. The Linux Command Line
https://linuxcommand.org/tlcl.php

