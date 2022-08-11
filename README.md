# Installation tips
To share some tips for some annoying errors when installing or running some programs.......

NOTE: guidelines here are based on M1.

So far, Multipass seems to be the best (and perhaps only) option for running Ubuntu 18.04 on M1

## Multipass
* GUI Dekstop Environment 
    
  Use Microsoft Remote Desktop app   
  `sudo apt update`   
  `sudo apt upgrade`  
  `sudo apt install ubuntu-desktop xrdp`
      
  After installation, you need to set a password.   
      
  Then when you run the app,   
  <img width="603" alt="스크린샷 2022-08-12 오전 1 11 23" src="https://user-images.githubusercontent.com/102891484/184180357-1baaab9c-12d4-4b4a-b7c8-8eddafe6b057.png">   
  click '+' and 'Add PC'
      
  Copy the IP address (on multipass terminal) or IPv4 (if you run `multipass info <'name of the linux'>`)
      
  ![이미지 2022  8  12  오전 1 38 중간](https://user-images.githubusercontent.com/102891484/184189325-e26f7c48-e7af-473f-92a7-c9fa3ca16e5e.jpeg)   
      
  and paste it in the PC name of the 'Add PC' screen.
  
  <img width="473" alt="스크린샷 2022-08-12 오전 1 50 22" src="https://user-images.githubusercontent.com/102891484/184189811-1227c8a7-c03a-4f2e-92f9-b668503f3ac4.png">
      
  A new PC is now added.

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
