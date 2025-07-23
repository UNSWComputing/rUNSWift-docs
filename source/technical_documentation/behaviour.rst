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

# Reilly note: Adding from architecture in case any blackboard stuff is relevant.

Threads
~~~~~~~

The threads are run in a function called safelyRun, which:

-  restarts the thread in the event of a segfault or other fatal signal
-  restarts the thread in the event of an exception being thrown
-  monitors for the thread if it goes overtime
-  sleeps the thread if it goes undertime (to allow other threads to
   run)
-  [re]constructs the thread, repeatedly calls the thread's tick()
   function, and destructs the thread safelyRun stop calling tick() when
   ctrl-c is pressed or the interrupt signal is received. Additionally,
   perception is monitored for freezes (tick() does not return).

To decrease the need for locks, and decrease the possibilities for
segfaults, most of the blackboard variables are not pointers, and exist
as long as the blackboard exists. It would be a concurrency error to
have one thread write a new pointer to the blackboard and free the old
one, while another thread may be accessing its contents. Some blackboard
variables are smart pointers to avoid this.

Multiple threads should never write to the same blackboard variable. If
two threads ever happened to write simultaneously, it could crash
either/both threads, as well as leaving corrupt data, causing another
thread to crash. Each sub-blackboard is written to only by its
corresponding top-level module.

Note that reads of structures on the blackboard greater than 1-word in
size, are not necessarily atomic, as the read may be interleaved with
another thread's write. An example is when reading from
``blackboard->receiver.data``.

Blackboard
~~~~~~~~~~

The `blackboard <../tree/master/robot/blackboard/>`__ is a global
variable where threads share information. The blackboard is broken into
sub-blackboards for each top-level module. Each sub-blackboard is
written to by its corresponding top-level module. Variables on the
blackboard should not contain pointers. Adding a variable to the
blackboard does not make it immediately accessible in offnao. You have
to manually archive it, see [[Blackboard Serialization]].


# Reilly note, same as above


Python Infrastructure
---------------------

We use python as a high level language for writing behaviour code. The
reasons for this are discussed in depth at: `Carl Chatfield Robocup
Report 2012 - Chapter
3 <http://cgi.cse.unsw.edu.au/~robocup/2012site/reports/CarlChatfieldRoboCupReport2012.pdf>`__

In order to enable this, we use the boost python libraries to set up an
embedded python interpreter within our ``runswift`` executable that has
access to parts of our blackboard. In every perception cycle, an entry
tick() function is called by our c++ code within the python interpreter
instance with a reference to the blackboard. The expected return value
is a BehaviourRequest object that contains any information to pass back
into the C++ code (primarily actions for motors & leds).

Key directories relating to the python interface:

-  **robot/perception/behaviour/**

   This folder contains the c++ parts of the behaviour chain. In
   BehaviourAdapter.cpp, it creates a PythonSkill (defined in the
   ``python`` subdirectory). On every tick, it executes the PythonSkill
   which returns a BehaviourRequest to it. This is then used to write
   actioncommands to the blackboard.

   -  **python/**

      The important pieces here:

      -  wrappers - Wrappers over some data types (see the report/code
         for details).
      -  converters - Converters for arrays, etc (see the report/code
         for details).
      -  PythonSkill.cpp - The PythonSkill class manages executing a
         python interpreter (setting up modules, paths, etc). It also
         watches files and reloads the interpreter if they change. This
         is useful for quick iteration on code (simply nao\_sync your
         new code over and the robot runs the new code). It also handles
         python exceptions that are uncaught by flashing the Leds,
         saying "Python error", and reloading the code. This is useful
         because in game, if your python code reaches an untested state
         and crashes, you want the interpreter to restart and continue
         (but notify you that it failed).
      -  RobotModule.cpp - This pulls all the wrappers in and gets
         compiled into a python module which can be imported within the
         interpreter as ``robot``. You can then access parts of the
         wrapped cpp code. e.g

.. code-block:: python
        
        # This is a simple behaviour.py
        import robot
        
        def tick(blackboard): 
            req = robot.BehaviourRequest() # Creates a Behaviour Request instance.
            req.actions.leds.rightEye = robot.rgb(True, False, False) # Set right eye to red.
            return req

-  **image/home/nao/data/behaviours**

   This is where the python files that run on the robot are kept. This
   folder gets synced to the robot by nao\_sync. The highest level file
   here is ``behaviour.py``. This file is run by PythonSkill at the top
   level. It calls the tick() function on this module, passing it a
   reference to the blackboard. The function must return a
   BehaviourRequest instance. Whatever else happens is up to your python
   architecture and can be customised to match some form of state
   machine / decision tree / other behaviour system implemented in
   python.