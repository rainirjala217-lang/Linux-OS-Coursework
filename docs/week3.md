# Week3. Application Selection for Performance Testing 

# 1) Application Section Matrix
   
For performance testing, different applications were selected so that each on represent a different type of workloads. Stressing was selected the test the CPU because it’s easy to use and clearly shows how the processor behaves when it is under heavy work. The same tools were used for memory testing since it can 
use a large amount of Ram and helps in understanding how the system handles memory pressure. I selected FIO test disk operations because it is widely used as a tool for measuring read and write speed. For measuring network speed/ data transfer, iPerf3 is ideal as it is very easy to use for this purpose. Finally, the Minecraft server was selected as a server application to simulate, since it acts like an actual server and uses CPU, memory and network simultaneously over time.

# 2) Installation Documentation (SSH-Based)

# Ubuntu Server:

<img width="1280" height="800" alt="WEEK3SER" src="https://github.com/user-attachments/assets/315237b8-b464-4bce-85a0-73463fb8271d" />

I installed and enabled SSH on my Ubuntu server using terminal commands. I first updated the system using sudo apt update, then installed the SSH server with sudo apt install openssh-server -y. I enabled the SSH service so it starts automatically using sudo systemctl enable ssh and started the service with sudo systemctl start ssh. I checked the SSH status using systemctl status ssh and confirmed that it was running successfully. Finally, I used the ip addr command to find the system’s IP address so it could be accessed remotely using SSH.

# Ubuntu desktop:

<img width="1227" height="754" alt="WEEK3DES" src="https://github.com/user-attachments/assets/3468206b-5711-44be-8291-793580967a85" />
<img width="1219" height="768" alt="WEEK3 1DSK" src="https://github.com/user-attachments/assets/f974a60a-be07-4b46-b925-8b81a2fb38ab" />

After enabling SSH on the Ubuntu server, I connected to the server from my Ubuntu desktop using the ssh command and the server’s IP address. The first time I connected, I accepted the security fingerprint and entered the password. Once connected, I successfully logged into the server remotely, confirming that SSH access was working correctly.

# 3) Expected Resource Profiles

# Stress-ng (CPU test):
This test mainly uses the CPU and when it runs, the CPU usage will be very high because the processor is doing a lot of work. Memory usage will be low, and there will be no disk or network activity. This test helps to see how the CPU behaves under heavy load.

# Stress-ng (memory test)

This test uses mainly of Ram. The test will run when
memory Usage is increase. CPU usage will be medium, and
disk usage may increase if the system starts using swap.
Network usage is not expected in this test.

# FIO (Disk test):

This used to test the disk. During this test, the system will show high disk read and write activity. CPU and memory usage will be lower compared to disk usage. There is no network activity in this test.

# iPerf3 (Network test):

This test focuses on the network and Network usage will be very high as data is sent and received. CPU usage may increase a little but disk usage will stay low. This test help to checking network speed.

# Minecraft Server (Server application):

The mine craft server works like a real server. Its runs for a long time and uses CPU and memory continuously. Disk usage happens when data is saved, and network usage stays active when user are connected.

# 4) Monitoring Strategy

Performance testing, I used basic Linux monitoring tools to observe how system resources were being used. I ran each application one at a time so that I could clearly see its effect on the system.

CPU testing using Stress-ng, I used the top command to monitor CPU usage. This helped me see how much the processor was being used while the test was running.

Memory testing using Stress-ng, I checked memory usage using free -h and vmstat. These commands helped me understand how much RAM was being used and whether the system started using swap memory.

For disk testing using FIO, I used the iostat command to monitor disk activity. This helped me observe disk read and write operations during the test.

For network testing using iPerf3, I monitored network usage using the nload command. This allowed me to see how much data was being sent and received during the network test.

For the Minecraft server, I used the top command to monitor overall system performance. I observed CPU and memory usage while the server was running and checked disk and network activity to understand how the server behaves over time.

# Conclusion:

In this coursework, I selected and tested different
applications to measure CPU, memory, disk, network, and
server performance. I successfully set up SSH on the
Ubuntu server and connected to it remotely from the Ubuntu desktop. By monitoring system resources during each test, I gained a clear understanding of how different workloads affect overall system performance.

# References:

1.	Ubuntu Server Documentation:
		
 https://help.ubuntu.com
 
2.	OpenSSH Server Documentation:
	
https://ubuntu.com/server/docs/openssh-server

3.	Stress-ng: Stress testing tool:
	
https://wiki.ubuntu.com/Kernel/Reference/stress-ng

4.	FIO – Flexible I/O Tester:

https://fio.readthedocs.io
