##############
Robot Detector
##############

As robots are significantly larger than the other objects on the field the standard
Connected Component Analysis does a poor job of finding candidates. To solve this
the region finder is run again at a low resolution with different grid and merging
settings. Clusters of these regions are grouped in order to generate candidate
robot regions, containing all regions forming the cluster.

The second part of the pipeline is the classifier. As with every component of
vision the key factor here is balancing the constraints of accuracy and efficiency.
Decision trees are extremely efficient, however, they struggle with the highly
variable appearance of robots. A machine learning method, random forest, is
used to bag the regions into the correct categories. In addition, careful feature
engineering is essential to achieve good performance. A large variety of features
were tested, and the following features were found to be the most informative:

* Width/height ratio
* White/black pixels ratio
* Size of the bounding box
* Mean of the pixels (binary image)
* Variance of the pixels (binary image)
* Scaled Mass Centre’s X
* Scaled Mass Centre’s Y
* Hu moments (`Visual pattern recognition by moment invariants <https://ieeexplore.ieee.org/document/1057692>`_)
* Zernike moments (`Invariant image recognition by zernike moments <https://ieeexplore.ieee.org/document/55109/>`_)

The scaled mass centre is calculated by dividing the zero order moments by
the first order moments. Hu and Zernike moments are values that relate to the
shape of the pattern in the image.

Each tree in the random forest is given access to a subset of these features.
This results in a variety of different decision trees, which leverage different aspects of the region’s appearance. These trees are then composed together, with
the vote of the “forest” giving a better classification quality than the individual
trees.
