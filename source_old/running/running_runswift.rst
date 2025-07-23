################
Running runswift
################

#. Open an ssh connection to the robot by running

    .. code-block:: bash

        $ ssh nao@mario

    .. note::
        Replace mario with the name of the robot’s head you’re using

    .. tip::
        ``nao`` is the user name, and ``mario`` is the hostname of the robot.

    .. note::
        For passwords, please :ref:`contact` us.

#. **On the robot** (in the terminal with the ssh connection), run

    .. code-block:: bash

        $ runswift

#. Once the chest light is flashing green
   **double press the chest** to stiffen the robot.


.. seealso::
    :ref:`button_presses` for ways to interact with the robot without a PC.

*******
Options
*******

Commonly used options are below:

========================================= ======= ==================================================================================
Option                                    Default Description
========================================= ======= ==================================================================================
-T                                        18      Team Number (eg. 18)
----------------------------------------- ------- ----------------------------------------------------------------------------------
-n                                        2       Player Number (eg. 2)
----------------------------------------- ------- ----------------------------------------------------------------------------------
-s                                        Game    Name of top level body python behaviour skill to execute
----------------------------------------- ------- ----------------------------------------------------------------------------------
--stateestimation.initial_pose_type       GAME    Type of initial pose (GAME/UNPENALISED/SPECIFIED)
----------------------------------------- ------- ----------------------------------------------------------------------------------
--stateestimation.specified_initial_x     0       Initial x value in mm (if stateestimation.initial_pose_type == SPECIFIED)
----------------------------------------- ------- ----------------------------------------------------------------------------------
--stateestimation.specified_initial_y     0       Initial y value in mm (if stateestimation.initial_pose_type == SPECIFIED)
----------------------------------------- ------- ----------------------------------------------------------------------------------
--stateestimation.specified_initial_theta 0       Initial theta value in degrees (if stateestimation.initial_pose_type == SPECIFIED)
========================================= ======= ==================================================================================

.. seealso::

    ``runswift --help`` for complete list of options

*******
Example
*******

To run a robot with

*   FieldPlayer skill
*   Starting from the centre of the field, facing opponent goal

.. code-block:: bash

    $ runswift -s FieldPlayer --stateestimation.initial_pose_type SPECIFIED


.. tip::
    Modify the options in ``runswift.cfg`` to make it easier if you have a lot of options!
