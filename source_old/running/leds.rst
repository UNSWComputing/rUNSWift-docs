####
LEDs
####

.. warning::
    LED Colours have not been updated for the V6 yet, don't 100% trust the information here

************
Chest Button
************

+-----------------------+------------------------------+-----------------------------+
| Chest button colour   | runswift State               | libagent State              |
+=======================+==============================+=============================+
| Flashing Red          | runswift is not responding   | libagent is in limp mode    |
+-----------------------+------------------------------+-----------------------------+
| Flashing Yellow       | runswift is not responding   | libagent is in stand mode   |
+-----------------------+------------------------------+-----------------------------+
| Flashing Green        | runswift is responding       | libagent is in limp mode    |
+-----------------------+------------------------------+-----------------------------+
| Solid Red             | runswift is not responding   | libagent is in sit mode     |
+-----------------------+------------------------------+-----------------------------+
| Solid Green           | runswift is responding       | libagent is in sit mode     |
+-----------------------+------------------------------+-----------------------------+

********
Left Ear
********

Shows Battery Charge, each LED indicates approximately 10%.

================ ===========================================
Effect           Description
================ ===========================================
LEDs turning Off Charging (LEDs fill up from current value)
LEDs turning On  Discharging (LEDs empty from current value)
================ ===========================================


*********
Left Foot
*********

============= ================================
Colour        Description
============= ================================
Flashing Pink Python Error
------------- --------------------------------
Solid White   Robot is on the Kicking Team
------------- --------------------------------
Off           Robot is not on the Kicking Team
============= ================================

**********
Right Foot
**********

============= ================================
Colour        Description
============= ================================
Flashing Pink Python Error
------------- --------------------------------
Solid White   Robot is on the Kicking Team
------------- --------------------------------
Off           Robot is not on the Kicking Team
============= ================================


********
Left Eye
********

=============== ===============
Colour          Description
=============== ===============
Flashing Pink   Python Error
--------------- ---------------
Flashing Red    Fallen Robot
--------------- ---------------
Flashing Yellow Falling Robot
--------------- ---------------
Flashing Green  Robot Picked Up
--------------- ---------------
Solid Red       Ball Detected
=============== ===============

*********
Right Eye
*********

=============== ===============
Colour          Description
=============== ===============
Flashing Pink   Python Error
--------------- ---------------
Flashing Red    Fallen Robot
--------------- ---------------
Flashing Yellow Falling Robot
--------------- ---------------
Flashing Green  Robot Picked Up
--------------- ---------------
Solid Red       Ball Player
--------------- ---------------
Solid Blue      Assisting
=============== ===============
