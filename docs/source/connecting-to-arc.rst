Connecting to ARC
=================

Access to ARC systems is via Secure Shell Protocol (SSH).

Fingerprints for the login node host keys can be found `here <https://arc-user-guide.readthedocs.io/en/latest/arc-host-keys.html>`_

Connecting from Linux
---------------------

Linux and Mac users should use ssh from a terminal to connect to the ARC systems.

To connect to the ARC cluster::

    ssh -X username@arc-login.arc.ox.ac.uk

To connect to the HTC cluster::

    ssh -X username@htc-login.arc.ox.ac.uk

Access to ARC is available only from within the University of Oxford network. If you are not on the University network, you should use the University VPN service to connect. If you are unable to use the VPN service, you may be able to register your static IP with the ARC team (support@arc.ox.ac.uk) to enable access.

If you are connecting from outside the University network (or from the VPN service) you will need to connect via gateway.arc.ox.ac.uk - ensure you specify your ARC username in the ssh command, as shown below::

    ssh -X username@gateway.arc.ox.ac.uk

You can then SSH to arc-login or htc-login as required.

.. note::

    The above examples include the -X option which allows the tunnelling of X11 graphics from the cluster to your local machine. This is optional. However, if you do require graphics, an X11 server needs to be running on your local machine. For Linux this is typically part of the installation - however on a Mac you may need to install an X11 server such as Xquartz. You can also use the ARC Graphical nodes to render graphics on your local client without using SSH or X11 see the section below on Graphical Nodes for more information.

Connecting from Windows
-----------------------

SSH is available as a command in PowerShell from Windows 10. Users of Windows 10 or newer should be able to connect to ARC from PowerShell with the commands given above. However, users of older Windows versions, or those requiring X11 forwarding, will need to download and install an application that allows them to connect - a popular example is MobaXterm.

MobaXterm for Windows can be found at `https://mobaxterm.mobatek.net/ <https://mobaxterm.mobatek.net/>`_

Connecting using ARC Graphical Nodes
------------------------------------

ARC have a number of graphical interactive nodes which you can use to interact with applications which require GUI operation, such as RStudio, Jupyter Notebooks and ANSYS Workbench. This service uses NoMachine NX to provide a remote desktop environemnt.

In order to use these interactive nodes, you **must** be connected to the university network or be remotely connected via the university VPN service. 

Accessing the Graphical nodes via a web browser
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You can connect directly via web browser to `nx.arc.ox.ac.uk <https://nx.arc.ox.ac.uk>`_ via the web-based client connection (which is lower quality in terms of
visual display). See `Configuring NoMachine Web Client <https://arc-user-guide.readthedocs.io/en/latest/arc-nx-web.html>`_

Accessing the Graphical nodes via the client software
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

You may download the `NoMachine Enterprise Client <https://www.nomachine.com/download-enterprise#NoMachine-Enterprise-Client>`_ and install this on your
local machine. See `Configuring NoMachine Client <https://arc-user-guide.readthedocs.io/en/latest/arc-nx-client.html>`_
