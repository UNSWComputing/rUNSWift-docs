############
runswift_gdb
############

GDB can be used to debug the runswift program on the NAO.

#. Sync with debugging symbols, run ``nao_sync -rg mario``.

    .. note::

        Replace "mario" with name of your robot

    .. tip::

        ``-g`` flag uploads debug symbols to the nao

#. Run ``runswift_gdb``
#. Use gdb as normal.
