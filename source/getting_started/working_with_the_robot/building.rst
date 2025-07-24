########
Building
########

To compile (build) the codebase for a V6 robot, run

.. code-block:: bash

    $ make build
    # or
    $ cd robot_ws
    $ colcon build --cmake-args ' -DCMAKE_BUILD_TYPE=Release'

.. tip::

    Optionally, you can also compile just a package


.. tip::
    Builds can fail in strange ways sometimes. Try TODO to do a clean build
