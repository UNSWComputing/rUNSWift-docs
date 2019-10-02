######
Vatnao
######

As part of our 2016-17 Vision System changes we developed a tool to assist in
development and debugging. The tool, Vatnao, runs the vision system on a local
machine using logs recorded on the robot. It allows the developer to examine
variables, annotate images based on how Vision processes the raw frames, and
even adjust configuration in real time. We used it heavily as part of development
of the ball detector to speed up the development cycle, reducing testing time,
quickly identifying problem cases and allowing us to quickly evaluate the effects
of tweaks and changes to our code base.

Vatnao has also allowed us to break down the components of each detector.
For example, in the case of the ball detector, each heuristic can be broken down
and displayed separately to determine optimal values for the checks. The tool
also handles other modules of vision, such as field feature and robot detection.
