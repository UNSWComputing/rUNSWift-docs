#############
3D Simulation
#############


********
Overview
********

Simulation allows for safe, quick testing of experimental code and settings,
and can help you practice using the code without having to leave your desk.


3D Simulation can be used for developing
    - Behaviours
    - Motion
    - Localisation
    - Support Tools

It cannot be used for developing
    - Vision


.. tip::
    Breaking simulated robots is a lot cheaper than breaking real ones!

********************
Installing Simulator
********************

Run ``$RUNSWIFT_CHECKOUT_DIR/bin/setup-simulation.sh``, in a terminal.


*********************
Running the Simulator
*********************

Running the simulator (RCSSServer3d)
====================================

To start the simulation server, in a new terminal, run ``rcssserver3d``

.. note::
    the following errors will show and **can be ignored**.

    ::

        (Light) ERROR: OpenGLServer not found
        (Light) ERROR: OpenGLServer not found
        (Material2DTexture) ERROR: cannot find TextureServer
        (Material2DTexture) ERROR: OpenGLServer not found.
        (Material2DTexture) ERROR: cannot find TextureServer
        (Material2DTexture) ERROR: OpenGLServer not found.
        (Material2DTexture) ERROR: cannot find TextureServer
        (Material2DTexture) ERROR: OpenGLServer not found.
        (Material2DTexture) ERROR: cannot find TextureServer
        (Material2DTexture) ERROR: OpenGLServer not found.
        (Material2DTexture) ERROR: cannot find TextureServer
        (Material2DTexture) ERROR: OpenGLServer not found.
        (Material2DTexture) ERROR: cannot find TextureServer
        (Material2DTexture) ERROR: OpenGLServer not found.
        (Material2DTexture) ERROR: cannot find TextureServer
        (Material2DTexture) ERROR: OpenGLServer not found.
        (Material2DTexture) ERROR: cannot find TextureServer
        (Material2DTexture) ERROR: OpenGLServer not found.
        (Material2DTexture) ERROR: cannot find TextureServer
        (Material2DTexture) ERROR: OpenGLServer not found.
        (Material2DTexture) ERROR: cannot find TextureServer
        (Material2DTexture) ERROR: OpenGLServer not found.
        (sparkgui.rb)  sparkRegisterMonitorCmdParser TrainerCommandParser
        (InputControl) ERROR: no FPSController found at '/usr/scene/camera/physics/controller'

Running the visualiser (RoboViz)
================================

To start the simulator visualier, in a new terminal run ``roboviz.sh``.
A window should pop up, with a soccer field.

Runing simswift (single robot)
==============================

#. Run ``nao_build-2.1.sh runswift`` in a new terminal to compile simswift. It is
   important to close the server and visualiser, to speed up the
   compilation. This step can be skipped if no re-compilation is
   required.
#. Launch robot by running ``simswift``.
   Runswift commandline arguments can be used, such as
   ``simswift -T 18 -n 1``.
#. To kill the robot, use Ctrl+C.


Running simswift (team)
=======================

#. ``nao_build-2.1.sh runswift`` to compile. Skip this step if you don't have to
   re-build.
#. ``sim_run`` to launch a whole team. This starts five robot agents.
#. ``sim_kill``, to terminate all agents.


Running with Offnao
===================

#. Run ``simswift`` in a new terminal. In the terminal, look for the following message and take note of the port number
   ``rUNSWift running in SIMULATION mode. DO NOT RUN THIS ON A NAO.    Listening for Offnao on port 10241.``
#. Run ``offnao``, and go ``File -> Connect To Nao (Ctrl+N)``. Enter
   ``127.0.0.1`` in first textbox, and the port number in the second
   textbox.
#. Click on the first textbox, and press ``Enter``.
#. Click on the red circle button at the bottom left of the offnao
   window to start recording.

.. tip::
    The port number is calculated from the team number and player number of the agent.

Speeding up the server
======================

#. Run ``export SPARK_FAST_TIME=true`` in a new terminal.
#. In the same terminal, run ``rcssserver3d``.
   This lets the server run as fast as your CPU can handle.

