ARC Systems 
===========

At the centre of the ARC service are two high performance compute clusters - **arc** and **htc**. 
 
**arc** is designed for multi-node parallel computation; **htc** is designed for high-thoughput operation (lower core count jobs). **htc** is also a more heterogeneous system offering different types of resources, such as GPGPU computing and high memory systems; nodes on **arc** are uniform. Users get access to both both clusters automatically as part of the process of obtaining an account with ARC, and can use either or both. 

For more detailled information on the hardware specifications of these clusters, see the tables below:


+---------+---------------------------------+-----------+------------------------------------------------------+-----------------+--------------------------------------------+
| Cluster | Description                     |Login Node |Compute Nodes                                         |Minimum Job Size |Notes:                                      |
+=========+=================================+===========+======================================================+=================+============================================+
| arc     | Our largest compute cluster.    | arc-login | CPU: 48 core Cascade Lake (2.90GHz)                  | 1 core	         | Non-blocking island size is 2212 cores     |
|         | Optimised for large parallel    |           | Memory: 392GB                                        |                 |                                            |
|         | Scheduler prefers large jobs.   |           |                                                      |                 |                                            |
|         | Offers low-latency interconnect |           |                                                      |                 |                                            |
+---------+---------------------------------+-----------+------------------------------------------------------+-----------------+--------------------------------------------+
| htc     | Optimised for single core jobs  | htc-login | CPUs: mix of Broadwell, Haswell, Cascade Lake        | 1 core          | Jobs will only be scheduled onto a GPU     |
|         | and SMP jobs up to one node     |           | GPU: P100, V100, A100, RTX                           |                 |                                            |
|         | Scheduler prefers small jobs.   |           |                                                      |                 |                                            |
|         | Supports jobs requiring GPUs.   |           |                                                      |                 |                                            |
+---------+---------------------------------+-----------+------------------------------------------------------+-----------------+--------------------------------------------+
 

Operating system
================


The ARC systems use the Linux Operating System (specifically CentOS 8) which is commonly used in HPC. We do not have any HPC systems running Windows (or MacOS). If you are unfamiliar with using Linux, please consider:

- Finding introduction to Linux resources online (through Google/Bing/Yahoo etc).
- Working through our brief Introduction to Linux course.
- Attending our Introduction to ARC training course (this does not teach you how to use Linux but the examples will help you gain a greater understanding).

Capability cluster (arc)
========================

The capability system - cluster name arc - has a total of 305 48 core worker nodes, some of which are co-investment hardware. It offers a total of 14,640 CPU cores.

All nodes have the following:

- 2x Intel Platinum 8628 CPU. The Platinum 8628 is a 24 core 2.90GHz Cascade Lake CPU. Thus all nodes have 48 CPU cores per node.
- 384GB memory
- HDR 100 infiniband interconnect. The fabric has a 3:1 blocking factor with non-blocking islands of 44 nodes (2112 cores).
- OS is CentOS Linux 8.1. Scheduler is SLURM.

Login node for the system is 'arc-login.arc.ox.ac.uk', which allows logins from the University network range (including VPN).

More details on the available nodes:

node count	core count	nodes	stakeholder	comments
45	2,160	arc-c[001-045]	Quantum Hub	
available for general use for short jobs (<12hrs)

8	384	arc-c[046-053]	Earth Science	available for general use for short jobs (<12hrs)
252	12,096	arc-c[054-305]	ARC	 
 

Throughput cluster (htc)
========================

The throughput system - cluster name htc  - currently has 25 worker nodes, some of which are co-investment hardware. Note that additional nodes will migrate into this system in the coming weeks. Please note: Co-investment machines have been purchased by specific departments/groups and are hosted by the ARC team (see Stakeholder column for details). These machines are available for general use, but may be subject to job time limits and/or may occasionally be reserved for exclusive use of the entity that purchased them.

19 of the nodes are GPGPU nodes. More information on how to access GPU nodes is available.

2 of the nodes are High Memory nodes with 3TB of RAM.

OS is CentOS Linux 8.1. Scheduler is SLURM.

Login node for the system is 'htc-login.arc.ox.ac.uk', which allows logins from the University network range (including VPN).

Details on the nodes are:

