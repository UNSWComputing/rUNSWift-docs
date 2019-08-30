#############
Ball Detector
#############

Ball detection takes in a region of interest, and determines if that
region contains a ball or not. It complies with the detector interface
in the vision infrastructure.

Inside the ball detector pipeline, there are two key stages: \* Internal
ROI finding to locate a ball candidate \* Pre-processing to help clear
up the image and add robustness to lighting variations. \* Heuristic
checks to determine whether the candidate is a ball or not.
