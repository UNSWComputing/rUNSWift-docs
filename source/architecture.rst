############
Architecture
############

The ``runswift`` infrastructure is fairly large, so this page lists some
key aspects and summaries. The best way to understand these in detail is
to read the reference papers and relevant code.

Overview - libraries, libagent, runswift and offnao
---------------------------------------------------

``libagent`` is the library loaded into ``naoqi`` and how ``runswift``
communicates with the robot hardware.

``soccer`` & ``soccer-static`` are the basic hardware-independent
modules (perception without cameras, networking threads, etc.). The
static version is for ``robot-static``, and the dynamic version is for
[[offnao]].

``robot-static`` is ``soccer-static`` with hardware-specific modules
(camera, some parts of motion).

``runswift`` is ``robot-static`` with ``main()``.

[[offnao]] is our current C++ visual debugger that connects to
``runswift`` via TCP.

If you poke around the cmake files, they should correlate with what's
said here, but if it doesn't, the cmake files take precedence (and
please update this).

Drivers and libagent
--------------------

Not sure about drivers? Naoqi modules are loaded by ``libagent`` `in
image/etc/naoqi/autoload.ini <../tree/master/image/etc/naoqi/autoload.ini>`__

``libagent`` is our communications bridge to the robot. It is a library
that we wrote within Aldebaran's proprietary NaoQi SDK that receives
information such as joint angles, and sends information such as LED
commands. It is also responsible for `button
presses <Button%20Presses%20for%20Nao>`__. libagent communicates with
our executable (runswift) via a shared memory object. (linux allows you
to allocate named memory that is shared with other processes.)

rUNSWift
--------

options
~~~~~~~

There are many options to the runswift executable. They can be put on
the command line, in the configuration file
`runswift.cfg <../tree/master/image/home/nao/data/runswift.cfg>`__, in
the per-robot configuration file , or sent from off-nao. They are
configured in options.cpp, and viewable by running "runswift --help".

Call tree
~~~~~~~~~

At the top of our call tree is main, naturally.
`main.cpp <../tree/master/robot/main.cpp>`__ launches threads for most
of our top level-modules, such as Perception and Motion. The threads
continuously run in a loop, independent of each other. Perception is
[currently] the only top-level module that contains other top-level
modules, namely Kinematics, Vision, Localisation, and Behaviour, which
are executed in that order. Behaviour contains a bridge to python, and
calls the execute method of a top-level python skill
(`GameController.py <../tree/master/image/home/nao/data/behaviours/skills/GameController.py>`__
skill by default).

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

Logging
~~~~~~~

We have a cout-like interface for recording log messages to a file. For
example:

``llog(INFO) << "RUNSWIFT soccer library spinning up!" << endl;``

Log files are saved in /var/volatile/runswift on the robot, and there is
one log file per source directory. The log levels available are SILENT,
QUIET, FATAL, ERROR, WARNING, INFO, VERBOSE, DEBUG1, DEBUG2, and DEBUG3.
Setting a log level will record messages of that level or higher. The
default log level is SILENT, and can be overridden using one of the
options mechanisms listed in the options section. e.g. "-l INFO" will
record messages at level SILENT, QUIET, FATAL, ERROR, WARNING, or INFO.
Using llog (especially in tight loops) takes resources, even if the set
log level is higher (e.g. "-l SILENT") than the one passed to llog (e.g.
"llog(DEBUG3)").

Adapters
~~~~~~~~

Including the blackboard in every file that needs to access a blackboard
variable has led to some unreasonably long compiles in previous years.
To alleviate this, we are using an Adapter-like pattern, where only the
files representing the top-level modules access the variables on the
blackboard. Blackboard.hpp should only be included from these special
<module>Adapter.cpp files, and the blackboard should only friend these
Adapters.

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
         wrapped cpp code. e.g \`\`\`python # This is a simple
         behaviour.py import robot

         def tick(blackboard): req = robot.BehaviourRequest() # Creates
         a Behaviour Request instance. req.actions.leds.rightEye =
         robot.rgb(True, False, False) # Set right eye to red. return
         req \`\`\`

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

Contact / Maintainer
====================

| For more information, contact
| \* ijnek - kenjibrameld@gmail.com