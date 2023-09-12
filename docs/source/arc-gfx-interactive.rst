Using the ARC desktop environment
=================================

ARC have a number of graphical interactive nodes which you can use to interact with applications which require GUI operation (such as RStudio, Jupyter Notebooks and ANSYS Workbench).

In order to use these interactive nodes, you must be connected to the university network or be remotely connected via the university VPN service. See  `Connecting to ARC <https://arc-user-guide.readthedocs.io/en/latest/connecting-to-arc.html>`_ for details how to connect to the graphical nodes.

Once you have connected to the NoMachine service by one of the described methods, you will be presented with the ARC desktop environment as shown below:

.. image:: images/arc-desktop.png
  :width: 800
  :alt: ARC Desktop
  
You can use the menu bar at the bottom of the window to access applications or, as in the example below, open the ``Konsole`` terminal window:

.. image:: images/arc-konsole.png
  :width: 800
  :alt: ARC Konsole
  
.. note::
  While it may look like you have your own Linux desktop to work with, the interactive nodes where you are running this desktop are 
  shpared with other ARC users, and therefore it is very important that you do not run computationally demanding jobs. 
  
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
