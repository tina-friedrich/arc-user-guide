SLURM Reference Guide
=====================

Using the SLURM job scheduler
-----------------------------

**Important note**
This guide is an introduction to the Slurm job scheduler and its use on the ARC clusters. ARC compute nodes typically have two 24 core processors and a range of memory sizes,
from 384GB to 3TB; however, there are some nodes with more (or fewer) cores and/or memory. In addition, some nodes in the HTC cluster have NVidia Tesla GPGPU cards. 

Introduction
------------

Jobs are run as batch jobs, i.e. in an unattended manner. Typically a user logs in to a login node (e.g. arc-login.arc.ox.ac.uk), prepares a job (which contains details of the work to carry out and the computer resources needed) and submits it to the job queue. The user can then log out (if she/he wishes) until their job has run, to collect the output data.

Jobs are managed by SLURM , which is in charge of:

- allocating the computer resources requested for the job,
- running the job and
- reporting the outcome of the execution back to the user.

Running a job involves, at the minimum, the following steps:

- preparing a submission script and
- submitting the job to execution.

This guide describes basic job submission and monitoring for SLURM.  The topics in the guide are:

- the main SLURM commands,
- preparing a submission script,
- SLURM partitions,
- submitting a job to the queue,
- monitoring a job execution,
- deleting a job from the queue and
- environment variables.
- job dependencies
- job arrays

Commands
--------

The table below gives a short description of the most used SLURM commands.

