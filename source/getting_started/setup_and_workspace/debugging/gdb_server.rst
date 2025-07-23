##########
GDB Server
##########

To run gdb, complete with symbol table for debugging, we need to compile
runswift, configured for GDB, and run a gdb server on the naos.
Fortunately, this is made easy with some simple scripts:

#. ``build-relwithdebinfo.sh`` Build complete with all debugging information,
   ready for gdb
#. ``nao_sync -rg <ip/hostname of nao>``. Sync with debugging symbols.
#. ``nao_connect_gdb <ip/hostname of nao>`` Open ports required for gdb
   server and ssh into the nao itself. You are now on the nao.
#. ``runswift_gdbserver`` Start up runswift, but wait for the remote gdb
   instance to connect. If you need to restart, you only need to run
   this command.
#. In a seperate terminal, run ``nao_remote_gdb`` Start up the remote gdb instance and connect to
   the runswift process running on the nao.

If everything has worked, you should see something like the following:

::

    GNU gdb (Ubuntu 7.7.1-0ubuntu5~14.04.2) 7.7.1
    ...
    For help, type "help".
    Type "apropos word" to search for commands related to "word".
    0xb78d78f0 in ?? () from /lib/ld-linux.so.2
    (gdb) ▯

From now on, you can use gdb as normal. Type ``c``/``continue`` to run.

If you want to make changes, you only need to run steps 1, 2 and 4 (in
the nao terminal) again, unless you've disconnected from the nao.

It should be noted that this is going to be running much slower than
normal, so any tasks requiring heavy syncing may not work as
anticipated.
