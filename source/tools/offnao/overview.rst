########
Overview
########

.. figure:: /draw.io/overview_tab.png


#. :ref:`field_view`
#. :ref:`cc_top_image`
#. :ref:`cc_bot_image`
#. :ref:`bb_variables`

.. _field_view:

**********
Field View
**********

Field View shows many things that our robot knows about the world and shows behaviour intentions.

.. _robot_pose:

Robot Pose
##########

Robot Pose and Covariance is displayed using a pacman-like symbol.

.. figure:: /images/pose.png

**θ** indicates one standard deviation of the robot's heading both in clockwise and anticlockwise direction.

The covariance ellipse indicates how accurately the position of the robot is known.
If a covariance ellipse is close to a circle, the robot is unaware of its position equally in all directions, but if
the covariance ellipse is stretched along one of it's axes, the robot knows its position well along the short axis, but not along the long axis.

.. tip::
    If the pacman's mouth is wide open, it is highly unsure of its heading.

.. tip::
    Covariance ellipses are used commonly in robot kalman filters, so search google to learn more.

My Pose
*******

My pose is the pose hypothesis used in behaviours, and can be identified by a :ref:`robot_pose` symbol with a **white ellipse**.

.. figure:: /images/my_pose.png

My Pose Hypotheses
******************

All the robot pose hypotheses are **yellow**, and use the :ref:`robot_pose` symbol.
The **brush thickness** of the covariance ellipse is the **weight of hypothesis**.

.. figure:: /images/hypotheses.png

The left and right hypotheses in the image have 1.0 and 0.03 weight respectively.
The right hypotheses has an extremely small brush thickness that ends up almost invisible.


.. _teammate_pose:

Teammate Pose
*************

Teammate's pose is shown in its corresponding :ref:`color`, and uses the :ref:`robot_pose` symbol.

.. _ball:

Ball Position and Velocity
##########################

======= ===========================
Element Description
======= ===========================
Dot     Ball Position
------- ---------------------------
Ellipse Position Covariance Ellipse
------- ---------------------------
Line    Ball Velocity
======= ===========================

The direction of the line from the ball, is the direction it is moving.

.. tip::

    The length of the line is how far the ball would travel over **one second** if the ball travelled at constant
    velocity.

EgoBall
*******

EgoBall is shown in **yellow**, and use the :ref:`ball` symbol.

.. figure:: /images/egoball.png

TeamBall
********

TeamBall is shown in **black**, and use the :ref:`ball` symbol as below,

.. figure:: /images/teamball.png

Teammate's Ball
***************

A teammate's ball is shown in its corresponding :ref:`color`, and uses the :ref:`ball` symbol.

.. _color:

Color
#####

A teammate's color is

* **red** if **playing** the ball
* **blue** if **assisting**
* otherwise, depends on it's :ref:`positioning`

.. _positioning:

Positioning
###########

Positionings are defined in ``robot/utils/PositioningDefs.hpp``.

================================================ ======= ======
Positioning                                      Color   Letter
================================================ ======= ======
POSITIONING_NONE                                 black   NA
POSITIONING_AGAINST_KICKING_TEAM_SUPPORTER       magenta F
POSITIONING_AGAINST_KICKING_TEAM_DEFENDER        black   D
POSITIONING_AGAINST_KICKING_TEAM_UPFIELDER       cyan    U
POSITIONING_FIND_BALL_FINDER                     gray    FB
POSITIONING_AGAINST_DRIBBLE_TEAM_RIGHT_SUPPORTER white   RS
POSITIONING_AGAINST_DRIBBLE_TEAM_SHOOTER         cyan    SH
POSITIONING_AGAINST_DRIBBLE_TEAM_LEFT_SUPPORTER  magenta LS
POSITIONING_AGAINST_DRIBBLE_TEAM_SWEEPER         black   SW
================================================ ======= ======

Positioning Letter
##################

The letter above a :ref:`teammate_pose` indicates it's positioning, as listed in :ref:`positioning`.

Player Number
#############

The number below a :ref:`teammate_pose` indicates it's player number.

Teammate WalkingTo
##################

The position of where a teammate robot is moving to when anticipating or in global find ball
is shown with a **50% opacity** :ref:`teammate_pose` symbol.


Robot Observations
##################

Visual robot observations are shown using a **green** :ref:`robot_pose` symbol.

.. figure:: /images/obstacle.png

Observed Balls
##############

Balls directly from the vision module are shown as an **orange dot**, as below

.. figure:: /images/ball_obs.png

Observed Field Features
#######################

Observed T-Junctions and corners are displayed using **black**, as below

.. figure:: /images/ff_obs.png

Observed centre-circle is displayed with **orange** if the orientation is known or **red** otherwise.

.. figure:: /images/cc_obs.png

Observed field lines are displayed in **red**.

* Ball Manoeuvre
* Ball Manoeuvre target
* Anticipate Position


.. _cc_top_image:

**************************
Color Classified Top Image
**************************

.. _cc_bot_image:

*****************************
Color Classified Bottom Image
*****************************

.. _bb_variables:

********************
Blackboard Variables
********************
