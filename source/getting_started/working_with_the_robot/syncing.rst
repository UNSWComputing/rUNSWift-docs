#######
Syncing
#######

To sync code in the ``image/`` directory, such as behaviours and configs, run

.. code-block:: bash

    $ nao_sync mario

To sync the compiled ``runswift`` program, add the ``-r`` flag

.. code-block:: bash

    $ nao_sync -r mario

.. note::

    Replace ``mario`` with the name of the robot's head you're using


*******
Options
*******

Commonly used options are below.

====== =========================================
Option Description
====== =========================================
-r     upload the compiled ``runswift`` program
------ -----------------------------------------
-d     delete contents of ~/nao
------ -----------------------------------------
-g     upload debugging symbols for gdb
====== =========================================

.. seealso::

    ``nao_sync --help`` for complete list of options

.. tip::

    Options can be concatenated, such as ``nao_sync -rd mario``.
