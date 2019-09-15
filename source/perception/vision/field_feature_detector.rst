######################
Field Feature Detector
######################

The field edge plays a vital role in the vision pipeline. The field edge
is used to determine where the field starts so that we can save time
when scanning the image for other features like the ball or field lines.
The module sets an index for each column to indicate the pixel at the
edge of the field for all other algorithms to use as a start when
scanning.

The algorithm for detecting the field edge starts at the top of the
image and scans down until it finds a significant patch of green. This
scan is run on every column and results in a set of points across the
image. RANSAC is then applied to the set of points to attempt to extract
straight lines out of it. We attempt to detect up to two lines in any
one image, since there can be two field edges in view at any point in
time. This algorithm is run in both the top and bottom cameras
independently since the field edge may run across both images.

If no field edge is detected, then we guess if the field edge is above
or below the current camera view. This guess is based on the amount of
green present in the image. If the image contains a large portion of
green, but no distinct field edge, the field edge is assumed to be above
the camera view and the entire image is treated as being "on the field".
If not enough green is present, then the robot is deemed to be looking
off the field or into the sky.

More details can be found
`here <http://cgi.cse.unsw.edu.au/~robocup/2014ChampionTeamPaperReports/20100930-2010rUNSWiftTeamReport.pdf>`__.
