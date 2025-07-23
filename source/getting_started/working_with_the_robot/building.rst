########
Building
########

To compile (build) the codebase for a V6 robot, run

.. code-block:: bash

    $ build-relwithdebinfo-2.8.sh

.. tip::

    Optionally, you can also compile just a single program, such as

    .. code-block:: bash

        $ build-relwithdebinfo-2.1.sh offnao.bin

    Possible programs that can be built are listed below.

    ============================== ============================== ==============================
                  v6                     v5 + offnao/vatnao           native + offnao/vatnao
    .                              .                               needed for v6 robot detector
    ------------------------------ ------------------------------ ------------------------------
    build-relwithdebinfo-2.8.sh    build-relwithdebinfo-2.1.sh    build-relwithdebinfo-native.sh
    ============================== ============================== ==============================
    runswift                       runswift                       runswift
    state-estimation-simulator.bin offnao.bin                     offnao.bin
    .                              vatnao.bin                     vatnao.bin
    .                              vatnao-legacy.bin              vatnao-legacy.bin
    .                              state-estimation-simulator.bin state-estimation-simulator.bin
    ============================== ============================== ==============================

.. note::
    By default, the maximum number of processors available will be used for compilation.


.. tip::
    Builds can fail in strange ways sometimes. Try ``build-relwithdebinfo-2.8.sh -B`` to do a clean build
