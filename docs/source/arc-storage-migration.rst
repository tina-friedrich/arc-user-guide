ARC Storage (Migration)
=======================


A short paragraph explaining why the new storage will be faster/better?
-----------------------------------------------------------------------

Over the last year the ARC team has been working on replacing part of the storage infrastructure behind the ARC and HTC clusters. This was necessary since the current storage infrastructure is reach end of life almost full, with more projects being added regularly, and scratch storage being more and more in demand and requirements for improved performance. 

Reminder about ``$HOME``, ``$DATA`` and ``$SCRATCH`` link to web page explanation
---------------------------------------------------------------------------------

The new storage covers 2 of the 3 different storage facilities provided by ARC, i.e. DATA and SCRATCH. The third, HOME, is currently not being upgraded. DATA is the shared permanent storage available to projects' users to store research data required and/or generated but jobs run on the clusters. SCRATCH is the temporary storage created at the beginning of the job which can be used by programs to store temporary data shared by processes during a job run. SCRATCH space is deleted after the job is stopped. 

More information on the different types of storage can be found on the ARC user guide at https://arc-user-guide.readthedocs.io/en/latest/arc-storage.html 

New storage/``/migration`` storage area
---------------------------------------

We have created all projects' and users' directories on the new storage and these can now be accessed under ``/migration/$PROJECT/$USER`` Each user is responsible for copying their own data to the new location. We would advise to copy data – not move it – as moving it takes longer, plus a copy process allows to confirm the files were transferred successfully. 

Once a project's data directory is fully migrated, we can 'switch' which area is mounted under /data/ on a per project basis. It would, likewise, be possible to mount the 'new' emtpy storage as ``/data/`` and mount the current file system under ``/migration``, which would allow for new data being produced in the correct place whilst old data continues to be transferred. Please contact ‘support@arc.ox.ac.uk’ if you would like your storage area switched, or discuss those options. 

How to transfer data
--------------------

There are many ways to copy files from one folder to another but not all are appropriate in this case. As mentioned above, using mv is not advisable as you do not want to remove the data from the old storage. ``cp`` is also not advisable as it is very slow. ``rsync`` is probably the best option, as it is interruptible and resumable, but may not be the fastest solution for very large trees. For very large trees, using a ``tar | tar`` solution may be faster.

The rsync solution looks like the following:

.. code-block:: shell

  cd /data/<projectname>/$USER
  rsync –avhP . /migration/<projectname>/$USER/

Alternatively, using tar can be done with the following method:

.. code-block:: shell

  cd /data/<projectname>/$USER
  tar cvf - . | tar xf - -C /migration/<projectname>/$USER/ 

These can be run from an nx session, an interactive session, or submitted as a job on the cluster. An example submission script would look something like:

.. code-block:: bash

  #!/bin/bash 
  #SBATCH --nodes=1 
  #SBATCH --ntasks-per-node=1 
  #SBATCH --cpus-per-task=2 
  #SBATCH --partition=short 
  #SBATCH --job-name=Data_migration 
  
  module purge 
  
  cd /data/<projectname>/$USER 
  
  # choose a method of transfer (uncomment the one you want to use) 
  #rsync -avhP . /migration/<projectname>/$USER/ 
  #tar cvf - . | tar xf - -C /migration/<projectname>/$USER/


Be careful when using a cluster job, and especially when copying in an interactive session; the time limit might interrupt your transfer before it is complete.

Who is responsible for migrating the data?
------------------------------------------

Each user is responsible for transferring their data; however, the project PI or a user appointed by the project PI is responsible for gathering progress from all project users and make the decision for when the whole project should be switched from the old storage to the new. The switch from old to new has to be done on a project basis. We cannot move users individually.

How long will my data be available on the old storage after migration?
----------------------------------------------------------------------


 
If you are unable to access either of these directories, please let us know.
