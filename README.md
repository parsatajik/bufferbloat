CSC458 PA2
---

This assignment was written by Parsa Tajik in December of 2022.

Setup Instructions
---
While in the assignment's directory, enter the following commands in your terminal to clear mininet and start the testing process:

    sudo mn -c
    sudo ./run.sh

Questions
---

__1. Why do you see a difference in webpage fetch times with small and large router buffers?__

    Our varied fetch times are a result of different buffer sizes and TCP's packet loss detection algorithm. When travelling from h1 to h2, the Ppackets are bottlenecked by the slower link and forced to wait in the buffer.


__2. Bufferbloat can occur in other places such as your network interface card (NIC). Check the output of ifconfig eth0 on your VirtualBox VM. What is the (maximum) transmit queue length on the network interface reported by ifconfig? For this queue size and a draining rate of 100 Mbps, what is the maximum time a packet might wait in the queue before it leaves the NIC?__

eth0's `ifconfig` output:

    eth0    Link encap:Ethernet  HWaddr 08:00:27:ea:8e:68
            inet addr:10.0.2.15  Bcast:10.0.2.255  Mask:255.255.255.0
            UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
            RX packets:47974 errors:0 dropped:0 overruns:0 frame:0
            TX packets:44169 errors:0 dropped:0 overruns:0 carrier:0
            collisions:0 txqueuelen:1000
            RX bytes:3936328 (3.9 MB)  TX bytes:74442569 (74.4 MB)

Hence, the maximum transmit queue length (`txqueuelen`) is 1000 and the max transit unit (`MTU`) is 1500. Ultimately, the maximum packet queue wait time is:

    add calculations here

__3.How does the RTT reported by ping vary with the queue size? Write a symbolic equation to describe the relation between the two (ignore computation overheads in ping that might affect the final result).__

    K = ~2.5 (constant based on our graphs)
    RTT = Queue Size * K
    RTT is directly correlated with Queue Size

__4.Identify and describe two ways to mitigate the bufferbloat problem.__

- Utilizing queue management algorithms for fixing the drop tail problem in case of bursty flows by dropping packets before the queue gets full.

- According to our experiment, we can also reduce the maximum buffer size to decrease the overall latency. It seems as though having multiple smaller buffers is a great way to mitigate the bufferbloat problem.







