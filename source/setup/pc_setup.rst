.. _pc_setup:

########
PC Setup
########

.. note::
    If this is your first time using rUNSWift software, follow the instructions on this page.
    For those that are looking to contribute to the codebase, please follow instructions on :ref:`pc-setup-contributing`.

******************
Install VirtualBox
******************

Download and Install `VirtualBox <https://www.virtualbox.org/wiki/Downloads>`_.

************************
Import rUNSWift VM Image
************************

#. Download OVA file from `http://robocup.web.cse.unsw.edu.au/runswift2/rUNSWift-VM.ova`
#. File -> Import Appliance
#. Select the Downloaded OVA file
#. Next
#. Import
#. Start

.. tip::
    OVA file is very big (>5GB), and you have to be on campus or a CSE student to download it.

.. tip::
    We have a smaller (3.2GB) OVA file for external users at `http://robocup.web.cse.unsw.edu.au/runswift2-htpasswd/rUNSWeenie.ova`.

.. note::
    For passwords, please :ref:`contact` us.


.. _setup_network:

******************************
Setup Wireless/Wired Network
******************************

.. warning::
    You only have to follow these steps if you have to connect to an actual robot.


For a VM, it is necessary to bridge wireless networks and wired networks (when using LAN)
from the host machine to the VM. Follow these instructions in VirtualBox.

#. Network
    #. Adapter 2
        #. Enable Network Adapter
        #. Attached to Bridged Adapter
        #. Name should be your wired adapter
        
******************
Using Hyper-V instead of Virtual Box
******************
If you using windows OS and already running hyper-v system, virtual box will not be able to start the VM. 
These instruction is converting the VM from virtual box to hyper-v.
Converting directly via microsoft converted wont work, some VM description is not supported, hence need to extract the VM description info, edit and override it before convert to hyper-v. Steps are below.

************************
Step by steps
************************

#. Download OVA file from `http://robocup.web.cse.unsw.edu.au/runswift2/rUNSWift-VM.ova`
#. Download Microsoft Virtual Machine Converter 3.0 `https://www.microsoft.com/en-gb/download/details.aspx?id=42497`
#. Download dsfok `https://www.mysysadmintips.com/-downloads-/Windows/Servers/dsfok.zip`
#. Create folder C:\AMConvertingrUNSWiftVM for converting and storage of VM, recommended to have at least 30gb space on this drive. Create empty folder 'VM' under it, C:\AMConvertingrUNSWiftVM\VM
#. Unzip OVA file to extract rUNSWift-VM-disk001.vmdk file to C:\AMConvertingrUNSWiftVM\
#. unzip dsfok.zip and run a cmd from that folder.
#. run `.\dsfo.exe C:\AMConvertingrUNSWiftVM\rUNSWift-VM-disk001.vmdk 512 1024 C:\AMConvertingrUNSWiftVM\Descriptor.txt`
#. Edit the Descriptor.txt comment out ddb.uuid.* and ddb.comment. example:
`
...

#ddb.uuid.image="da0f0b53-5c68-4d2d-a357-7db834223cca"
#ddb.uuid.parent="00000000-0000-0000-0000-000000000000"
#ddb.uuid.modification="00000000-0000-0000-0000-000000000000"
#ddb.uuid.parentmodification="00000000-0000-0000-0000-000000000000"
#ddb.comment=""
`
#. NOTE DSFI.exe not DSFO.exe, run `.\dsfi.exe C:\AMConvertingrUNSWiftVM\rUNSWift-VM-disk001.vmdk 512 1024 C:\AMConvertingrUNSWiftVM\Descriptor.txt`
#. Now the vmdk is ready to be converted to hyper-v. Run powershell `Import-Module "C:\Program Files\Microsoft Virtual Machine Converter\MvmcCmdlet.psd1"`
#. Run powershell `ConvertTo-MvmcVirtualHardDisk -SourceLiteralPath C:\AMConvertingrUNSWiftVM\rUNSWift-VM-disk001.vmdk -DestinationLiteralPath C:\AMConvertingrUNSWiftVM\VM -VhdType DynamicHardDisk -VhdFormat Vhd`
#. Now you can create new hyper-v VM, with settings: Generation 1, Dynamic Memory, HD use existing HD in C:\AMConvertingrUNSWiftVM\VM
#. Done, you can start the VM it should load the ubuntu screen.
#. Any questions, pm Andrew Million in slack group.
