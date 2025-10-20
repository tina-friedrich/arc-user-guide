ARC/HTC Operating System Migration
==================================


Introduction
------------

As part of our ongoing improvements to the ARC service, we are rolling out a Major OS Upgrade: Transitioning from Red Hat Enterprise 8 to Red Hat Enterprise 9. We are upgrading the cluster OS from CentOS 8.1 to AlmaLinux 9.4.

All nodes in the cluster have features that allow to specify the operating system during job submission:

Current Legacy OS:
    - os:redhat7
    - os_version:7.7
    - os_flavour:CentOS

Current OS:
    - os:redhat8
    - os_version:8.1
    - os_flavour:CentOS

New OS:
    - os:redhat9
    - os_version:9.4
    - os_flavour:AlmaLinux

During the transition period, jobs will default to RHEL8 unless explicitly requesting RHEL9. From **1st September 2025** RHEL9 will become the default OS and RHEL8 will need to be explicitly requested.

We strongly encourage users to test workloads on RHEL9-compatible nodes as soon as possible to ensure smooth migration.

The full transition will be completed by October 2025. Please reach out with any questions or concerns.

Migration Timeline
------------------

All nodes including login nodes and nx graphical on both ARC and HTC will be migrated to AlmaLinux 9 by the **end of October 2025**. The legacy nodes which are currently running CentOS 7.7 will be migrated to the current CentOS 8.1 OS.

On **1st September 2025**, Alma9 will be the default OS in the queueing system and you will need to explicitly specify if you want to use a node with the older version by adding the following line in your submission script:

.. code-block:: bash

   #SBATCH --contraint="os:redhat8"

Who is responsible for ensuring my workflow works on the new OS?
----------------------------------------------------------------

Each user is responsible for testing their workflow on the new operating system. The ARC team will be working on bringing as many modules as possible to the new OS, however, some may not be supported on the new platform. When this is the case, ensure you can port your workflow to the latest version of the package as possible. Again, please reach out with any questions or concerns.


How to test my workflow.
------------------------

In order to test your workflow, you will need to explicitly request the new OS when submitting your job as until it is fully rolled out, the cluster will default to the current OS. This can be done to two ways:

You can add the requirement into your script by adding the line:

.. code-block:: bash

  #SBATCH --constraint="os:redhat9"

Alternatively to can add the flag to your sbatch command:

.. code-block:: console

  [user@arc-login ~]$ sbatch --constraint="os:redhat9" mysubmit.sh

.. note::

  Nodes with the new OS are being added to the clusters in batches, and currently not all clusters or types of nodes had instances with the new OS installed. If you submit a job requesting the new OS for specification that do have have the new OS installed you will get the following error:

   .. code-block:: text

    sbatch: error: Batch job submission failed: Invalid feature specification


