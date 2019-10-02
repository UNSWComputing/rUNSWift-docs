#########
Behaviour
#########

In 2018, we modified our behaviour architecture to improve dynamic role switching.
From 2010, the higher level layers of rUNSWift’s behaviours have been written in Python, allowing faster development. Our behaviours are modelled off a
decision tree. Nodes are divided into two categories, roles and skills. Roles, such
as “Goalie” and “Penalty Striker”, define what the robot should be doing during
a game. Skills are specific actions a robot has chosen to take.

Skills range from relatively high level actions, such as approaching the ball
or walking to a global point on the field, to lower level actions, such as stand or
crouch. This allows the low level skills to be inherited as components of several
higher level skills, which in turn are used by one or more roles.

State transitions can happen a frequently when a robot is involved in ball
play. Under the old system, when transitions take place in high level skills, all
child skills must be reinitialised. This process creates a computational overhead
that reduced robot responsiveness, particularly during critical periods of play
around the ball. To mitigate this we redesigned our system so that all objects
are initialised at the start, and a reset routine is called on only the nodes of
interest when a transition takes place
