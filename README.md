[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/IAASVEAZ)
# CSIT5970 Assignment-1: EC2 Measurement (2 questions, 4 marks)

### Deadline: 11:59PM, Feb, 28, Friday

---

### Name: Bailong Zhao
### Student Id: 21093440
### Email: bzhaoau@connect.ust.hk

---

## Question 1: Measure the EC2 CPU and Memory performance

1. (1 mark) Report the name of measurement tool used in your measurements (you are free to choose *any* open source measurement software as long as it can measure CPU and memory performance). Please describe your configuration of the measurement tool, and explain why you set such a value for each parameter. Explain what the values obtained from measurement results represent (e.g., the value of your measurement result can be the execution time for a scientific computing task, a score given by the measurement tools or something else).

I use sysbench as the measurement tool, the config that I use are 

```
sysbench memory --threads=32 run
sysbench --test=cpu --threads=32 run
```
I use multi threading as it is multi core. 

2. (1 mark) Run your measurement tool on general purpose `t2.micro`, `t2.medium`, and `c5d.large` Linux instances, respectively, and find the performance differences among these instances. Launch all the instances in the **US East (N. Virginia)** region.
  
   >Does the performance of EC2 instances increase commensurate with the increase of the number of vCPUs and memory resource?
    Yes, the memory performance increase. However, it is not always the case for CPU

    In order to answer this question, you need to complete the following table by filling out blanks with the measurement results corresponding to each instance type.

    | Size        | CPU performance | Memory performance |
    | ----------- | --------------- | ------------------ |
    | `t2.micro` |         2298.21        |         465.19 MiB/sec          |
    | `t2.medium`  |         4632.14        |       635.45 MiB/sec             |
    | `c5d.large` |       1230.51          |             6140.62 MiB/sec       |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI.

## Question 2: Measure the EC2 Network performance

1. (1 mark) The metrics of network performance include **TCP bandwidth** and **round-trip time (RTT)**. Within the same region, what network performance is experienced between instances of the same type and different types? In order to answer this question, you need to complete the following table.

   Between the same type, the network performance is better (higher bandwidth, lower RTT), and vice versa

    | Type                      | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | `t3.medium` - `t3.medium` |       3.52         |   0.3111       |
    | `m5.large` - `m5.large`   |         4.80       |     0.121     |
    | `c5n.large` - `c5n.large` |         3.91       |      0.142    |
    | `t3.medium` - `c5n.large` |         1.98       |       0.823   |
    | `m5.large` - `c5n.large`  |        3.21        |      0.541    |
    | `m5.large` - `t3.medium`  |        5.02        |    0.201      |

    > Region: US East (N. Virginia). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. Note: Use private IP address when using iPerf within the same region. You'll need iPerf for measuring TCP bandwidth and Ping for measuring Round-Trip time.

3. (1 mark) What about the network performance for instances deployed in different regions? In order to answer this question, you need to complete the following table.

   In the same region, the performance is better, higher bandwidth, lower RTT and vice versa for transmission between different region

    | Connection                | TCP b/w (Mbps) | RTT (ms) |
    | ------------------------- | -------------- | -------- |
    | N. Virginia - Oregon      |     0.0231           |     72.2     |
    | N. Virginia - N. Virginia |      1.10          |     0.426     |
    | Oregon - Oregon           |       1.03         |      0,529    |
 
    > Region: US East (N. Virginia), US West (Oregon). Use `Ubuntu Server 22.04 LTS (HVM)` as AMI. All instances are `c5.large`. Note: Use public IP address when using iPerf within the same region.