.. tip::
    Run ``export SPARK_FAST_TIME=false`` to disable the speed-up.


********************
How It Works
********************

3D Simulation consists of
    - `rcssserver3d`_
    - `simswift`_
    - `RoboViz`_

.. figure:: /images/Simulator_Structure.png


rcssserver3d
============

3D soccer simulation server running on top of simspark
simulation system. Developed by the RoboCup 3D Simulation League.
rUNSWift modifications are made in `rUNSWift's fork <https://gitlab.com/ijnek/SimSpark>`__.
More information can be found at `Simspark Wiki <https://gitlab.com/robocup-sim/SimSpark/wikis/home>`__.

simswift
========

simswift is the rUNSWift build target on a Linux PC, and is the agent that connects to the simulation server.
Refer to `Collette's (2017)
thesis <https://github.com/UNSWComputing/rUNSWift-2017-release/blob/master/docs/Collette-Using_3D_Simulation_to_Develop_Robot_Code/Collette-Using_3D_Simulation_to_Develop_Robot_Code.pdf>`_
for more info.

RoboViz
=======

User-friendly visualiser for the simulator.
Provides a graphical interface to interact with the simulator, such as moving the ball and robots.
rUNSWift modifications are made in `rUNSWift's fork <https://github.com/ijnek/RoboViz>`__.
More information can be found at `magmaOffenburg/RoboViz GitHub <https://github.com/magmaOffenburg/RoboViz>`__.


**************
Making changes
**************

Recompiling changes
===================

SimSpark
--------

* To re-compile Spark, run ``spark_build`` from anywhere.
* To re-compile rcssserver3d, run ``rcs_build`` from anywhere.

.. note::
    ``spark_build``, ``rcs_build`` are located in ``simspark/bin/``

Pushing changes
===============

Making changes to SimSpark / RCSS
---------------------------------

#. Gain push access to `rUNSWift's Simspark Fork <https://github.com/UNSWComputing/SimSpark>`_
#. Create pull request with a branch with changes.

Making changes to Roboviz
-------------------------

#. Gain push access to `rUNSWift's RoboViz Fork <https://github.com/UNSWComputing/RoboViz>`_
#. Create pull request with a branch with changes.

.. note::
    For GitHub push access, please :ref:`contact` us.


**********************
rUNSWift Modifications
**********************

This is a list of what rUNSWift has modified in the SimSpark and
RoboViz. This list should be kept up to date so we know what to preserve
when incorporating changes made in the original open-source projects.

SimSpark / RCSS Modifications
=============================

100FPS
------

-  To match the speed of the motion of the SoftBank NAO V5, the
   simulator's FPS was changed from 50FPS to 100FPS.

SPARK_FAST_TIME
---------------

-  This is an environment variable that was added to affect multiple
   settings to allow speed-ups in the simulator

rcssserver3d/bin
----------------

-  ``rcs_build`` and ``spark_build`` scripts were added in
   ``rcssserver3d/bin`` for easy compiling of the simulator.

Disabling Autoref
-----------------

-  Autoreffing has been disabled, as it is not needed.

FieldFeatures
-------------

-  A significant modification rUNSWift has made to rcssserver3d, is the
   addition of "FieldFeatures" (corners, t-junctions, centre circles,
   etc).
-  This is a modification to allow the "orientation" of a fieldfeature
   to be recognised (such as a corner) by the agent in the simulator
-  To view the list of fieldfeatures refer to
   ``simspark/rcssserver3d/data/rsg/agent/nao/soccer.rsg``

RoboViz Modification List
=========================

Goal and Penalty Box Size
-------------------------

-  Goal and Penalty Box Size were modified to meet SPL requirements

************
Known issues
************

* rcssserver3d will sometimes crash, and keep running in the
  background. This can happen especially if you disconnect/connect
  agents very quickly. When this happens, run the following command:
  ``pkill -9 rcssserver3d; rcssserver3d``
* Some movements such as the getup have not been tuned in the
  simulator.
