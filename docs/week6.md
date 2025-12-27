# Week 6 Performance Evaluation and Analysis

# 1.Introduction 
In Week 6, I evaluated the performance of my Ubuntu Server under different workload conditions. The purpose of this testing was to understand how the operating system behaves when the system is idle and when it is under load. I tested CPU usage, memory usage, disk I/O performance, and network performance. The results were analysed to identify performance bottlenecks and to check overall system stability.

# 2. Testing methodology:
I carried out performance testing in four main steps. First, I collected baseline performance data while the server was idle to understand normal system behaviour. Next, I performed load testing by applying CPU, memory, disk, and network workloads. After that, I analysed the results to identify performance bottlenecks. Finally, I applied performance optimisations and re-tested the system to observe any improvements.

# 3. Baseline Performance Testing:
I collected baseline performance measurements while the server was idle. During this time, CPU usage was low, memory usage was stable, and no swap space was used. Disk activity was minimal, and network latency was very low with no packet loss. These results were used as a reference point for comparing performance during load testing.

I used these commands

top

free -m

df -h /

vmstat 1 5

ping -c 10 192.168.56.101
 
 <img width="1280" height="800" alt="week6" src="https://github.com/user-attachments/assets/3e1c30d5-55a1-4eb8-8313-73f1a4761202" />

The top command was used to observe real-time CPU and process activity while the system was idle. CPU usage remained very low and most processes were in a sleeping state. This confirms that the system was under minimal load during baseline testing.

 <img width="1280" height="800" alt="week6 1" src="https://github.com/user-attachments/assets/e0ac7229-ac1b-4e60-a347-e920d86040e5" />

This screenshot shows the system status while the server was idle. The free -m output shows that enough memory was available and no swap was used. The df -h command shows normal disk usage with plenty of free space. The vmstat results show low system activity and no heavy processing. The ping test shows very low network delay and no packet loss, which means the network connection was stable.

# 4. CPU Performance Testing
To test CPU performance, I used a CPU stress test to increase processor usage for a short period. This allowed me to observe how the system behaves under high CPU load.

I used This command for CPU load:

stress --cpu 2 --timeout 60

 <img width="1280" height="102" alt="week6 2" src="https://github.com/user-attachments/assets/6d9f18e8-0a3b-472a-a3f7-1b64f6f256ca" />

The stress command was used to apply CPU load for 60 seconds using two workers. This test increased CPU usage and completed successfully. The result confirms that the system remained stable during CPU stress testing.

# 5. Memory Performance Testing
I tested memory performance by applying a memory workload to the system. This test was used to observe how the operating system handles increased memory usage.

Used command:

stress --vm 1 --vm-bytes 512M --timeout 60

<img width="1280" height="104" alt="week6 3" src="https://github.com/user-attachments/assets/036c8351-9b2d-431b-8e94-98b22dfd6532" />

This shows memory performance testing using the stress command. One virtual memory worker was run for 60 seconds while allocating 512 MB of memory. The test completed successfully, which shows that the system was able to handle increased memory usage without crashing or becoming unstable.


# 6. Disk I/O Performance Testing:
Disk I/O performance was tested using a sequential write operation to measure disk write speed.

Used command:

dd if=/dev/zero of=baseline_test bs=1M count=512

 <img width="1280" height="127" alt="week6 4" src="https://github.com/user-attachments/assets/a1b88395-97f0-4dc8-bad8-c52da385c0fe" />

This screenshot shows disk I/O performance testing using the dd command. A 512 MB file was written to disk using zero-filled data to measure write speed. The result shows a write speed of about 435 MB/s, indicating that the disk was able to handle sustained write operations efficiently.

# 7. Network Performance Testing
I tested network performance by measuring both latency and throughput between the host machine and the Ubuntu Server using a Host-Only network.

Used command:

# For server:
iperf3 -s

<img width="1280" height="570" alt="week6 5 2" src="https://github.com/user-attachments/assets/9728e9c4-bdf4-4bdc-95ca-56fa962bb99e" />


This network performance testing using iperf3 in server mode. The server successfully accepted a connection from the client and transferred a large amount of data. High and stable network throughput was achieved, showing that the network connection is fast and reliable with no errors.

# For client:
iperf3 -c 192.168.56.101

