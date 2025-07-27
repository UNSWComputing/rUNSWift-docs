######
Motion
######

********
Overview
********

The motion module should be run in its own thread with the highest priority on the robot,
as joint angles need to be calculated at approximately 82 frames per second to maintain stability.
We haven't quite figured out if that's happening yet in ROS2.
The MotionAdapter node controls the motion and handles the motion processing. In
legacy, there were 3 areas, but now touch and effector are handled but the nao_lola package.
Now, it essentially takes in a MotionCommand, wraps it with SafetySkill (for handling ref
pickups and getups when falling), and runs it through the generators.

**********
Literature
**********

**The most relevant report to motion currently is** `rUNSWift Walk2014
Report <http://cgi.cse.unsw.edu.au/~robocup/2014ChampionTeamPaperReports/20140930-Bernhard.Hengst-Walk2014Report.pdf>`__
(Hengst, 2014)

Other reports that include motion concepts to varying degrees:

*   `Learning to Control a Biped with
    Feet <http://cgi.cse.unsw.edu.au/~robocup/2014ChampionTeamPaperReports/20141113-HengstLangeWhite-Humanoids2011Paper31.pdf>`__
    (Hengst, Lange, White, 2011)

*   `Humanoid Omni-directional Locomotion
    <http://cgi.cse.unsw.edu.au/~robocup/2014ChampionTeamPaperReports/20111010-Brock.White-OmniDirectionalLocomotion.pdf>`__
    (White, 2011)

*   `Dynamic Omnidirectional Kicks on Humanoid Robots
    <http://cgi.cse.unsw.edu.au/~robocup/2014ChampionTeamPaperReports/20120824-Belinda.Teh-OmniDirectionalKicks.pdf>`__
    (Teh, 2012)

*   `Reinforcement Learning of Bipedal Lateral Behaviour and Stability Control with Ankle-Roll Activation
    <http://cgi.cse.unsw.edu.au/~robocup/2014ChampionTeamPaperReports/20130000-Bernhard.Hengst-RLLateralStability-CLAWAR13.pdf>`__
    (Hengst, 2013)

*   `Bipedal walk and goalie behaviour in Robocup SPL
    <http://cgi.cse.unsw.edu.au/~robocup/2014ChampionTeamPaperReports/20130108-Roger.Liu-WalkAndGoalie.pdf>`__
    (Liu, 2013)

*   `rUNSWift Robocup SPL 2013 Special Project A Report
    <http://cgi.cse.unsw.edu.au/~robocup/2014ChampionTeamPaperReports/20130817-Dan.Padiha-WalkStabilisation-Behaviours-DropIn.pdf>`__
    (Padilha, 2013)


*******
Actions
*******

.. note::
    These are not ROS2 actions, these are physical actions performed by the robot

Most of the work in producing actions happens in the generator area. The
main generator class is the DistributedGenerator that calls upon
subsequent generators depending on the requested action. There are also
some basic generators that all generated joints get passed through, such
as the ClippedGenerator, which ensures that joint requests do not go
past their maximum values.

All actions are defined in MotionCommand [TODO link?]. If you do add
a new ActionType to it, remember to fill out all the corresponding
maps in DistributedGenerator, if it needs a special priority or head movement. 
These priorities define what actions can be interrupted, for example the get up 
action has the highest priority.

To set a generator for a particular body action, you'll need to add
something like this to DistributedGenerator:

.. code:: c

    bodyGenerators[Body::BACK_FLIP] = (Generator*)(new BackFlipGenerator());
       if (!bodyGenerators[Body::BACK_FLIP])
          RCLCPP_FATAL(motion_node_->get_logger(), "bodyGenerators[BACK_FLIP] is NULL!");

All generators should subclass the basic Generator.hpp class and fill in
the virtual functions, such as isActive, reset, and stop. Along with the
ActionCommand priorities, these functions help DistributedGenerator
decide how and when to transition between different actions.

Static Actions
==============

Static actions are typically used for straightforward motions such as
standing, squatting, diving and getups. These are handled by the ``ActionGenerator``. To
specify which action should be performed, the ActionGenerator is passed
the file name of the relevant .pos file.

.pos Files
----------

**The format for pos files are described in** ``$RUNSWIFT_CHECKOUR_DIR/image/home/nao/data/pos/README.md``.

They typically look like this, for eg. ``stand.pos``:

::

      HY    HP    LSP   LSR   LEY   LER   LWY   LHYP  LHR   LHP   LKP   LAP   LAR   RHR   RHP   RKP   RAP   RAR   RSP   RSR   REY   RER   RWY   LH    RH    DUR
    $ 0     0     0     0     0     0     0     0.75  0.75  0.75  0.75  0.75  0.75  0.75  0.75  0.75  0.75  0.75  0     0     0     0     0     0     0
    ! 0     0     90    10    0     0     0     0     0     -25   50    -25   0     0     -25   50    -25   0     90    -10   0     0     0     0     0     1000


.. figure:: http://doc.aldebaran.com/2-8/_images/naov6_motors.png

All pos files can be found in ``$RUNSWIFT_CHECKOUT_DIR/image/home/nao/data/pos``.

Dynamic Actions
===============

Dynamic actions are for more complicated movements, such as the walk and
kicks. Instead of reading the joint values from a pos file, they are set
in the relevant generator's ``makeJoints`` function.

**********
Kinematics
**********

Forward Kinematics
==================

These can be found in perception (just a legacy location as it was
originally only used for vision).

