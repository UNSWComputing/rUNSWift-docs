######
Vision
######

The Vision module begins by retrieving both the top and bottom camera
images. If one of the images is not ready, the thread will wait until
they are both ready. Two primary foveas are constructed from the raw
images, one per camera, to form the basis of the vision pipeline. The
top camera image is scaled down from 1280x960 (native camera resolution)
to 160x120 whilst the bottom camera image is scaled down from 640x480 to
80x60.

A region of interest finder is used to extract the white blobs out of
the image. Once these regions have been found, they are passed into each
detector which is tasked with determining whether that region has the
object it is trying to detect or not.


.. toctree::
   :maxdepth: 2

   image_thresholding
   field_boundary_preprocessor
   region_of_interest_preprocessor
   field_feature_detector
   ball_detector
   robot_detector
