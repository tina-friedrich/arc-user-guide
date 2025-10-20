ARC Systems
===========

At the centre of the ARC service are two high performance compute clusters - **arc** and **htc**.

- **arc** is designed for multi-node parallel computation
- **htc** is designed for high-thoughput operation (lower core count jobs).

**htc** is also a more heterogeneous system offering different types of resources, such as GPGPU computing and high memory systems; nodes on **arc** are uniform. Users get access to both both clusters automatically as part of the process of obtaining an account with ARC, and can use either or both.

For more detailled information on the hardware specifications of these clusters, see the tables below:

.. table::
        :widths: 5, 25, 15, 20, 20, 15

        +---------+--------------------------------------------------------------------------------+------------+----------------------------------------------------------------------+------------------+---------------------------------------------------------------------------+
        | Cluster | Description                                                                    | Login Node | Compute Nodes                                                        | Minimum Job Size | Notes:                                                                    |
        +=========+================================================================================+============+======================================================================+==================+===========================================================================+
        | arc     | | Our largest compute cluster.                                                 |            | | CPU: 48 core Cascade Lake (Intel Xeon Platinum 8268 CPU @ 2.90GHz) |                  | Non-blocking island size is 2212 cores                                    |
        |         | | Optimised for large parallel jobs spanning multiple nodes.                   | arc-login  | | Memory: 392GB                                                      | 1 core           |                                                                           |
        |         | | Scheduler prefers large jobs.                                                |            |                                                                      |                  |                                                                           |
        |         | | Offers low-latency interconnect (Mellanox HDR 100).                          |            |                                                                      |                  |                                                                           |
        +---------+--------------------------------------------------------------------------------+------------+----------------------------------------------------------------------+------------------+---------------------------------------------------------------------------+
        | htc     | | Optimised for single core jobs, and SMP jobs up to one node in size.         |            | | CPUs: mix of Broadwell, Haswell, Cacade Lake                       |                  | Jobs will only be scheduled onto a GPU node if requesting a GPU resource. |
        |         | | Scheduler prefers small jobs.                                                | htc-login  | | GPU: P100, V100, A100, RTX                                         | 1 core           |                                                                           |
        |         | | Also catering for jobs requiring resources other than CPU cores (e.g. GPUs). |            |                                                                      |                  |                                                                           |
        +---------+--------------------------------------------------------------------------------+------------+----------------------------------------------------------------------+------------------+---------------------------------------------------------------------------+

Operating system
----------------


The ARC systems use the Linux Operating System (specifically AlmaLinux 9) which is commonly used in HPC. We do not have any HPC systems running Windows (or MacOS). If you are unfamiliar with using Linux, please consider:

- Finding introduction to Linux resources online (through Google/Bing/Yahoo etc).
- Working through our brief Introduction to Linux course.
- Attending our Introduction to ARC training course (this does not teach you how to use Linux but the examples will help you gain a greater understanding).

Capability cluster (arc)
------------------------

The capability system - cluster name arc - has a total of 305 48 core worker nodes, some of which are co-investment hardware. These machines are available for general use, but may be subject to job time limits and/or may occasionally be reserved for exclusive use of the entity that purchased them.

The ARC system offers a total of 14,640 CPU cores.

All nodes have the following:

- 2x Intel Platinum 8628 CPU. The Platinum 8628 is a 24 core 2.90GHz Cascade Lake CPU. Thus all nodes have 48 CPU cores per node.
- 384GB memory
- HDR 100 infiniband interconnect. The fabric has a 4:1 blocking factor with non-blocking islands of 44 nodes (2112 cores).
- OS is AlmaLinux 9.4. Scheduler is SLURM.

Login node for the system is 'arc-login.arc.ox.ac.uk', which allows logins from the University network range (including VPN).

The generally available partitions are:

