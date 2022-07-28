
Using the ARC Graphical Interactive Nodes
-----------------------------------------


ARC have a number of graphical interactive nodes which you can use to interact with applications which require GUI operation, such as RStudio, Jupyter Notebooks
and ANSYS Workbench.

In order to use these interactive nodes, you must be connected to the university network or be connected via the university VPN service. 

**Accessing the Graphical Interactive nodes**

You can connect directly via web browser to `nx.arc.ox.ac.uk <https://nx.arc.ox.ac.uk>`_ via the web-based client connection (which is lower quality in terms of
visual display). See `Configuring NoMachine Web Client <https://arc-user-guide.readthedocs.io/en/latest/arc-nx-web.html>`_

Alternatively you can download the `NoMachine Enterprise Client <https://www.nomachine.com/download-enterprise#NoMachine-Enterprise-Client>`_ and install this on your
local machine. See `Configuring NoMachine Client <https://arc-user-guide.readthedocs.io/en/latest/arc-nx-client.html>`_

.. note::
  While it may look like you have your own Linux desktop to work with, the interactive nodes where you are running this desktop are shared with other ARC users, and   
  therefore it is very important that you not run computationally demanding jobs. 
  
  To run jobs that are more demanding than simple GUI application usage, please open a     Konsole window and start an interactive X11 session on an interactive compute   node using::
     
       srun -p interactive --x11 --pty /bin/bash
  
  
