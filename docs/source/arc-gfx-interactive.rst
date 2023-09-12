Using the ARC desktop environment
=================================

ARC provide a graphical login service, to facilitate access to GUI applications such as RStudio, Jupyter Notebooks, and ANSYS Workbench. This service uses NoMachine NX to provide a remote desktop.

In order to use this service, you must be connected to the university network or be remotely connected via the university VPN service. See  `Connecting to ARC <https://arc-user-guide.readthedocs.io/en/latest/connecting-to-arc.html>`_ for details how to connect to the graphical login nodes.

NoMachine NX allows you to detach from a session, and reconnect to it later - simply close your browser or NX client windows. Processes on the NX nodes will continue to run once you've detached. You can reconnect to a session later; your running sessions will be presented to you when you reconnect. However, exiting a session (or logging out of the desktop environent) will terminate the session, terminating all processes running within it. 

Once you have connected to the NX service by one of the described methods, you will be presented with the ARC desktop environment as shown below:

.. image:: images/arc-desktop.png
  :width: 800
  :alt: ARC Desktop
  
You can use the menu bar at the bottom of the window to access applications or, as in the example below, open the ``Konsole`` terminal window:

.. image:: images/arc-konsole.png
  :width: 800
  :alt: ARC Konsole

It is possible to access the clusters from the ARC desktop environment. Open a terminal as described above, and run::

    module load cluster/arc

to access the 'ARC' cluster or::

    module load cluster/htc

for access to the 'HTC' cluster.

The graphical login nodes provide fast access to the data file system; they can (and should) be used for pre- or post-processing. 

  
.. note::
  While it may look like you have your own Linux desktop to work with, the interactive nodes where you are running this desktop are 
  shared with other ARC users, and should not be used to run computationally demanding jobs. 
  
  To run applications that are more demanding, please open a ``Konsole`` shell window and start an interactive X11 
  session on a compute node by following the instructions below:
              
  To run an interactive session on the ARC cluster::
  
     module load cluster/arc
     srun -p interactive --x11 --pty /bin/bash
    
  To run an interactive session on the HTC system::
                
     module load cluster/htc
     srun -p interactive --x11 --pty /bin/bash
                
              
Running applications from the desktop
-------------------------------------
  
There are a number of predefined applications which you can find under the ``ARC`` sub-menu, within the ``Applications`` section of the main menu bar, see below for examples:
  
  .. image:: images/arc-apps1.png
    :width: 800
    :alt: ARC Apps Menu
  
Applications|ARC Sub-menu 
  
  .. image:: images/arc-apps2.png
    :width: 350
    :alt: ARC Apps List

Clicking on these menu items will start up the appropriate version of the specified application, with any other required modules automatically loaded.

.. note::
   If you need customised versions of applications or supporting modules (such as custom Anaconda virtual environments) you should load/activate and run these as
   appropriate from the ``Konsole`` command window, in the same way as the ARC or HTC systems.
