##########
Kinematics
##########

Kinematic transforms must be performed on the robots to reduce/prevent systematic errors caused by physical inaccuracies of a nao’s physical build.
This is critical for vision when determining the distance and heading to objects.
The offsets in the angle of the camera mount are determined in this camera/joint offset calibration.

Offset variables (measured in degrees) exist for both the top and bottom cameras as they must be considered separately.
These variables exist for the yaw, pitch, and roll of the cameras.

The procedure of camera/joint calibration involves comparing projected field lines to actual field lines seen in the image to adjust offsets.
These offsets are used in the determination of the kinematic chain (i.e. determining the D-H Parameters).
This kinematic chain is then sent to offnao with the inverse taken to project a map of the field onto the image, offsets then accounted for with the process repeating until the projections match the image.

************
Instructions
************

In this example, we will use a robot with the head of mario and body of yoshi.

========= =========
Head name Body name
========= =========
mario     yoshi
========= =========

#.  Ensure ``bodyName`` is correct in ``image/home/nao/data/configs/mario.cfg``

    .. code-block:: cfg

        [player]
        bodyName=yoshi

    .. note::
        Replace ``mario`` and ``yoshi`` with your robot's head and body names

#.  Run ``runswift`` on the NAO
#.  Run ``offnao`` on PC
#.  Follow instructions on cameraPoseTab
#.  Stop offnao recording
#.  Copy the tuned **bodyPitch** config into ``image/home/nao/data/configs/body/yoshi.cfg``

    .. code-block:: cfg

        [kinematics]
        bodyPitch=3.5

    .. note::
        Replace ``yoshi`` with your robot's body name

#.  Copy the tuned **camera** kinematics configs into ``image/home/nao/data/configs/mario.cfg``

    .. code-block:: cfg

        [kinematics]
        cameraYawBottom=0
        cameraPitchBottom=3.2
        cameraRollBottom=0.75
        cameraYawTop=0
        cameraPitchTop=0.4
        cameraRollTop=-0.85

    .. note::
        Replace ``mario`` with your robot's head name


.. warning::
    Offnao crashes when RAM fills up, so regularly save the config values.
