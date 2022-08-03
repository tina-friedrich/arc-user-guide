Copying data to/from ARC
------------------------

MacOS/Linux users (and other Unix like operating systems) can use rsync, sftp, or scp. 

.. note::

    $HOME and $DATA are shared between the ARC and HTC systems, so the instructions below will work for both systems. gateway.arc.ox.ac.uk has no access to $HOME, but $DATA is available. 

Copying to the ARC systems
^^^^^^^^^^^^^^^^^^^^^^^^^^

1) Make sure you know the path to the destination directory. Login to ARC and create a directory in $DATA. Change to that directory and run the command 'pwd'; this will show you the full path to the destination directory. For example if you have created a directory myscripts in $DATA, 'pwd' will show output like::

    [ouit0578@gateway Scripts]$ pwd
    /data/system/ouit0578/myscripts

2) On your Mac or Linux PC open a terminal use the command 'cd directoryname' to get to the source directory where the file(s) you want to copy are located. The command pwd will show the full path to this directory, take note of this path. For example if you have a directory scripts the path might be something like::

    Scripts$ pwd
    /local/scripts
 
3) Still on your MAC or Linux PC to copy files use an scp command with the format::

    scp path/filename arcuserid@gateway.arc.ox.ac.uk:/path_to_destination_directory/

Continuing with the above example - to copy all the files in /local/scripts this would be::

    scp /local/scripts/* ouit0578@gateway.arc.ox.ac.uk:/data/system/ouit0578/myscripts/

To copy an entire directory hierarchy use the recurse option, -r 

For example::

    scp -r /local/scripts/* ouit0578@gateway.arc.ox.ac.uk:/data/system/ouit0578/myscripts/

In both the above cases, you will be prompted to authenticate with your ARC password.

Copying from the ARC systems
^^^^^^^^^^^^^^^^^^^^^^^^^^^^

The reverse should be used for copying from arc. Using the methods above, take note of the source (ARC) and destination (local PC) paths. In this example these will be::
 
ARC directory:  /data/system/ouit0578/mydata

Local PC directory: /local/datafromarc
 
Copying data from Mac or Linux PC
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
 
To copy files from your local PC::
 
    scp ouit0578@gateway.arc.ox.ac.uk:/data/system/ouit0578/mydata/* /local/datafromarc/
    
Again a recursive copy can be made using the -r option::

    scp -r ouit0578@gateway.arc.ox.ac.uk:/data/system/ouit0578/mydata/* /local/datafromarc/

In both the above cases, you will be prompted to authenticate with your ARC password.

Copying to/from Windows clients
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

Windows users can use tools such as MobaXterm or WinSCP to copy files. Use the discovery method in step 1) above to work out the remote ARC path for the transfer.
