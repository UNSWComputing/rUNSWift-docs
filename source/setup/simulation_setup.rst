###################
3D Simulation Setup
###################

*****
Setup
*****

.. note::
    You will have to be inside the UNSW CSE firewall for the following
    script to work. We should find a way to make it accessible from
    anywhere.

Run ``$RUNSWIFT_CHECKOUT_DIR/bin/sim_setup.sh``, in a terminal.

**********************
Running the Simulation
**********************

Running the simulator (RCSSServer3d)
====================================

To start the simulation server, in a new terminal, run ``rcssserver3d``
Note: the following errors will show and **can be ignored**.

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

1. Run ``sim_build`` in a new terminal to compile simswift. It is
   important to close the server and visualiser, to speed up the
   compilation. This step can be skipped if no re-compilation is
   required.
2. Launch robot by running ``simswift``.
   Runswift commandline arguments can be used, such as
   ``simswift -T 18 -n 1``.
3. To kill the robot, use Ctrl+C.


Running simswift (team)
=======================

1. ``sim_build`` to compile. Skip this step if you don't have to
   re-build.
2. ``sim_run`` to launch a whole team. This starts five robot agents.
3. ``sim_kill``, to terminate all agents.


Running with Offnao
===================

1. Run ``simswift`` in a new terminal. In the terminal, look for the
   following message and take note of the port number
   ``rUNSWift running in SIMULATION mode. DO NOT RUN THIS ON A NAO.    Listening for Offnao on port 10241.``
   (NOTE: The port number is calculated from the team number and player
   number of the agent.)
2. Run ``offnao``, and go ``File -> Connect To Nao (Ctrl+N)``. Enter
   ``127.0.0.1`` in first textbox, and the port number in the second
   textbox.
3. Click on the first textbox, and press ``Enter``.
4. Click on the red circle button at the bottom left of the offnao
   window to start recording.

Speeding up the server
======================

1. Run ``export SPARK_FAST_TIME=true`` in a new terminal.
2. In the same terminal, run ``rcssserver3d``.
   This lets the server run as fast as your CPU can handle.
   (NOTE: Run ``export SPARK_FAST_TIME=false`` to disable the
   speed-up.)
