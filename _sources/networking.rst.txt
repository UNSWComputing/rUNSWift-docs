##########
Networking
##########

============== ============== ============= ======= ============================================
From           To             Port          UDP/TCP Description
============== ============== ============= ======= ============================================
Nao            Nao            10000 - 10250 TCP     Team Communication, not serialised
-------------- -------------- ------------- ------- --------------------------------------------
Nao            Offnao (PC)    10125         TCP     Debug information, serialised using protobuf
-------------- -------------- ------------- ------- --------------------------------------------
Offnao (PC)    Nao            10125         TCP     Sends commands, sent as text
-------------- -------------- ------------- ------- --------------------------------------------
Nao            GameController 3939          UDP     Notifies GameController that robot is alive
-------------- -------------- ------------- ------- --------------------------------------------
GameController Nao            3838          UDP     Sends game and player statuses
-------------- -------------- ------------- ------- --------------------------------------------
Remote Control Nao            2000          UDP     Sends remote control signals to Nao
-------------- -------------- ------------- ------- --------------------------------------------
Simulated Nao  Offnao (PC)    10125 - 11661 TCP     Debug information, serialised using protobuf
-------------- -------------- ------------- ------- --------------------------------------------
Simulated Nao  rcssserver3d   3100          TCP     Sends joint requests
-------------- -------------- ------------- ------- --------------------------------------------
rcssserver3d   Simulated Nao  3100          TCP     Sends joint angles and vision information
============== ============== ============= ======= ============================================