<img width="1280" height="800" alt="week6 5 1" src="https://github.com/user-attachments/assets/60a28ef8-16f4-4250-a5c4-f1dd884996ff" />

 The network performance test from the client side using the iperf3 -c 192.168.56.101 command. The client successfully connected to the Ubuntu server and sent data for about 10 seconds. The results show high and stable network throughput (around 33 Gbit/s) with very low retransmissions, which confirms that the network connection between the client and server is fast, stable, and reliable.

# 8. Performance Optimisation
After analysing the results, I applied two performance optimisations.

8.1 Disk Optimisation

I reduced unnecessary disk writes by remounting the root filesystem with the noatime option.

Used command:

sudo mount -o remount,noatime /

 <img width="1279" height="96" alt="week6 6" src="https://github.com/user-attachments/assets/31f70d8e-7775-4b61-ad45-6cb7a5c0fbca" />

The command sudo mount -o remount,noatime / was run successfully to remount the root filesystem with the noatime option. This optimisation reduces unnecessary disk writes and helps improve disk I/O performance.

# 8.2 Memory Optimisation
I improved memory performance by reducing system swappiness to limit swap usage.

Used command:

sudo sysctl vm.swappiness=10

 <img width="1279" height="96" alt="week6 7" src="https://github.com/user-attachments/assets/3651ea59-9388-4383-800d-69651695feff" />

The system swap setting being adjusted using the command sudo sysctl vm.swappiness=10. This reduces how often the system uses swap memory and encourages it to use RAM instead. The command was applied successfully, helping improve system performance under normal and moderate load.


# 9. Performance Summary
|Metric|	Baseline|	Under Load|	After Optimisation|
|-----|-------|------|------|
|CPU usage |~1-2% |~95-100% |~2-5% |
|Memory usage |~463 MB |~975 MB |~820 MB |
|Disk performance |~0 MB/s |~435-520 MB/s |~520 MB/s |
|Network throughput |~0 Gbit/s |~33 Gbit/s |~33 Gbit/s |
|System stability |Stable |Stable |Stable|

This table summarises system performance during baseline, load testing, and after optimisation. CPU and memory usage increased under load as expected, while disk and network performance showed high throughput. After optimisation, the system returned to stable behaviour with improved overall performance and no stability issues.

# 10. Performance Visualisations

CPU Usage:

<img width="594" height="306" alt="Screenshot 2025-12-27 155826" src="https://github.com/user-attachments/assets/8ee605a7-9cc7-4c45-a466-dcad6050eb46" />

This chart shows CPU usage across different testing phases. During baseline testing, CPU usage was very low at around 1.5%, showing the system was idle. Under load, CPU usage increased to 100%, which confirms that the CPU stress test fully utilised the processor. After optimisation, CPU usage dropped to about 3.5%, showing that the system returned to a stable and efficient state.

Memory Usage:
<img width="527" height="262" alt="Screenshot 2025-12-27 155849" src="https://github.com/user-attachments/assets/e4513fc5-198f-46d3-a9f3-56d14a54d7cc" />

This chart illustrates memory usage during different system states. At baseline, memory usage was around 463 MB, indicating low resource usage. During load testing, memory usage increased to approximately 975 MB as expected. After optimisation, memory usage reduced to about 820 MB, showing improved memory management and more efficient use of RAM.

Network Throughput:

<img width="583" height="305" alt="Screenshot 2025-12-27 155857" src="https://github.com/user-attachments/assets/065edd9f-4689-4eb0-98d0-0b5b969e0be5" />

This chart shows network throughput across testing phases. During baseline testing, network activity was almost zero. Under load, network throughput increased significantly to around 33 Gbit/s using iperf3. After optimisation, throughput remained stable at the same level, confirming that network performance was not affected and remained reliable.

# 11. Conclusion

In this Week, I tested the performance of my Ubuntu Server to understand how the operating system behaves when idle and under different workloads while being managed remotely via SSH. Baseline testing showed low resource usage and stable system behaviour. When CPU, memory, disk, and network loads were applied, resource usage increased as expected, but the system remained stable. After applying disk and memory optimisations, performance improved while maintaining reliability. Overall, this testing helped demonstrate how Linux manages system resources under load and how performance tuning can improve efficiency in a headless server environment.
