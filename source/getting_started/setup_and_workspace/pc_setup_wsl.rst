##########
WSL & Ubuntu Native Instructions
##########

If you work on Windows, using the rUNSWift Docker image is the simplest way to get up and running.
However, IsaacSim only works with WSL so I've written this for anyone who wants to follow my steps.
This guide is also applicable to anyone not running the Docker image.


1. Install Ubuntu 22.04 from the Microsoft Store: https://www.microsoft.com/store/productId/9PN20MSR04DW?ocid=pdpshare
2. Install Docker Desktop, and ensure you have WSL support enabled: https://docs.docker.com/docker-for-windows/wsl/
3. Clone the repo
4. Run ``make setup`` which installs 3rd party packages
5. Ctrl F the docker file for ``sudo apt install`` and install everything that's in the docker file. All may not be necessary but doing them all will avoid issues later
6. Ctrl F the naoimage-snippets for ``sudo apt install`` and install everything there. Again, not necessary but if you want to simulate the robot, the robots depend on some of these.

.. note::
    The below steps haven't been tried as of 2025

GUI apps should work out of the box if you're on Windows 11 via Wslg. I haven't tested this
Explore running your own X11 server (we have faced some issues around OpenGL in wslg).

Vcxsrv works great for this purpose.

