#############
Ball Detector
#############

Ball detection is a critical component of any robot soccer system. The 2016 transition to a black and white ball has made the task significantly more difficult.
The ball can no longer be distinguished from other objects by its colour alone,
instead requiring a more complex system that considers a candidate’s appearance. This rendered the 2015 orange ball detector entirely ineffective. The 2017
ball detector adequately met this challenge primarily making use of the circular
shape of the ball and its distinctive pattern. Despite this, the 2017 ball detector
had a number of limitations and assumptions. The structure of the 2017 ball
detector remained in 2018, with improvements made to address its limitations,
increasing the reliability and accuracy.

Inside the ball detector, all regions are passed initially filtered through a ball
candidate finder. The regions from the Connected Component Analysis are not always a perfect
crop of the ball and can include field lines, other robots and goal posts with the ball.
A tightly cropped and consistently scaled
region of interest is desirable as it significantly simplifies the problem of ball
pattern detection. Achieving a tight crop is the role of the ball candidate finder.
For “easy” cases cropping is done by Naive ROI, while more
complex regions require Blob ROI. We also eliminate regions
that are clearly not ball like due to size and shape. Scaling is performed in the
region regeneration step.

Next, region specific pre-processing is performed to adjust
the image and make the major features of the ball candidate more salient. The
white pixels are used to perform a circle fit, and we discard regions for which an
adequate circle cannot be found.

A ball candidate that reaches this stage undergoes two final heuristic checks
to analyse the likelihood that it is a ball. Each
of these checks give the candidate a score if passed. To be considered a ball a
candidate must achieve a score above a certain score threshold.

**More details can be found in the** `Team Report 2018 <http://cgi.cse.unsw.edu.au/~robocup/2018/TeamPaper2018.pdf>`_.
