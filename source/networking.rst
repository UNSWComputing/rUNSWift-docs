##########
Networking
##########

============== ============== ======== =================== ======= ============================================
From           To             Listener Port                UDP/TCP Description
============== ============== ======== =================== ======= ============================================
Nao            Nao/GC         Nao/GC   10000+team          UDP     Team Communication, serialised as in memory
-------------- -------------- -------- ------------------- ------- --------------------------------------------
Nao            Offnao (PC)    Nao      10125               TCP     Debug information, serialised using protobuf
-------------- -------------- -------- ------------------- ------- --------------------------------------------
Offnao (PC)    Nao            Nao      10125               TCP     Sends commands, serialised using protobuf
-------------- -------------- -------- ------------------- ------- --------------------------------------------
Nao            GameController GC       3939                UDP     Notifies GameController that robot is alive
-------------- -------------- -------- ------------------- ------- --------------------------------------------
GameController Nao            Nao      3838                UDP     Sends game and player statuses
-------------- -------------- -------- ------------------- ------- --------------------------------------------
Remote Control Nao            Nao      2000                UDP     Sends remote control signals to Nao
-------------- -------------- -------- ------------------- ------- --------------------------------------------
Simulated Nao  Offnao (PC)    Offnao   10125+6*team+player TCP     Debug information, serialised using protobuf
-------------- -------------- -------- ------------------- ------- --------------------------------------------
Simulated Nao  rcssserver3d   rcsss3d  3100                TCP     Sends joint angles
-------------- -------------- -------- ------------------- ------- --------------------------------------------
rcssserver3d   Simulated Nao  rcsss3d  3100                TCP     Sends perceptor readings (joints, imu, etc.)
-------------- -------------- -------- ------------------- ------- --------------------------------------------
rcssserver3d   roboviz        rcsss3d  3200                TCP     Sends scene graphs
============== ============== ======== =================== ======= ============================================
