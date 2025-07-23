#################
VM Image Creation
#################

These are instructions on creating an OVA file to be used in :ref:`pc_setup` for new team members.

#. Download `Ubuntu Desktop Image <http://releases.ubuntu.com/22.04/>`_.

   .. tip:: For a smaller VM, try Alpine Linux, Tiny Core Linux, or Slax 9.  (Only Slax 9 has been tested.)
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
           Memory size of 2GB is a minimum.
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
                Maximum 1 CPU per 1.5GB Base Memory
                Recommendation is equal to the number of cores on your system.  Ignore the 'Invalid settings detected'.
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

        .. tip:: Do not use the standard runswift password

    #. Continue
    #. Restart Now (after installation is complete)

#.  Inside the VM, in a terminal,

    .. code-block:: bash

        ZID=your_zid
        mkdir -p ~/.ssh
        cd ~/.ssh
        wget --user=$ZID --ask-password https://www.cse.unsw.edu.au/~robocup/Nao/Downloads/vm-files/.ssh/id_rsa https://www.cse.unsw.edu.au/~robocup/Nao/Downloads/vm-files/.ssh/config
        ssh-keygen -p -N '' -f ~/.ssh/id_rsa
        # Enter old passphrase: the standard runswift password
        sudo apt install git
        cd ~
        git clone git@github.com:UNSWComputing/rUNSWift.git rUNSWift
        rUNSWift/bin/setup-build.sh
        rUNSWift/bin/setup-simulation.sh
        rm -rf ~/.ssh/id_rsa

    .. note::
        For passwords, please :ref:`contact` us.
    .. note::
        Consider squashing history
    .. tip::
        Reduce the VM size by commenting out ctc-2.8, flite, and game controller from source.sh/setup-build.sh if you don't need them

#. Shutdown the VM
#. Machine -> Export to OCI
    #. Uncheck "Write Manifest File"
    #. Next
    #. Export
#.  Upload ova file to server

    .. code-block:: bash

        rsync -aP ~/Documents/runswift-18.04.ova runswift@runswift2.cse.unsw.edu.au:/var/www/html/