`Modified DH parameters
<https://en.wikipedia.org/wiki/Denavit%E2%80%93Hartenberg_parameters#Modified_DH_parameters>`_
are used to calculate the forward kinematics chain. See
`Walk2014 Report <http://cgi.cse.unsw.edu.au/~robocup/2014ChampionTeamPaperReports/20140930-Bernhard.Hengst-Walk2014Report.pdf>`_
for the Camera to Foot transform used in the Nao v4 (most of which is
similar in the Nao v5 and v6) These are used for calculating the robot pose and
converting camera image space co-ordinates to robot relative
co-ordinates.

The DH parameters for each of Nao v4 limbs can be found in
`Bel Teh's thesis <http://cgi.cse.unsw.edu.au/~robocup/2012site/reports/Belinda_Teh_Thesis.pdf>`_
(see Tables 3.1-3.3). These are used for calculating the centre of mass.

Note that body lean (as detected from IMU) is also applied when
converting into world space as the robot's foot is not always flat on
the ground.

Inverse Kinematics
==================

Both Kinematic Transforms and Iterative Inverse Kinematics for turning
the feet can be found at the very bottom of Walk2014.cpp. They were
copied from the symbolic Matlab solution and of the kinematic chain and
iterative inverse method. Reference to the original work can be found in
the `2010 rUNSWift Team Report <http://cgi.cse.unsw.edu.au/%7Erobocup/2010site/reports/report2010.pdf>`_
in Chapter 6.


******************
Walk2014 Generator
******************

Walk2014 addresses shortcomings in the walk first developed in 2010,

*   Stability - addressed by a new Stabiliser using a reinforcement
    learnt policy and the Centre-of-Mass moved towards centre of foot.
*   Slow side-stepping - addressed with a new sidestepping generator that
    can take larger sidesteps.
*   Robots overheat - addressed by using a stand command with low stiffness.
*   Transition between stand, walks,
    kicks, and getup is not smooth - addressed by integrating these
    behaviour into the walk.
*   Acceleration and braking uses an inefficient
    ratcheting technique - addressed by ability to start and stop in one
    step. Forward is still limited to changes of e.g. 50mm / step, (built
    into walk).
*   Limited repertoire of kicks - addressed by new kicks,
    e.g. stab-kick, walk-kick, etc.

Walk2014 is more responsive than previous rUNSWift walks. Python roles
and skills have more control (and hence responsibility) for parameter
settings:

#.  The forward, left and turn body action commands define the step-size (mm / rad)
    per second.
#.  The user will need to ensure that the combination of
    forward/left/turn stays within the capability of the walk. However,
    the values have been clipped to +/- 300mm for forward, +/-200mm for
    left, and +/- 2.0 radian for turn. Please note that the above ranges
    for forward, left, turn are with only one parameter set, the others
    are zero). In combination these ranges will need to be reduced, but
    combinations have not all been tested.

    Combination of parameter values are evaluated using an ellipsoid clamp,
    and transitions are dealt by clamping the maximum change of forward, left and turn.


Two Different Stand Postures
============================

With ``actioncommand.stand(power=stiffness)`` the walk performs a stand
routine and turns the stiffness to the motors using power. The power
parameter is optional and defaults to 0.1.

``actioncommand.crouch(power=stiffness)``, the walk stops rocking, but is
READY for action i.e. legs are kept bent. Stiffness is kep to 0.4
minimum to ensure the robot retains this stance. The power parameter is
optional and defaults to 0.4.

However, there are some cases where the robot needs to stand but walk
shouldn't be running, for example when the robot first boots up or
during ref pick up. We then use two pos files (initial.pos and
stand.pos) that map to these two different stand postures.

Calibration
===========

The walk has been calibrated so that forward, left and turn will move
the real robot approximately the specified distance/angle in one second
in steady state operation. The odometry is calibrated based on foot
movements and should be more accurate than average parameter values. For
example, when changing speed, the odometry will record the movements at
82Hz and not use the parameter values. In the ``Walk2014Generator``,

.. code:: c

    // linear calibration to achieve actual performance ie turn in action command achieves turn/sec in radians on the robot
    forward *= 1.0;
    left *= 0.82;
    turn *= 0.78;

Kicks
=====

The standard kick is also integrated into Walk2014Generator to make
transitioning between the two as smooth as possible. It uses many of the
same parameters and calculations.

The motion of the kick is defined in several phases:

#. The back phase moves the foot backwards in preparation for the kick
   swing. It also moves the foot sideways depending on the position of
   the ball. This dynamic left movement helps reduce time spent lining
   up. The power parameter is used at this stage to affect how far back
   the kick foot should go back.

#. The kick swing phase swings the foot forward into the ball. The power
   parameter is used at this stage to affect how far forwards the kick
   foot travels forwards.

#. The follow through phase holds and stabilises at the end of the kick
   swing.

#. The end phase returns the foot back to the zero position.

*****************
Walk Preprocessor
*****************

Since the behaviour module runs at 30fps in a separate thread and does
not have access to the state of the walk cycle found in walk generator,
it has no precise way to tell when a step begins and when it ends.
That's why walk parameters are given as step size per second. However,
this makes certain higher level behaviours difficult when precision of
steps is required, such as lining up to the ball before kicking it.

The walk preprocessor is a wrapper around the walk generator and has
access to the state of the walk cycle. It breaks down a single higher
level behaviour request into multiple walk parameters for the walk
generator. Thus avoiding the need for synchronisation between the
behaviour and motion thread, and ensures precision of steps.

This was used to perform a motion line up and turn dribble, but both are
outdated and unused.