.. table::
        :widths: 20 20 20 20 20

        +-------------+---------------+------------------+------------------+------------------+
        | Partition   | Nodes / cores | Nodes            | Default run time | Maximum run time |
        +=============+===============+==================+==================+==================+
        | short       | 256 / 12,288  | | arc-c[046-293] | 1 hour           | 12 hours         |
        |             |               | | arc-c[300-301] |                  |                  |
        |             |               | | arc-c[306-311] |                  |                  |
        +-------------+---------------+------------------+------------------+------------------+
        | medium      | 242 / 11,616  | arc-c[046-287]   | 12 hours         | 2 days           |
        +-------------+---------------+------------------+------------------+------------------+
        | long        | 242 / 11,616  | arc-c[046-287]   | 1 day            | unlimited        |
        +-------------+---------------+------------------+------------------+------------------+
        | legacy      | 6 / 288       | arc-c[294-299]   |                  | 10 minutes       |
        +-------------+---------------+------------------+------------------+------------------+
        | devel       | 2 / 96        | arc-c[302-303]   |                  | 10 minutes       |
        +-------------+---------------+------------------+------------------+------------------+
        | interactive | 2 / 96        | arc-c[304-305]   | 1 hour           | 4 hours          |
        +-------------+---------------+------------------+------------------+------------------+

Throughput cluster (htc)
------------------------

The throughput system - cluster name htc - currently 95 worker nodes, some of which are co-investment hardware. These machines are available for general use, but may be subject to job time limits and/or may occasionally be reserved for exclusive use of the entity that purchased them. The hardware on the HTC system
is more heterogeneous than on the ARC system.

49 of the nodes are GPGPU nodes. More information on how to access GPU nodes is available.

2 of the nodes are High Memory nodes with 3TB of RAM.

OS is AlmaLinux 9.4. Scheduler is SLURM.

Login node for the system is 'htc-login.arc.ox.ac.uk', which allows logins from the University network range (including VPN).

Details on the partitions are:

.. table::
        :widths: 10 20 30 18 22

        +-------------+-------------------+------------------------------------------+------------------+------------------+
        | Partition   | Nodes / cores,    | Nodes                                    | Default run time | Maximum run time |
        |             | GPUs              |                                          |                  |                  |
        +=============+===================+==========================================+==================+==================+
        | short       | | 93 / 3,716      | | htc-c[001-046,048-073]                 | 1 hour           | 12 hours         |
        |             | - 76x V100        | | htc-g[009-018]                         |                  |                  |
        |             | - 16x A100        | | htc-g[020-038]                         |                  |                  |
        |             | - 24x RTX8000     | | htc-g[041-043,045-055]                 |                  |                  |
        |             | - 12x RTXA6000    | | htc-g[058-060]                         |                  |                  |
        |             | - 20x P100        |                                          |                  |                  |
        |             | - 52x Titan RTX   |                                          |                  |                  |
        +-------------+-------------------+------------------------------------------+------------------+------------------+
        | medium      | | 61 / 2,808      | | htc-c[006-046,048-073]                 | 12 hours         | 2 days           |
        |             | | - 48x V100      | | htc-g[009-018,045-049]                 |                  |                  |
        |             | | - 16x A100      |                                          |                  |                  |
        |             | | - 24x RTX8000   |                                          |                  |                  |
        +-------------+-------------------+------------------------------------------+------------------+------------------+
        | long        | | 61 / 2,808      | | htc-c[006-046,048-073]                 | 1 day            | unlimited        |
        |             | | - 48x V100      | | htc-g[009-018,045-049]                 |                  |                  |
        |             | | - 16x A100      |                                          |                  |                  |
        |             | | - 24x RTX8000   |                                          |                  |                  |
        +-------------+-------------------+------------------------------------------+------------------+------------------+
        | devel       | | 1 / 28          | htc-g039                                 |                  | 10 minutes       |
        |             | | - 4x V100       |                                          |                  |                  |
        +-------------+-------------------+------------------------------------------+------------------+------------------+
        | interactive | | 1 / 28          | htc-g040                                 | 1 hour           | 4 hours          |
        |             | | - 4x V100       |                                          |                  |                  |
        +-------------+-------------------+------------------------------------------+------------------+------------------+

