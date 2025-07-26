################
Running the code
################

You have two options, either run using systemd or run in an ssh terminal. 
By default, all systemd services except foxglove will start on boot to be game ready.

.. note::
    This is different to *legacy* TODO add link

*************
Using systemd
*************

#. Open an ssh connection to the robot by running

    .. code-block:: bash

        ssh nao@<robot>

    .. tip::
        ``nao`` is the user name, and ``<robot>`` is the hostname of the robot.

    .. note::
        For passwords, please :ref:`contact` us.

#. **On the robot** (in the terminal with the ssh connection)

    To start a service

    .. code-block:: bash

        sudo systemctl start <service>

    To stop a service

    .. code-block:: bash

        sudo systemctl stop <service>
    
    .. note::
        The list of services are:

        - runswift_motion
        - runswift_vision
        - runswift_stateestimation
        - runswift_comms
        - runswift_behaviours
        - runswift_hri
        - runswift_startup
        - runswift_errors
        - foxglove

#. Once the chest light is flashing green
   **press the chest** or hold the 3 head sensors for one second to stiffen the robot


.. seealso::
    :ref:`button_presses` for ways to interact with the robot without a PC.

~~~~~~~
Example
~~~~~~~

Often we want to use foxglove to use various tools. This particular example is 
the process we use for kinematics calibration. First ssh in, then use:

.. code-block:: bash

    sudo systemctl stop runswift_behaviours
    sudo systemctl start foxglove

Then, you can connect to the robot using the foxglove web app at `http://<robot>:8765`


****************
Using a terminal
****************

This method is useful for debugging since you can see the output of the code in the terminal.

#. Open an ssh connection to the robot by running

    .. code-block:: bash

        ssh nao@<robot>

    .. tip::
        ``nao`` is the user name, and ``<robot>`` is the hostname of the robot.

    .. note::
        For passwords, please :ref:`contact` us.

#. **On the robot** (in the terminal with the ssh connection)

    * Since systemd starts services by default, we need to stop them

    .. code-block:: bash

        sudo systemctl stop runswift_motion
        sudo systemctl stop runswift_vision
        sudo systemctl stop runswift_stateestimation
        sudo systemctl stop runswift_comms
        sudo systemctl stop runswift_behaviours
        sudo systemctl stop runswift_hri
        sudo systemctl stop runswift_startup
        sudo systemctl stop runswift_errors

~~~~~~~
Example
~~~~~~~

First, run the code block above to kill all services. Then ssh in and run:

.. code-block:: bash

    source robot_ws/install/setup.bash
    ros2 launch motion_port motion_launch

TODO check that's correct ^