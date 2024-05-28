Submitting Priority Jobs
========================

Jobs submitted to ARC cluster default to the standard service level.  To purchase priority credit see the `ARC Accounting <https://www.arc.ox.ac.uk/arc-accounting>`_ page for details.  Once your project is set up with priority credits, you can check the balance of your ARC credit using the ``mybalance`` command.  You'll find now that the command reports balance for two accounts.  One account is for your standard credit.  The account with the ``-priority`` suffix is for your priority credit.

Submit jobs with priority QoS (Quality of Service)
--------------------------------------------------

To submit jobs with higher priority, you need to add the ``--qos=priority`` option to your ``sbatch`` submission.  This can be on the command line::

  sbatch --qos=priority ...

where "..." is replaced by whatever other options you might normally include on your ``sbatch`` commands.

Or you can include an ``#SBATCH`` directive comment at the beginning of your submission script::

  #SBATCH --qos=priority

A job submitted with the "Quality of Service" (qos) setting "priority" will run with higher priority and consume credits from the ``-priority`` account.
When you run out of priority credit your priority jobs will be held.  They can have their QOS set to normal and then they will be able to run as standard priority jobs.