Node CPU details are:

.. table::
        :widths: 15 35 20 20 10

        +----------------+-----------------------------------------------+----------------+-----------------+--------------+
        | Nodes          | CPU                                           | Cores per node | memory per node | interconnect |
        +================+===============================================+================+=================+==============+
        | htc-c[005-006] | Intel Platinum 8628 (Cascade Lake), 2.90GHz   | 96             | 3TB             | HDR100       |
        +----------------+-----------------------------------------------+----------------+-----------------+--------------+
        | htc-c[007-046] | Intel Platinum 8628 (Cascade Lake), 2.90GHz   | 48             | 384GB           |              |
        +----------------+-----------------------------------------------+----------------+-----------------+--------------+
        | htc-c047       | Intel E7-8860v3 (Haswell), 2.60GHz            | 128            | 6TB             |              |
        +----------------+-----------------------------------------------+----------------+-----------------+--------------+
        | htc-c[048-049] | AMD EPYC 9634 (Genoa), 2.25GHz                | 168            | 2.3TB           |              |
        +----------------+-----------------------------------------------+----------------+-----------------+--------------+
        | htc-c[050-055] | AMD EPYC 9634 (Genoa), 2.25GHz                | 168            | 1.5TB           |              |
        +----------------+-----------------------------------------------+----------------+-----------------+--------------+
        | htc-c[056-073] | AMD EPYC 9634 (Genoa), 2.25GHz                | 84             | 1.1TB           |              |
        +----------------+-----------------------------------------------+----------------+-----------------+--------------+
        | htc-g[009-018] | Intel Platinum 8628 (Cascade Lake), 2.90GHz   | 48             | 384GB           | HDR100       |
        +----------------+-----------------------------------------------+----------------+-----------------+--------------+
        | htc-g019       | AMD Epyc 7452 (Rome), 2.35GHz                 | 64             | 1TB             |              |
        +----------------+-----------------------------------------------+----------------+-----------------+--------------+
        | htc-g[020-029] | Intel Silver 4210 (Cascade Lake), 2.20GHz     | 20             | 256GB           |              |
        +----------------+-----------------------------------------------+----------------+-----------------+--------------+
        | htc-g[030-040] | Intel Gold 5120 (Skylake), 2.20GHz            | 28             | 384GB           |              |
        +----------------+-----------------------------------------------+----------------+-----------------+--------------+
        | htc-g[041-043] | Intel Silver 4112 (Skylake), 2.60GHz          | 8              | 192GB           |              |
        +----------------+-----------------------------------------------+----------------+-----------------+--------------+
        | htc-g[045-049] | Intel E5-2698 v4 (Broadwell), 2.20GHz         | 40             | 512GB           |              |
        +----------------+-----------------------------------------------+----------------+-----------------+--------------+
        | htc-g[050-052] | Intel Silver 4208 (Cascade Lake), 2.10GHz     | 16             | 128GB           | HDR100       |
        +----------------+-----------------------------------------------+----------------+-----------------+--------------+
        | htc-g[053-055] | Intel Gold 6342 (Ice Lake), 2.80GHz           | 16             | 500GB           | HDR100       |
        +----------------+-----------------------------------------------+----------------+-----------------+--------------+
        | htc-g056       | Intel Gold 6342 (Ice Lake), 2.80GHz           | 48             | 512GB           | HDR100       |
        +----------------+-----------------------------------------------+----------------+-----------------+--------------+
        | htc-g057       | NVidia Grace Hopper AArch64 3.5GHz            | 72             | 580GB           |              |
        +----------------+-----------------------------------------------+----------------+-----------------+--------------+
        | htc-g058       | Intel Gold 5418Y (Sapphire Rapids), 2.0GHz    | 48             | 1.5TB           |              |
        +----------------+-----------------------------------------------+----------------+-----------------+--------------+
        | htc-g[059-060] | Intel Platinum 8468 (Sapphire Rapids), 2.1GHz | 96             | 1TB             | HDR100       |
        +----------------+-----------------------------------------------+----------------+-----------------+--------------+

