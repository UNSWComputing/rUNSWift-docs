##################################
Connected Component Analysis (CCA)
##################################

Currently, everything of interest on the RoboCup Soccer SPL field is primarily
white. In the 2017 vision system, regions of interest (ROIs) were created by
finding white areas in a colour calibrated image. Minimal changes was required
to move to the binarised image in 2018. These ROIs are located using a connected
component analysis algorithm as described in
`Sequential operations in digital picture processing <https://www.cs.virginia.edu/~jlp/66.sequential.op.pdf>`_
with some modifications.

Since we just need the bounds of the regions, only the first pass of the algorithm is performed, recording the axis aligned extents of each group of pixels.
When this is done connected groups can be quickly merged by taking the maximums of these bounds.

This algorithm tends to produce large groups containing most of the objects
in the frame due to field lines connecting other white objects, such as the ball.
As this is undesirable for the purposes of locating important objects the we split
the scene into a grid, and prevents components from being connected across
grid lines. Unfortunately, this may split useful objects like the ball so the system
merges nearby groups where the edged of the bounding box have a sufficient ratio
of white to not white pixels. This achieves bounding boxes that are reasonably
likely to contain interesting objects, tightly bounded when those objects are not
close to other white objects.

**Figure below describes the region finding.** From left to right: The binary image. Regions
generated without grid splitting. Regions generated with grid splitting, culled
to show only ball like regions. Final regions generated with grid splitting and
merging, culled to show only ball like regions.

.. figure:: ../../images/connected_component_analysis.png