+---------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| Command | Description                                                                                                                                                                                       |
+=========+===================================================================================================================================================================================================+
| sacct   | Report job accounting information about active or completed jobs                                                                                                                                  |
+---------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| salloc  | Allocate resources for a job in real time (typically used to allocate resources and spawn a shell, in which the srun command is used to launch parallel tasks                                     |
+---------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| sbatch  | Submit a job script for later execution (the script typically contains one or more srun commands to launch parallel tasks)                                                                        |
+---------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| scancel | Cancel a pending or running job                                                                                                                                                                   |
+---------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| sinfo   | Reports the state of partitions and nodes managed by SLURM (it has a variety of filtering, sorting, and formatting options)                                                                       |
+---------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| squeue  | Reports the state of jobs (it has a variety of filtering, sorting, and formatting options), by default, reports the running jobs in priority order followed by the pending jobs in priority order |
+---------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+
| srun    | Used to submit a job for execution in real time                                                                                                                                                   |
+---------+---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+


All SLURM commands have extensive help through their man pages, for example::

  man sbatch
  
Will show you the help pages for the **sbatch** command.

Preparing a submission script
-----------------------------

A submission script is a shell script that:

- describes the processing to carry out (e.g. the application, its input and output, etc.) and
- requests computer resources (number of cpus, amount of memory, etc.) to use for processing.

The simplest case is that of a job that requires a single node (this is the smallest unit we allocate on ARC) with the following requirements:

- the job uses 1 node,
- the application is a single process,
- the job will run for no more than 100 hours,
- the job is given the name "test123" and
- the user should be emailed when the job starts and stops or aborts.

Example 1: job running on a single node
---------------------------------------

Supposing the application is called myCode and takes no command line arguments, the following submission script runs the application in a single job::

    #!/bin/bash
    # set the number of nodes
    #SBATCH --nodes=1
    # set max wallclock time
    #SBATCH --time=100:00:00
    # set name of job
    #SBATCH --job-name=test123
    # mail alert at start, end and abortion of execution
    #SBATCH --mail-type=ALL
    # send mail to this address
    #SBATCH --mail-user=john.brown@gmail.com
    
    # run the application
    myCode
    
The script starts with ``#!/bin/bash`` (also called a shebang), which makes the submission script a Linux bash script.

The script continues with a series of lines starting with #, which represent bash script comments.  For SLURM, the lines starting with **#SBATCH** are directives that request job scheduling resources.  (Note: it's very important that you put all the directives at the top of a script, before any other commands; any **#SBATCH** directive coming after a bash script command is ignored!)

The resource request ``#SBATCH --nodes=n`` determines how many compute nodes a job are allocated by the scheduler; only 1 node is allocated for this job.  A note of caution is on threaded single process applications (e.g. Matlab).  These applications cannot run on more than a single compute node; allocating more (e.g. **#SBATCH --nodes=2**) will end up with the first node being busy and the rest idle.

The maximum walltime is specified by ``#SBATCH --time=T`` where T has format hh:mm:ss.  Normally, a job is expected to finish before the specified maximum walltime.  After the walltime reaches the maximum, the job terminates regardless whether the job processes are still running or not. 

The name of the job can be specified too with ``#SBATCH --job-name="name"``

Lastly, an email notification is sent if an address is specified with ``#SBATCH --mail-user=<email_address>``  The notification options can be set with ``#SBATCH --mail-type=<type>`` where <type> may be BEGIN, END, FAIL, REQUEUE or ALL (for any change of job state).

The final part of a script is normal Linux bash script and describes the set of operations to follow as part of the job.  The job starts in the same folder where it was submitted (unless an alternative path is specified), and with the same environment variables (modules, etc.) that the user had at the time of the submission.  In this example, this final part only involves invoking the myCode application executable.

Example 2: job running on multiple nodes
----------------------------------------

As a second example, suppose we want to run an MPI application called myMPICode with the following requirements:

- the run uses 2 nodes,
- the job will not run for more than 100 hours,
- the job is given the name "test123" and
- the user should be emailed when the job starts and stops or aborts.

Supposing no input needs to be specified, the following submission script runs the application in a single job::

    #!/bin/bash
    # set the number of nodes and processes per node
    #SBATCH --nodes=2
    # set the number of tasks (processes) per node.
    #SBATCH --ntasks-per-node=16
    # set max wallclock time
    #SBATCH --time=100:00:00
    # set name of job
    #SBATCH --job-name=test123
    # mail alert at start, end and abortion of execution
    #SBATCH --mail-type=ALL
    # send mail to this address
    #SBATCH --mail-user=john.brown@gmail.com
    
    mpirun $MPI_HOSTS myMPICode

In large part, the script above is similar to the one for a single node job except in this example, ``#SBATCH --ntasks-per-node=m`` is used to reserve m cores per node and to
prepare the environment for a MPI parallel run with m processes per each compute node.

Slurm partitions
----------------

Slurm partitions are essentially different queues that point to collections of nodes.

You can specify the Slurm partition by adding the #SBATCH --partition= directive to the top of your submission script so adding::

  #SBATCH --partition=devel 

will send your job to the devel partition. Alternatively, the partition can be supplied with the sbatch command like this::

  sbatch --partition=devel JOBSCRIPT.sh
  
Defining a partition on the sbatch command line takes precedence over the definition in the jobscript.

You can see the current state of the partitions with the sinfo command. 

All Slurm commands have extensive help through their man pages; try for example::

  man sbatch

Submitting jobs with the command sbatch
---------------------------------------

Once you have a submission script ready (e.g submit.sh), the job is submitted to the execution queue with the command::

  sbatch submit.sh

The queueing system prints a number (the job id) almost immediately and returns control to the linux prompt.  At this point the job is in the submission queue.

Once you have submitted the job, it will sit in a pending state until the resources have been allocated to your job (the length of time your job is in the pending
state is dependent upon a number of factors including how busy the system is and what resources you are requesting). You can monitor the progress of the job using the
command squeue (see below).

Once the job starts to run you will see files with names such as slurm-1234.out either in the directory you submitted the job from (default behaviour) or in the directory
where the script was instructed explicitly to change to. 

Monitoring jobs with the command squeue
---------------------------------------

squeue is the main command for monitoring the state of systems, groups of jobs or individual jobs.

The command squeue prints the list of current jobs.  The list looks something like:: 

  JOBID	  PARTITION   NAME      USER    ST    TIME    Nodes NODELIST(REASON)
  2497	  short       test1.14  bob     R     0.07    1     arc-c252
  2499	  long        test1.35	mary    R     0.22    4     arc(200-203)
  2511	  devel       ask.for.	steve   PD    0.00    1     (Resources)

The first column gives the job ID, the second the partition (or queue) where the job was submitted, the third the name of the job (specified by the user
in the submission script) and the fourth the owner of the job.  The fifth is the status of thejob (R=running, PD=pending, CA=cancelled, CF=configuring, CG=completing,
CD=completed, F=failed). The sixth column gives the elapsed time for each particular job.  Finally, there are the number of nodes requested and the nodelist where
the job is running (or the cause that it is not running).

Some other useful squeue features include::

  -u for showing the status of all the jobs of a particular user, e.g. squeue -u bob for user bob;
  -l for showing more of the  available information;
  --start to report  the  expected  start  time  of pending jobs.
 
Read all the options for squeue on the Linux manual using the command ``man squeue`` including how to personalize the information to be displayed.

Deleting jobs with the command scancel
--------------------------------------

Use the scancel command to delete a job, for example::

  scancel 1121 
  
to delete job with ID 1121.  A user can delete his/her own jobs at any time, whether the job is pending (waiting in the queue) or running.  
A user cannot delete the jobs of another user.  Normally, there is a (small) delay between the execution of the scancel command and the time 
when the job is dequeued and killed.  Occasionally a job may not delete properly, in which case, the ARC support team can delete it upon request.

Environment variables
---------------------

At the time a job is launched into execution, Slurm defines multiple environment variables, which can be used from within the submission script to
define the correct workflow of the job.  The most useful of these environment variables are the following::

  SLURM_SUBMIT_DIR, which points to the directory where the sbatch command is issued;
  SLURM_JOB_NODELIST, which returns the list of nodes allocated to the job;
  SLURM_JOB_ID, which is a unique number Slurm assigns to a job.

In most cases, SLURM_SUBMIT_DIR does not have to be used, as the job goes by default to the directory where the slurm command was issued.  This behaviour of Slurm is in contrast with other schedulers, such as Torque, which goes to the home directory of the user account.  SLURM_SUBMIT_DIR can be useful in a submission script when files must be copied to/from a specific directory that is different from the directory where the slurm command was issued.

SLURM_JOB_ID is useful to tag job specific files and directories, typically output files or run directories.  For instance, the submission script line::

  myApp > $SLURM_JOB_ID.out
  
runs the application myApp and redirects the standard output to a file whose name is given by the job ID.  The job ID is a number assigned by Slurm and differs from
the character string name given to the job in the submission script by the user.

Job Dependencies
----------------

Job dependencies are used to defer the start of a job until the specified dependencies have been satisfied.

They are specified with the --dependency option to sbatch in the format::

  sbatch --dependency=<type:job_id[:job_id][,type:job_id[:job_id]]> ...

Dependency types::

  after:jobid[:jobid...]	job can begin after the specified jobs have started
  afterany:jobid[:jobid...]	job can begin after the specified jobs have terminated
  afternotok:jobid[:jobid...]	job can begin after the specified jobs have failed
  afterok:jobid[:jobid...]	job can begin after the specified jobs have run to completion with an exit code of zero

For example::

  sbatch job1.sh
  1802051
  sbatch --dependency=afterok:1802051 job2.sh
  
In the above example, job script job1.sh is submitted and is given a JobID of 1802051. We then submit job2.sh with a dependency that it only run
when job 1802051 has completed.

Job Arrays
----------

Job arrays offer a mechanism for submitting and managing collections of similar jobs quickly and easily. In general, job arrays are useful for applying the same processing routine to a collection of multiple input data files. Job arrays offer a very simple way to submit a large number of independent processing jobs.

By submitting a single job array sbatch script, a specified number of “array-tasks” will be created based on this “master” sbatch script. 

For example::

    #!/bin/bash
    #SBATCH --job-name=arrayJob
    #SBATCH --output=arrayJob_%A_%a.out
    #SBATCH --error=arrayJob_%A_%a.err
    #SBATCH --array=1-4
    #SBATCH --time=02:00:00

    # Print this sub-job's task ID
    echo "My SLURM_ARRAY_TASK_ID: " $SLURM_ARRAY_TASK_ID

    # Run "application" using input filename modified by SLURM_ARRAY_TASK_ID
    ./application input_$SLURM_ARRAY_TASK_ID.txt
    
The above example uses the --array=1-4 specification to create four array tasks which run the command "application" on different input files, the filename of each being modified by the SLURM_ARRAY_TASK_ID variable. 

The %A_%a construct in the output and error file names is used to generate unique output and error files based on the master job ID (%A) and the array-task's ID (%a). In this fashion, each array-task will be able to write to its own output and error file.

For clarity, the input and output files for the above script, if submited as jobID 1802055 would be::

  JobID     --output                --error	                Application Input filename
  1802055_1	arrayJob_1802055_1.out  arrayJob_1802055_1.err  input_1.txt
  1802055_2	arrayJob_1802055_2.out  arrayJob_1802055_2.err  input_2.txt
  1802055_3	arrayJob_1802055_3.out	arrayJob_1802055_3.err	input_3.txt
  1802055_4	arrayJob_1802055_4.out	arrayJob_1802055_4.err	input_4.txt

Note: You can specifiy the ``--array`` option on the ``sbatch`` command line instead of inside the submission script. For example if the ``--array`` option was removed from the above script and the script was named **jobArray.sh** the command would be::

  sbatch --array=1-4 jobArray.sh

More information about Slurm job arrays can be found in the Slurm Job Array Documentation