GPU Resources
-------------

ARC has a number of GPU nodes in the "htc" cluster.

Node GPU details are:

.. table::
        :widths: 15 10 10 15 10 10 20 10

        +----------------+-----------+-------+------------+-----+------------+-------------------------+----------+
        | Nodes          | GPUs      | #GPUs | GPU memory | ECC | CUDA cores | CUDA compute capability | nvlink   |
        +================+===========+=======+============+=====+============+=========================+==========+
        | htc-g[009-014] | RTX8000   | 4     | 40GB       | yes | 4608       | 7.5                     | no       |
        +----------------+-----------+-------+------------+-----+------------+-------------------------+----------+
        | htc-g[015-019] | A100      | 4     | 40GB       | yes | 6912       | 8.0                     | no       |
        +----------------+-----------+-------+------------+-----+------------+-------------------------+----------+
        | htc-g[020-029] | Titan RTX | 4     | 24GB       | no  | 4606       | 7.5                     | pairwise |
        +----------------+-----------+-------+------------+-----+------------+-------------------------+----------+
        | htc-g[030-034] | P100      | 4     | 16GB       | yes | 3584       | 6.0                     | no       |
        +----------------+-----------+-------+------------+-----+------------+-------------------------+----------+
        | htc-g[035-036] | V100      | 4     | 16GB       | yes | 5120       | 7.0                     | no       |
        +----------------+-----------+-------+------------+-----+------------+-------------------------+----------+
        | htc-g[037-038] | V100      | 4     | 32GB       | yes | 5120       | 7.0                     | yes      |
        +----------------+-----------+-------+------------+-----+------------+-------------------------+----------+
        | htc-g[039-040] | V100      | 4     | 16GB       | yes | 5120       | 7.0                     | yes      |
        +----------------+-----------+-------+------------+-----+------------+-------------------------+----------+
        | htc-g[041-043] | Titan RTX | 4     | 24GB       | yes | 4606       | 7.5                     | pairwise |
        +----------------+-----------+-------+------------+-----+------------+-------------------------+----------+
        | htc-g[045-049] | V100-LS   | 8     | 32GB       | yes | 5120       | 7.0                     | yes      |
        +----------------+-----------+-------+------------+-----+------------+-------------------------+----------+
        | htc-g[050-052] | RTXA6000  | 4     | 48GB       | yes | 10,752     | 8.6                     | yes      |
        +----------------+-----------+-------+------------+-----+------------+-------------------------+----------+
        | htc-g[053-055] | H100      | 4     | 82GB       | yes | 10,752     | 12.6                    | no       |
        +----------------+-----------+-------+------------+-----+------------+-------------------------+----------+
        | htc-g056       | MI210     | 4     | 64GB       | yes |            |                         |          |
        +----------------+-----------+-------+------------+-----+------------+-------------------------+----------+
        | htc-g057       | GH200     | 1     | 96GB       | yes | 10,752     | 12.6                    | no       |
        +----------------+-----------+-------+------------+-----+------------+-------------------------+----------+
        | htc-g058       | H100      | 4     | 96GB       | yes | 10,752     | 12.6                    | yes      |
        +----------------+-----------+-------+------------+-----+------------+-------------------------+----------+
        | htc-g[059-060] | H100      | 8     | 80GB       | yes | 10,752     | 12.6                    | yes      |
        +----------------+-----------+-------+------------+-----+------------+-------------------------+----------+

Storage
-------

Our clusters systems share 2PB of high-performance GPFS storage; this holds per-cluster scratch file systems as well as project data storage.

On all nodes with HDR100 interconnect, project data storage is mounted natively; all other nodes access this storage via NFS.

Software
--------

Users may find the application they are interested in running is already been installed on at least one of the systems.  Users are welcome to request the installation of new applications and libraries or updates to already installed applications via our software request form.