Node Count	CPU	Cores Per Node	memory per node	# GPUs	GPUs	GPU memory	nvlink	interconnect	stakeholder	notes
2	Intel E5-2640v3 (Haswell), 2.60GHz	16	64GB	-	-	-	-	-	ARC	 
2	Intel E5-2640v4 (Broadwell), 2.60 GHz	20	128GB	-	-	-	-	-	ARC	 
2	Intel Platinum 8628 (Cascade Lake), 2.90GHz	48	3TB	-	-	-	-	HDR 100	ARC	 
40	Intel Platinum 8628 (Cascade Lake), 2.90GHz	48	384GB	-	-	-	-	-	ARC	 
8	Intel Platinum 8628 (Cascade Lake), 2.90GHz	48	384GB	2	V100	32GB	no	HDR 100	Quantum Hub	available for short jobs (<12hrs)
4	Intel Platinum 8628 (Cascade Lake), 2.90GHz	48	384GB	4	A100	40GB	no	HDR 100	ARC	 
6	Intel Platinum 8628 (Cascade Lake), 2.90GHz	48	384GB	4	RTX8000	40GB	no	HDR 100	ARC	 
1	AMD Epyc 7452 (Rome), 2.35GHz	64	1TB	4	A100	40GB	no	-	Wes Armour	available for short jobs (<12hrs)
10	
Intel Silver 4210 (Cascade Lake), 2.20GHz

20	256GB	4	TITAN RTX	24GB	no	-	ECR	available for short jobs (<12hrs)
5	Intel Gold 5120 (Cascade Lake), 2.20GHz	28	384GB	4	P100	16GB	no	-	Torr Vision Group	available for short jobs (<12hrs)
3	Intel Silver 4112 (Cascade Lake), 2.60GHz	8	192GB	4	TITAN RTX	24GB	yes	-	Applied Artificial Intelligence Lab	available for short jobs (<12hrs)
2	Intel Gold 5120 (Cascade Lake), 2.20GHz	28	384GB	4	V100	16GB	yes	-	Torr Vision Group	available for short jobs (<12hrs)
2	Intel Gold 5120 (Cascade Lake), 2.20GHz	28	384GB	4	V100	16GB	yes	-	Dell UK	interactive / devel nodes
2	Intel Gold 5120 (Cascade Lake), 2.20GHz	28	384GB	4	V100	32GB	yes	-	Torr Vision Group	available for short jobs (<12hrs)
1	Intel E5-2698 v4 (Broadwell), 2.20GHz	40	512GB	8	V100	16GB	yes	-	ARC	 
5	Intel E5-2698 v4 (Broadwell), 2.20GHz	40	512GB	8	V100-LS	32GB	yes	-	ARC	 
3	Intel Silver 4208 (Cascade Lake), 2.10GHz	16	128GB	4	RTX-A6000	48GB	yes	HDR100	Applied Artificial Intelligence Lab	available for short jobs (<12hrs)
GPU Resources
ARC has a number of GPU nodes in the "htc" cluster.

The following table (containing data from http://www.nvidia.com/object/tesla-servers.html and https://developer.nvidia.com/cuda-gpus) describes the characteristics of each GPU card.

 	Tesla K40	Tesla K80	Tesla M40	Tesla P4	Tesla P100
GPU Architecture	Kepler	Kepler	Maxwell	Pascal	Pascal
Memory size	12 GB	24 GB	24GB	8GB	16GB
ECC	yes	yes	no	yes	yes
CUDA cores	2880	4992	3072	2560	3584
CUDA Compute Capability	3.5	3.7	5.2	6.1	6.0
 	Tesla V100	Titan RTX	Quadro RTX 8000	Tesla A100	RTX A6000
GPU Architecture	Volta	Turing	Turing	Ampere	Ampere
Memory size	16GB/32GB	24GB	48GB	40GB/80GB	48GB
ECC	yes	no	yes	yes	yes
CUDA cores	5120	4606	4608	6912	10,752
CUDA Compute Capability	7.0	7.5	7.5	8.6	8.6
 

NVidia DGX Max-Q
These nodes are a version of the NVIDIA Volta DGX-1 32GB V100 Server (offering 8x NVLinked Tesla V100 32GB GPUs) using the slightly lower clock speed V100-SXM2-32GB-LS version of the Volta cards. The systems have 40 CPU cores (E5-2698 v4 @ 2.20GHz CPUs) and 512GB of system memory.

The plots below show typical benchmark results between the DGX1V and DGX Max-Q:

 

typical GROMACS benchmark results between the DGX1V and DGX Max-Qbenchmark results for tensorflow, DGX1V and DGX-MaxQ

 

Storage
=======

Our clusters systems share 2PB of high-performance GPFS storage.

Software
========

Users may find the application they are interested in running is already been installed on at least one of the systems.  Users are welcome to request the installation of new applications and libraries or updates to already installed applications via our software request form.
