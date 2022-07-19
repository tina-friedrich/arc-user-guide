
Submission Script Basics
------------------------


**What is a submission script**

A ``submission script`` describes the resources you wish the resource manager ``SLURM`` to allocate to your job, and also what commands you wish to run, including any set-up
these commands may need.

The script needs to be created using a Linux text editor such as ``nano`` or ``vi`` - we recommend creating and editing submission scripts on the cluster rather than editing
them on a Windows machine, as this can cause problems.

**Submission Script Example**

In this example we are going to create a submission script to run a test application on the cluster. To begin with we change directory to your $DATA area and make a new directory
to work in::

  cd $DATA
  mkdir example
  cd example
  
We now have a directory named ``example`` in your ``$DATA`` area. Now we need to create the submission script to describe your job to SLURM. First use the ``nano`` editor 
to create the file::

  nano submit.sh

This command will start the Linux ``nano`` editor. You can use this to add the following lines, which will be explained as we go on::

  #! /bin/bash
  #SBATCH --nodes=1
  #SBATCH --ntasks-per-node=8
  #SBATCH --time=00:10:00
  #SBATCH --partition=devel
  
  module load mpitest
  
  mpirun mpisize

.. note::
  Ensure the ``#! /bin/bash`` line is the first line of the script and the ``#SBATCH`` lines start at the beginning of the line.

To exit ``nano`` hold ``CTRL-X`` then answer ``Y`` to the question ``Save Modified buffer?`` then hit ``enter`` when asked ``File Name to Write: submit.sh``

**The anatomy of the script**

The first line ``#! /bin/bash`` tells Linux that this file is a script which can be run by the BASH shell interpreter. 

The following ``#SBATCH`` lines request specific cluster resources: 

``--nodes=1`` requests one ARC node
``--ntasks-per-node=48`` requests 8 cores
``--time=00:10:00`` requests a run time of 10 minutes (the maximum for the ``devel`` partition)
``--partition=devel`` requests that this job runs on the ``devel`` partition, which is reserved for testing

**Submitting the job**

Now that you have a submission script, you can submit it to the SLURM resource manager. To do this type the following at the command line::

  sbatch submit.sh
  
SLURM will respond with::

  sbatch: CPU resource required, checking settings/requirements...
  Submitted batch job nnnnnnnnn
  
Where ``nnnnnnnnn`` is your job number.

