###############
Getup
###############

We fall over a lot, so we need to make sure the getup works reliably.

************
Instructions
************

#.  Find the most inclined part of the field of the next game.
#.  Run `runswift` (triple-tap), stiffen (double-tap), and put the robot in the penalised state (double single-tap).
#.  Edit the appropriate image/home/nao/data/pos/individualPoses/<robot>_getup<side><version>.pos

    The main thing to note is the head pitch during the last part of the getup.

    Here (getupBack) you can see the head pitch is changed to 31 degrees, to snap forward to help get the body up.
    Then the head pitch snaps back to 0 degrees, to stabilise the robot during standing.
    The stabilisation is the most important part of the calibration.

    .. code-block:: diff

        @@ -26,28 +30,28 @@
        
        left hand to the side a little so it doesn't fall backwards or forwards, but not straight out or it falls to the left
        # HY    HP    LSP   LSR   LEY   LER   LWY   LHYP  LHR   LHP   LKP   LAP   LAR   RHR   RHP   RKP   RAP   RAR   RSP   RSR   REY   RER   RWY   LH    RH    DUR
        -! 0     -10    106   10    0      0    0     -66   19    -45   120   -12   -10   -38   -70   24    54    3     120   -16   -30   9     0     0     0     200
        +! 0     31    106   10    0      0    0     -66   19    -45   120   -12   -10   -38   -70   24    54    3     120   -16   -30   9     0     0     0     200
        
        HY    HP    LSP   LSR   LEY   LER   LWY   LHYP  LHR   LHP   LKP   LAP   LAR   RHR   RHP   RKP   RAP   RAR   RSP   RSR   REY   RER   RWY   LH    RH    DUR
        right leg half in
        -! 0     -10    106   10    0      0    0     -68   10    -14   120   -30   -21   -27   -86   40    58    1     120   -14   -30   9     0     0     0     200
        +! 0     31    106   10    0      0    0     -68   10    -14   120   -30   -21   -27   -86   40    58    1     120   -14   -30   9     0     0     0     200
        -! 0     -10    106   10    0      0    0     -64   12    -16   120   -53   -11   -26   -70   42    53    1     120   -14   -30   9     0     0     0     200
        +! 0     0     106   10    0      0    0     -64   12    -16   120   -53   -11   -26   -70   42    53    1     120   -14   -30   9     0     0     0     200
        -! 0     -10    106   10    0      0    0     -60   23    -40   120   -61   -8    -24   -30   47    41    3     120   -14   -30   9     0     0     0     200
        +! 0     0     106   10    0      0    0     -60   23    -40   120   -61   -8    -24   -30   47    41    3     120   -14   -30   9     0     0     0     200
        
        shift body to left - the 3 lines here are the most unstable, be careful
        -! 0     -10    106   10    0      0    0     -59   24    -22   120   -68   -4    -25   -28   40    30    11    120   -16   -30   9     0     0     0     200
        +! 0     0     106   10    0      0    0     -59   24    -22   120   -68   -4    -25   -28   40    30    11    120   -16   -30   9     0     0     0     200
        
        right leg more in
        -! 0     -10    106   10    0      0    0     -57   24    -30   120   -68   0     -7    -32   82    -2    20    120   -16   -30   9     0     0     0     300
        +! 0     0     106   10    0      0    0     -57   24    -30   120   -68   0     -7    -32   82    -2    20    120   -16   -30   9     0     0     0     300
        
        sit
        $ 1     1     0     0     0     0     0     1     1     1     1     1     1     1     1     1     1     1     0     0     0     0     0     0     0     
        -! 0     -10    106   10    0      0    0     0     0     -51   121   -68   0     0     -51   122   -69   5     71    -1    34    47    -53   0     0     400
        +! 0     0     106   10    0      0    0     0     0     -51   121   -68   0     0     -51   122   -69   5     71    -1    34    47    -53   0     0     400
        
        stabilise in sitting position 
        $ 1     1     0     0     0     0     0     1     1     1     1     1     1     1     1     1     1     1     0     0     0     0     0     0     0     
        -! 0     -10    106   10    0      0    0     0     0     -51   121   -68   0     0     -51   122   -69   0     71    -1    34    47    -53   0     0     300
        +! 0     0     106   10    0      0    0     0     0     -51   121   -68   0     0     -51   122   -69   0     71    -1    34    47    -53   0     0     300
        
        stand
        $ 1     1     0     0     0     0     0     1     1     1     1     1     1     1     1     1     1     1     0     0     0     0     0     0     0     
        -! 0     -10    106   10    0      0    0     0     0     -21   49    -28   0     0     -21   49    -28   0     91    -10   90    8     90    0     0     400
        +! 0     0     106   10    0      0    0     0     0     -21   49    -28   0     0     -21   49    -28   0     91    -10   90    8     90    0     0     400

    Here (getupFront) you can see the head pitch is changed to -20 degrees, to snap further back, to stabilise the robot during standing.
    The stabilisation is the most important part of the calibration.

    .. code-block:: diff

        @@ -31,22 +31,22 @@
        HY    HP    LSP   LSR   LEY   LER   LWY   LHYP  LHR   LHP   LKP   LAP   LAR   RHR   RHP   RKP   RAP   RAR   RSP   RSR   REY   RER   RWY   LH    RH    DUR
        right leg half in
        ! 0     29    50    45    19    -18   0     -68   10    -14   120   -44   -19   -27   -86   40    58    1     120   -16   -30   9     0     0     0     100
        -! 0     -10    50    43    19    -18   0     -64   12    -16   120   -44   -19   -26   -70   42    53    1     120   -16   -30   9     0     0     0     100
        +! 0     -20    50    43    19    -18   0     -64   12    -16   120   -44   -19   -26   -70   42    53    1     120   -16   -30   9     0     0     0     100
        -! 0     -10    50    41    19    -18   0     -60   23    -13   120   -44   -19   -24   -57   47    41    3     120   -16   -30   9     0     0     0     100
        +! 0     -20    50    41    19    -18   0     -60   23    -13   120   -44   -19   -24   -57   47    41    3     120   -16   -30   9     0     0     0     100
        
        shift body to left - the 3 lines here are the most unstable, becareful
        -! 0     -10    50    40    19    -18   0     -59   24    -23   120   -68   -4    -25   -32   40    34    11    117   -16   -30   9     0     0     0     100
        +! 0     -20    50    40    19    -18   0     -59   24    -23   120   -68   -4    -25   -32   40    34    11    117   -16   -30   9     0     0     0     100
        
        right leg more in
        -! 0     -10    60    33    16    -16   0     -57   24    -26   120   -68   -7    -7    -33   82    -2    7     110   -16   -30   9     0     0     0     300
        +! 0     -20    60    33    16    -16   0     -57   24    -26   120   -68   -7    -7    -33   82    -2    7     110   -16   -30   9     0     0     0     300
        
        both leg in, body straight
        -! 0     -10    70    25    12    -12   0     -51   26    -15   120   -68   -7    -20   -15   120   -67   7     100   -16   -30   9     0     0     0     400
        +! 0     -20    70    25    12    -12   0     -51   26    -15   120   -68   -7    -20   -15   120   -67   7     100   -16   -30   9     0     0     0     400
        -! 0     -10    70    25    12    -12   0     -51   26    -15   120   -68   -7    -20   -15   120   -67   7     100   -16   -30   9     0     0     0     100
        +! 0     -20    70    25    12    -12   0     -51   26    -15   120   -68   -7    -20   -15   120   -67   7     100   -16   -30   9     0     0     0     100
        
        squat with both legs closed
        -! 0     -10    77    25    8     -8    0     0     0     -50   120   -68   0     -0    -50   120   -68   0     90    -16   -30   9     0     0     0     400
        +! 0     -20    77    25    8     -8    0     0     0     -50   120   -68   0     -0    -50   120   -68   0     90    -16   -30   9     0     0     0     400
        
        stand
        -! 0     -10    84    18    4     -4    0     0     0     -39   85    -47   0     0     -39   85    -47   0     90    -13   -15   0     0     0     0     400
        +! 0     -20    84    18    4     -4    0     0     0     -39   85    -47   0     0     -39   85    -47   0     90    -13   -15   0     0     0     0     400
        -! 0     -10    90    10    0     0     0     0     0     -28   50    -25   0     0     -28   50    -25   0     90    -10   0     0     0     0     0     400
        +! 0     -20    90    10    0     0     0     0     0     -28   50    -25   0     0     -28   50    -25   0     90    -10   0     0     0     0     0     400
