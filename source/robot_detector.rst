##############
Robot Detector
##############

The 2017 Robot Detection uses the Colour Rois to find clusters of white
in the top camera. A cluster is defined as any collection of regions
that overlap or touch each other. The cluster's boundary box is then
classified as the cluster's heightest point to its lowest and its
furthest left and right values.

These clusters have some rudimentary checks done on them to check size,
percentage of area in them which is actually part of a colour roi, and
its width to height ratio. Anything which is too small, does not have
enough area covered by colour rois or is not taller than it is wide is
discarded. Everything else is classified as a robot.

This is a simple detector and as such it often will get other objects on
the field that are large and white (i.e. goal posts). It also misses
robots that have fallen over or are very close as these do not usually
match the width to height ratio. However as we check percentage of
white, field features do not tend to be falsely classified.

Details on robot detection prior to 2017 can be found
`here <http://cgi.cse.unsw.edu.au/~robocup/2014ChampionTeamPaperReports/20140831-Jaiden.Ashmore-RobotDetectionReport.pdf>`__.
