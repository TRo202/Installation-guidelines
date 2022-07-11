# Installation tips
To leave some tips for some annoying errors when installing or running some programs.......

NOTE: guidelines here are based on M1.


## UTM 

* ### Ubuntu 18.04
  Problem: "Stuck in black screen with flashing cursor when booting to install Ubuntu"

  Solution: Change the display setting from "Graphics interface" to "Console interface" when running installation codes.

* ### Ubuntu 20.04
  Error: "EFI stub: Exiting boot services and installing virtual address map…"

  Cause: Sometimes UTM becomes frozen, and when you forcibly shut down the virtual machine, this error will occur when rebooting it.

  Solution:     
      1) In the VM setting, switch display setting from full graphics to console mode.   
      2) Restart the VM and go into “Ubuntu”    
      3) Run fsck -y /dev/mapper/ubuntu--vg-root (Read the code, and if it’s fsck.ext4, type it instead of “fsck”. If the directory is a bit different from the code, use the one written in the code)    
      4) Run exit. Close the VM and switch display setting back to full graphics.


## MoveIt 2 (Foxy)
  1. Problem: "Cannot locate rosdep definition for [python-lxml] and [python3]"    
  - When running `rosdep install -r --from-paths . --ignore-src --rosdistro $ROS_DISTRO -y`,    
  error code is `ERROR: the following packages/stacks could not have their rosdep keys resolved to system dependencies:    
    moveit_kinematics: Cannot locate rosdep definition for [python-lxml]    
    moveit_ros_planning_interface: Cannot locate rosdep definition for [python3]`

  - Solution:     
    1) Run `echo $ROS_DISTRO` to make sure ROS_DISTRO environment variable is set
    2) Run `rosdep resolve python-lxml -v`. But `ERROR: no rosdep rule for 'python-lxml'`          
    3) Run `sudo apt update`, `sudo apt dist-upgrade`.    
    
  2. Problem: "fatal error: linux/errno.h: No such file or directory"
  - When running `colcon build --mixin release`     
  error code is `/usr/include/aarch64-linux-gnu/bits/errno.h:26:11`
  
  - Solution:
    1) install the missing file `linux.errno.h` by installing “linux-libc-dev-arm64-cross” package by running `sudo apt-get install linux-libc-dev-arm64-cross`     
    * Note to check which package you’re missing
(https://packages.debian.org/search?searchon=contents&keywords=errno.h&mode=exactfilename&suite=bullseye&arch=any)
