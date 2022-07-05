General FAQs
============
  
How do I become a ARC user?
---------------------------
The supercomputing facility is available to all Oxford University researchers.  You can become a user by registering with the ARC. 
Start with the `User registration Page <https://www.arc.ox.ac.uk/getting-started-obtaining-an-account>`_

Where should a new ARC user begin?
----------------------------------
Look at information in `this section of the ARC website. <https://www.arc.ox.ac.uk/what-next>`_

What systems can I access as a user?
------------------------------------
All registered users have access to all the ARC systems.

How much disk space do I have?
------------------------------
Default quota on ``$HOME`` is 15 gigabytes (GB) per user and on ``$DATA`` is 5 terabytes (TB) per project/group.  Larger quotas limits are available on request.

How do I log on to the ARC systems?
-----------------------------------
Linux and Mac users should use ``ssh`` to connect to the ARC systems.  For example, issuing the following command:: 

  ssh -X bob@system.arc.ox.ac.uk

from a Linux or Mac terminal, the user bob log on to **system** (**system** could be ``arc-login`` or ``htc-login``).  The user is prompted to provide the password.

We recommend the use of the ``-X`` flag to ``ssh``, which allows users to run graphical applications remotely (such as the emacs editor).  This option allows X11 forwarding using subject to security control.

Windows users should install an application called ``PuTTY``. To connect to one of the ARC machines, ``PuTTY`` has to operate in the ``ssh``
mode.  To allow remote applications to display graphics through the link, the X11 tunelling option has to be enabled.  (The best way to learn about how to do this
is to search the web for "putty x11 tunnelling".)  Additionally, Windows users that wish to use X11 graphics via ``PuTTY`` must install a X11 server, and ``xming`` is arguably the best option. 

Windows users can also use a combined SSH/X-Server client such as `MobaXTerm <https://mobaxterm.mobatek.net/>`_ to connect to ARC systems.

How do I transfer files to/from the ARC systems?
------------------------------------------------
Linux and Mac users should use ``scp`` for transfering files.  For example, the command::

   scp localfolder/myfile.txt bob@system.arc.ox.ac.uk:/path/to/remote/folder

copies the file ``myfile.txt`` from the local host to system in the directory ``/path/to/remote/folder`` on the ARC system.  Also::

   scp bob@system.arc.ox.ac.uk:/path/to/remote/folder/myfile.txt localfolder/

copies myfile.txt from the remote directory to the local one.  In both cases, the target file is overwritten if it exists.  Study the scp Linux manual (man scp)
to learn more; for example the -r (recursive) option is useful for transferring entire directories.

Linux and Mac users may also find ``rsync`` very useful, for instance for maintaining directory structures on their workstation in sync with copies on the ARC storage.

The command::

   rsync -avz localfolder bob@system.arc.ox.ac.uk:/path/to/remote/folder

copies the directory ``localfolder`` to the directory ``/path/to/remote/folder`` on the ARC system. The files are transferred recursively in "archive" mode, which ensures that symbolic links, permissions, ownerships, etc. are preserved.  The example above also uses compression ``-z`` to reduce the size of the transferred data. Unlike ``scp``, ``rsync`` does not simply overwrite existing files but rather updates, transferring only the differences between two files.

Windows users can use ``pscp``, usually bundled with ``PuTTY``.  Alternatively, ``WinSCP`` is a very easy to use, open source scp client for Windows.

 
How do I access the ARC systems from outside the University network?
--------------------------------------------------------------------
There are two main ways to access the ARC systems from outside the University network:

By connecting to the University of Oxford virtual private network (VPN) and accessing the ARC systems as though users were on campus
(see `University VPN Information<http://help.it.ox.ac.uk/network/vpn/index>`_ for more details).

By connecting to the ARC external access server, ``gateway.arc.ox.ac.uk`` gateway has a firewall in place and only permits access from known locations.
Thus, users need to provide the ARC (static) IP addresses from the location that they need to connect from.  This should be an IP address from an identifiable institution. 

The first method is the preferred form for any users who have University SSO passwords.  The second method is useful for users who are external collaborators.

 
How do I acknowledge ARC in my publications?
--------------------------------------------
Please see the acknowledgements section on the ARC Terms and Conditions page.

 
Will application X run on the ARC supercomputers faster than on my workstation?
-------------------------------------------------------------------------------
We hope so, but it may not for many reasons.  If you wish to investigate whether you can achieve speed up on your application, then please contact us.

 
How many credits do I have left?
--------------------------------
Use the ``mybalance`` command on ARC or HTC to find out how many credits you have left.

 
How do I change my password?
----------------------------
Use the ``passwd`` command on the login nodes to change your password.

 
I have forgotten my password. How do I reset my password?
---------------------------------------------------------
If you have forgotten your password or your password has expired and you can no longer access ARC to change it yourself, you will need to contact us using
the support email address.  We will then issue a temporary password via email.

 
I accidentally deleted files, how do I get them back?
-----------------------------------------------------
Unfortunately ARC does not keep dedicated backups of its storage resources.  We recommend that users store data at sites other than the ARC, for example, on
departmental resources.
