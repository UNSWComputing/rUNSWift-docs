#######################
VirtualBox Instructions
#######################

#. Download `Ubuntu Desktop Image <http://releases.ubuntu.com/22.04/>`_.
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

    #. Continue
    #. Restart Now (after installation is complete)

Refer to :ref:`setup_network` for bridging the networks between host machine and VM.
