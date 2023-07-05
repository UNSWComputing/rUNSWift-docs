###############
Walk
###############

We need to calibrate the walk speed for each opponent.

************
Instructions
************

#.  ``image/home/nao/data/behaviours/body/skills/Walk.py``

    In general, the higher the speed, the more likely the robot is to fall over.

.. note::

    It is sometimes better to have a high walk speed especially on unstable terrain, for instance, fields with a lot of wrinkles/bubbles as seen in RoboCup Asia-Pacific Tianjin 2023. Please do not feel compelled to stick to low walk speeds. However, be prepared to catch the robot while testing to prevent damaging it or use a harness. Also, consider running it in a physics simulator first if one is available.


    .. code-block:: python

        # Range between 0.0 and 1.0. Use 0 in lab and 1 in serious games. v5 robots
        # do not work with low speed - 0.5 is functional. v6 need further testing.
        SPEED = 0.4
