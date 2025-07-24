########
Work in progress
########

In 2024, rUNSWift underwent major changes in order to move to an Ubuntu-based 
image. In 2025, rUNSWift underwent more major changes and moved to ROS2 Humble.
In 2025, it was announced that the 2026 RoboCup-SPL will be merging with the 
RoboCup Humanoid Kids-size League, and almost definitely changing from the NAO
platform. As such, many things weren't fully completed and this page aims to 
summarise all of the things that weren't quite finished.

structure:
We aimed to set up with a desktop_ws for simulators, and other desktop things. It
didn't quite all make it to the same place, and desktop_ws and robot_ws are a bit 
jumbled. We also only have a `make build` for robot_ws and nothing for desktop_ws

ROS2:
we transitioned to ros2 successfully, but nobody was an expert so there's still 
some things we didn't touch. Working with components, intra-process communication
and custom RMW are all concepts we haven't touched. We also haven't moved to a 
ROS2 like way of config files.

Threads etc:
In legacy, they locked threads for different tasks. Now that everything runs as 
nodes and we didn't have a lot of knowledge or time to test, we haven't quite 
settled on the most efficient way to run everything smoothly with regards to threads.

Shared IDE addons would be good. TODO add 2024 link

