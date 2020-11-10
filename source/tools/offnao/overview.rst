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

TeamBall Position and Velocity
##############################

TeamBall position and velocity estimates are shown in black color as below,

 .. figure:: /images/teamball.png

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


My Pose Hypotheses
##################

All the robot pose hypotheses are **yellow**, and use the :ref:`robot_pose` symbol.
The **brush thickness** of the covariance ellipse is the **weight of hypothesis**.

.. figure:: /images/hypotheses.png

The left and right hypotheses in the image have 1.0 and 0.03 weight respectively.
The right hypotheses has an extremely small brush thickness that ends up almost invisible.

My Pose
#######

My pose is the pose hypothesis used in behaviours, and can be identified by a :ref:`robot_pose` symbol with a **white ellipse**.

.. figure:: /images/my_pose.png


* Ego Ball Position
* Ego Ball Velocity
* Teammate's ball observation
* Teammate's positions
* Teammate's player numbers
* playingBall
* isAssisting
* role and their colors
* where teammate is walking to
* visual robot obstacles
* vision balls
* observed field features
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
