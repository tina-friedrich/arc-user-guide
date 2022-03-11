ARC Storage
===========

Once your account has been created, you will immediately have access to two persistent storage areas:

**$HOME** (/home/username) with a 15GB quota

**$DATA** (/data/projectname/username)  sharing a 5TB quota with your project colleagues

Additionally, when you run a SLURM job, a per-job **$SCRATCH** and **$TMPDIR** for temporary data/workfiles is created. 

**$TMPDIR** is local to a compute node

**$SCRATCH** is on a shared file system and available to all nodes in a job, if a job spans multiple nodes.

Note: Both **$SCRATCH** and **$TMPDIR** are not persistent; they will be automatically removed on job exit. It is important that your job copies all files into your $DATA area before it exits; we will not be able to recover your data if you left it on **$SCRATCH** or **$TMPDIR** once a job finished.

As a rule we recommend that you use your **$DATA** area to store your data, but utilise the per job **$SCRATCH** or **$TMPDIR** area - especially for intermediate or temporary files. Generally you would copy all required input data at the start of your job and then copying results back to your **$DATA** area.

A simple example of how to do this would be::

  #!/bin/bash
  cd $SCRATCH || exit 1

  rsync -av $DATA/myproject/input ./
  rsync -av $DATA/myproject/bin ./ 

  module load foss/2020b

  mpirun ./bin/my_software

  rsync -av --exclude=input --exclude=bin ./ $DATA/myproject/
  
This example copies directories '$DATA/myproject/input' and '$DATA/myproject/bin' into $SCRATCH (which will then contain directories 'input' and 'bin'); runs './bin/my_software'; and copies all files in the $SCRATCH directory - excluding directories 'input' and 'bin' - back to $DATA/myproject/ once the mpirun finishes.

If you are unable to access either of these directories, please let us know.

Quota
-----

By default your **$HOME** area will have a 15GB quota while the **$DATA** area will have a 5TB quota that is shared between yourself and the other members of your project.

To check your quota use the command::

  myquota

This command will list both your home quota and the quota of shared project data areas that you are a member of.

We can provide more detailed statements of data area quota usage to project leaders on request.

Larger Data quotas (more than 5TB) are available on request as a chargeable service. Please contact ARC support for further information.

Backups
-------

We do NOT currently create backups of the ARC shared file system (although the file system IS resilient to failures). We therefore strongly encourage you to keep copies of your files elsewhere, particularly when that data is critical to your research.

Snapshots
---------

Snapshots have been configured to be generated on home directories. Snapshots provide easy access to older versions of files. This is useful if files have been accidentally deleted or overwritten. It does not, however, constitute a backup; old snapshots will not be kept indefinitely (max. two weeks for weekly snapshots).

Within your home directory, there is a .snapshot directory which contains the hourly, daily and weekly snapshots available. 
To list/examine the snapshots, simply 'cd' into $HOME/.snapshot and list the available directories::

  cd $HOME/.snapshot
  ls -1tr

You will see a listing of all snapshots (reverse order, i.e. newest last)::

  weekly.2020-08-02_0015
  weekly.2020-07-26_0015
  daily.2020-08-06_0010
  hourly.2020-08-07_1105
  hourly.2020-08-07_1005
  hourly.2020-08-07_0905
  daily.2020-08-07_0010
  hourly.2020-08-07_1305
  hourly.2020-08-07_1205
  hourly.2020-08-07_1405

To choose a particular snapshot, simply change into the relevant directory::

  cd hourly.2020-08-07_1205

Within those directories you will essentially find a copy of your home directory as it was when the snapshot was taken.

If you've accidentally deleted a file in your home directory which existed earlier than the last snapshot, then you can retrieve the older copy from the snapshot. Simply find the version of the file you are after within the .snapshot structure, and copy it back into your home directory.

For example - assuming you have deleted a file 'ARC-Introduction-2018-Hilary.pptx' from folder $HOME/Documents by mistake. To recover it, the steps would be::

  [$(arcus) Documents]$ pwd
  /home/ouit0622/Documents

  [$(arcus) Documents]$ ls -1
  ARC-Introduction-2018-Hilary.pptx
  arc_job_submission_exercises
  arc_presentation
  MATLAB

  [$(arcus) Documents]$ rm ARC-Introduction-2018-Hilary.pptx

  [$(arcus) Documents]$ ls -1
  arc_job_submission_exercises
  arc_presentation
  MATLAB

  [$(arcus) Documents]$ cd $HOME/.snapshot/
  [$(arcus) .snapshot]$ ls -1tr
  weekly.2020-08-02_0015
  weekly.2020-07-26_0015
  daily.2020-08-06_0010
  hourly.2020-08-07_1105
  hourly.2020-08-07_1005
  hourly.2020-08-07_0905
  daily.2020-08-07_0010
  hourly.2020-08-07_1305
  hourly.2020-08-07_1205
  hourly.2020-08-07_1405

  [$(arcus) .snapshot]$ cd hourly.2020-08-07_1405

  [$(arcus) hourly.2020-08-07_1405]$ pwd
  /home/ouit0622/.snapshot/hourly.2020-08-07_1405

  [$(arcus) hourly.2020-08-07_1405]$ cd Documents

  [$(arcus) Documents]$ ls -1
  ARC-Introduction-2018-Hilary.pptx
  arc_job_submission_exercises
  arc_presentation
  MATLAB

  [$(arcus) Documents]$ cp ARC-Introduction-2018-Hilary.pptx $HOME/Documents

  [$(arcus) Documents]$ $HOME/Documents/
  [$(arcus) Documents]$ pwd
  /home/ouit0622/Documents

  [$(arcus) Documents]$ ls -1
  ARC-Introduction-2018-Hilary.pptx
  arc_job_submission_exercises
  arc_presentation
  MATLAB
  
Note: Snapshots do not take up space in the file system, i.e. they do not count towards your quota. If you are trying to determine where in your home directory space is used,
you must exclude the .snapshot directory from your commands as otherwise the information would be incorrect.
