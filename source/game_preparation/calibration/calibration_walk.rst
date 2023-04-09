###############
Camera Settings
###############



************
Instructions
************

#.  ``image/home/nao/data/behaviours/body/skills/Walk.py``

    The higher the speed, the more likely the robot is to fall over.

    .. code-block:: bash

        # Range between 0.0 and 1.0. Use 0 in lab and 1 in serious games. v5 robots
        # do not work with low speed - 0.5 is functional. v6 need further testing.
        SPEED = 0.4
