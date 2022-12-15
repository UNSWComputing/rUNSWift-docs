########
Overview
########

.. figure:: /draw.io/overview_tab.png


#. :ref:`field_view`
#. Top Image
#. Bottom Image
#. Blackboard Variables

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

Ball Manoeuvre
##############

A robot's ball manouevre intention is displayed using a colored sector extending
from the ball's current location to the target ball location (indicated with a **pink** dot)

**Green** cone indicates a **kick**, while **blue** indicates a **dribble** intention.

The centre angle of the sector indicates the heading accuracy that must be achieved for the robot to execute the manoeuvre when lining up with the ball.

The radius of the sector may be finite or infinite. A finite radius indicates that the robot will try and control its kick strength to aim for a certain field coordinate,
while an infinite radius indicates that the robot will try and kick the ball in the direction of the sector with maximum power.

A maximum power kick towards the opponent goal:

.. figure:: /images/ball_manouevre.png

A dribble towards the opponent goal box:

.. figure:: /images/ball_manouevre_dribble.png

A controlled power kick towards the opponent goal box:

.. figure:: /images/ball_manouevre_soft.png

.. note::
    Dribble strength is **not** controllable

Anticipate Position
###################

The intended anticipate position of a robot that is executing an Anticipate or TeamFindBall skill is visualised using a grey
:ref:`robot_pose`, as below. The heading variance of the pie-shape indicates the acceptable heading error once the robot is at its
anticipate position.

.. figure:: /images/anticipate_position.png

