###############
Camera Settings
###############

Good camera settings make distinguishing the balls, robots and the field lines easy. Consider the shadows and change in lighting over time, and find some settings that are robust to change in lighting.

************
Instructions
************

#.  To modify Camera Settings through terminal, run

    .. code-block:: bash

        $ runswift --calibration.camera terminal

#.  Copy camera settings values into ``image/home/nao/data/runswift.cfg``.

    .. code-block:: cfg

        [camera]
        top.autowhitebalance=1
        top.exposureauto=1
        top.aetargetexposure=10
        top.autofocus=0
        top.focusabsolute=0

        bot.autowhitebalance=1
        bot.exposureauto=1
        bot.aetargetexposure=10
        bot.autofocus=0
        bot.focusabsolute=0
