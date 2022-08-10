Copying data to/from ARC
------------------------

MacOS/Linux users (and other Unix like operating systems) can use rsync, sftp, or scp. These commands need to be run on your **local** machine as you can only pull files from ARC or push files to it.  

.. note::

    $HOME and $DATA are shared between the ARC and HTC systems, so the instructions below will work for both systems. ``gateway.arc.ox.ac.uk`` has no access to $HOME, but $DATA is available. 

Copying to the ARC systems
^^^^^^^^^^^^^^^^^^^^^^^^^^

1) Make sure you know the full path to the destination directory on ARC - The best way to to this is to log in to ARC, change to that directory and run the command ``pwd``; this will show you the full path to the directory. 

For example if you have created a directory ``myscripts`` in $DATA, ``pwd`` will show output like::

    [ouit0578@gateway]$ cd $DATA/myscripts
    [ouit0578@gateway]$ pwd
    /data/system/ouit0578/myscripts

2) On your local Mac or Linux PC open a terminal window and change directory to the directory where the file(s) you want to copy **to** ARC are located. The command ``pwd`` will show the full path to this directory, take note of this path. For example if you have a directory named ``scripts`` in your local home directory the path may look something like::

    $ cd scripts
    $ pwd
    /home/user/scripts
 
3) While still working on your MAC or Linux PC: to copy files, use the ``scp`` command with the format::

    scp <source> <destination>
   
    scp local/path/filename arcuserid@gateway.arc.ox.ac.uk:/path_to_destination_directory/
    
.. note::
   The **remote** side of the copy requires you to specify your ARC username followed by the ``@`` symbol, then the name of the machine you want to connect to - in this case ``gateway.arc.ox.ac.uk`` followed by a ``:`` (colon) then the remote directory path. 

Continuing with the above example - to copy all the files in /local/scripts this would be::

    scp /home/user/scripts/* ouit0578@gateway.arc.ox.ac.uk:/data/system/ouit0578/myscripts/

To copy an entire directory hierarchy use the recurse option, -r 

For example::

    scp -r /home/user/scripts/* ouit0578@gateway.arc.ox.ac.uk:/data/system/ouit0578/myscripts/

In both of the above cases, you will be prompted to authenticate with your ARC password.

Copying from the ARC systems
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The reverse should be used for copying from arc. Using the methods above, take note of the source (ARC) and destination (local PC) paths. In this example we will use:
 
ARC directory:  ``/data/system/ouit0578/mydata``
Local PC directory: ``/home/user/datafromarc``
 
Copying data from Mac or Linux PC
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
 
Once again, we must run the scp command on our local machine as we are going to **pull** the data back from ARC.  
 
To copy files from your local PC::
 
    scp ouit0578@gateway.arc.ox.ac.uk:/data/system/ouit0578/mydata/* /home/user/datafromarc/
    
Again a recursive copy can be made using the -r option::

    scp -r ouit0578@gateway.arc.ox.ac.uk:/data/system/ouit0578/mydata/* /home/user/datafromarc/

In both the above cases, you will be prompted to authenticate with your ARC password.

Copying to/from Windows clients
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Windows users can use tools such as MobaXterm or WinSCP to copy files. Use the discovery method in step 1) above to work out the remote ARC path for the transfer.
