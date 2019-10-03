#################
VM Image Creation
#################

These are instructions on creating an OVA file to be used in :ref:`pc_setup` for new team members.

#. Download `Ubuntu Desktop Image <http://releases.ubuntu.com/18.04/>`_.
#. Download and Install `VirtualBox <https://www.virtualbox.org/wiki/Downloads>`_.
#. New
    #.  ======= ===============
        Name    rUNSWift-VM
        ------- ---------------
        Type    Linux
        ------- ---------------
        Version Ubuntu (64-bit)
        ======= ===============
    #. Next
    #. =========== ======
       Memory Size 4096MB
       =========== ======

        .. tip::
            Memory size of 4GB is a minimum.
            You also want to leave at least 4GB for your host machine.
            Recommendation is half your system memory.
    #. Next
    #. Create a Virtual Hard Disk now
    #. Create
    #. Expert Mode
    #. ============================= =====================
       File Size                     50GB
       ----------------------------- ---------------------
       Hard disk file Type           VDI
       ----------------------------- ---------------------
       Storage on physical hard disk Dynamically allocated
       ============================= =====================
#. Settings
    #. System
        * Processor
            ============ ======
            Processor(s) 4 CPUs
            ============ ======

            .. tip::
                The number of processors should be equal to the number of cores on your system.
                Ignore the 'Invalid settings detected'.
    #. Storage
        #. Click on *Empty* under *Controller:IDE*.
        #. *Attributess* -> *Optical Drive* -> click on the disc icon
        #. Choose Virtual Optical Disk File
        #. Select downloaded iso file
#. Start
    #. English
    #. Install Ubuntu
    #. Continue (US Keyboard)
    #. Continue (Minimal Installation and Download Updates)
    #. Install Now (Erase disk)
    #. Continue (write changes to disk?)
    #. Continue (Sydney)
    #.  ========= =============
        Your name (your choice)
        --------- -------------
        username  (your choice)
        --------- -------------
        password  (your choice)
        ========= =============

    #. Continue
    #. Restart Now (after installation is complete)

#.  Inside the VM, download

    * `.ssh/config <https://www.cse.unsw.edu.au/~robocup/Nao/Downloads/vm-files/.ssh/config>`_
    * `.ssh/id_rsa <https://www.cse.unsw.edu.au/~robocup/Nao/Downloads/vm-files/.ssh/id_rsa>`_

    from CSE into ``~/.ssh/``.

    In a terminal,

    .. code-block:: bash

        ssh-keygen -p -N '' -f ~/.ssh/id_rsa
        # Enter old passphrase: the standard runswift password
        sudo apt install git
        git clone git@github.com:UNSWComputing/rUNSWift.git rUNSWift
        rUNSWift/bin/build_setup.sh
        rUNSWift/bin/sim_setup.sh

    .. note::
        For passwords, please :ref:`contact` us.

#. Shutdown the VM
#. Machine -> Export to OCI
    #. Uncheck "Write Manifest File"
    #. Next
    #. Export
#.  Upload ova file to server

    .. code-block:: bash

        rsync -aP ~/Documents/runswift-18.04.ova runswift@runswift2.cse.unsw.edu.au:/var/www/html/
