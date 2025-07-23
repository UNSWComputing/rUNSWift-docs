###########################################
WSL Instructions (Recommended for Windows)
###########################################

If you work on Windows, using Ubuntu via WSL with Docker would be the simplest way to get up and running.

1. Install Ubuntu 22.04 from the Microsoft Store: https://www.microsoft.com/store/productId/9PN20MSR04DW?ocid=pdpshare
2. Install Docker Desktop, and ensure you have WSL support enabled: https://docs.docker.com/docker-for-windows/wsl/
3. Clone the repo, and run ``make build-all``. Everything should just work.

GUI apps should work out of the box if you're on Windows 11 via Wslg.
Explore running your own X11 server if you have issues with offnao (we have faced some issues around OpenGL in wslg).

Vcxsrv works great for this purpose.

