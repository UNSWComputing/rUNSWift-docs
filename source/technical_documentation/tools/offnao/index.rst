######
Offnao
######

Offnao is a tool built in house that collects, saves, restores and streams data
from Nao robots. It can record all the data from the robot’s sensors, including
either the colour classified or raw camera data. If given the raw camera data
Offnao can also run the vision system offline. Offnao also collects information
about the internal state of the robot, such as its beliefs about its position, team
mate position and ball position, along with what the vision system has detected.

All this information can be displayed through various visualisation methods,
including annotated versions of the robot’s camera image and an overhead field
view.

.. figure:: /images/offnao.png

Kinematic offsets can be calibrated to compensate for differences in the head mounting
and looseness in the robot’s joints. Debug logs recorded by the main code may
be viewed. Finally, raw data from the non vision sensors, such as sonar and foot
sensors, can be monitored.

.. toctree::
   :maxdepth: 2

   overview
