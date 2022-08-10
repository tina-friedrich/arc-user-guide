Copying data to/from ARC
------------------------

MacOS/Linux users (and other Unix like operating systems) can use rsync, sftp, or scp. These commands need to be run on your **local** machine as you can only pull files from ARC or push files to it.  

.. note::

    $HOME and $DATA are shared between the ARC and HTC systems, so the instructions below will work for both systems. ``gateway.arc.ox.ac.uk`` has no access to $HOME, but $DATA is available. 

Copying to the ARC systems
^^^^^^^^^^^^^^^^^^^^^^^^^^

1) Make sure you know the full path to the destination directory on ARC - The best way to to this is to log in to ARC change to that directory and run the command 'pwd'; this will show you the full path to the directory. For example if you have created a directory ``myscripts`` in $DATA, ``pwd`` will show output like::

    [ouit0578@gateway]$ cd $DATA/myscripts
    [ouit0578@gateway]$ pwd
    /data/system/ouit0578/myscripts

2) On your Mac or Linux PC open a terminal window and change directory to the local directory where the file(s) you want to copy are located. The command ``pwd`` will show the full path to this directory, take note of this path. For example if you have a directory named ``/local/scripts`` the path might be something like::

    $ cd /local/scripts
    $ pwd
    /local/scripts
 
3) While still working on your MAC or Linux PC: to copy files, use the ``scp`` command with the format::

    scp <source> <destination>
   
    scp local/path/filename arcuserid@gateway.arc.ox.ac.uk:/path_to_destination_directory/

Continuing with the above example - to copy all the files in /local/scripts this would be::

    scp /local/scripts/* ouit0578@gateway.arc.ox.ac.uk:/data/system/ouit0578/myscripts/

.. note::
   Note in the above example we are using the username ``ouit0578`` to connect to ARC via ``gateway.arc.ox.ac.uk`` with the destination ARC path. You should, of course, use your ARC username.


To copy an entire directory hierarchy use the recurse option, -r 

For example::

    scp -r /local/scripts/* ouit0578@gateway.arc.ox.ac.uk:/data/system/ouit0578/myscripts/

In both of the above cases, you will be prompted to authenticate with your ARC password.

Copying from the ARC systems
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The reverse should be used for copying from arc. Using the methods above, take note of the source (ARC) and destination (local PC) paths. In this example we will use:
 
ARC directory:  ``/data/system/ouit0578/mydata``
Local PC directory: ``/local/datafromarc``
 
Copying data from Mac or Linux PC
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
 
Once again, we must run the scp command on our local machine as we are going to **pull** the data back from ARC.  
 
To copy files from your local PC::
 
    scp ouit0578@gateway.arc.ox.ac.uk:/data/system/ouit0578/mydata/* /local/datafromarc/
    
Again a recursive copy can be made using the -r option::

    scp -r ouit0578@gateway.arc.ox.ac.uk:/data/system/ouit0578/mydata/* /local/datafromarc/

In both the above cases, you will be prompted to authenticate with your ARC password.

Copying to/from Windows clients
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Windows users can use tools such as MobaXterm or WinSCP to copy files. Use the discovery method in step 1) above to work out the remote ARC path for the transfer.
