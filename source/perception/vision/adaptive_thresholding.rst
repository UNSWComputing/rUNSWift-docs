#####################
Adaptive Thresholding
#####################

In 2018 we converted the vision system to work with binary images to be more
robust to varied lighting. This is done with adaptive thresholding, which is an
effective method for calculating the threshold dynamically in scenes with uneven levels of brightness.
This is a significant improvement on the static colour calibrated tables used by the team in previous years.

We utilise an efficient implementation (`Adaptive Thresholding Using the Integral Image <http://citeseerx.ist.psu.edu/viewdoc/download?doi=10.1.1.420.7883&rep=rep1&type=pdf>`_)
to achieve real-time thresholding on the Nao.
The algorithm determines the average y value (in the YUV422 image) of the pixels within a
square window surrounding each pixel.
If the value of the centre pixel is sufficiently lower than the average within
the window it is set to black, otherwise it is set to white. This process can
be performed efficiently, regardless of window size, with the integral image.


An example of the adaptive thresholding process below.
White pixels are considered light whilst green pixels are dark.

.. figure:: ../../images/adaptive_thresholding.png

As this method does not rely on specialised colour tables the exposure of the
image may be allowed to vary. This has allowed us to enable auto exposure on the
camera, further improving our system’s robustness to changes in lighting. Target exposure was brought down to minimise motion blur. Furthermore, manual
colour classification of the environment before each game is no longer necessary,
reducing the setup time. The main downside is the loss of colour information,
previously used to determine the field boundary.
