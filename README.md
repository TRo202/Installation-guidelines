# Installation-guidelines
To leave some tips for some annoying errors when installing or running some programs.......

NOTE: guidelines here are based on M1.


## UTM (virtual machine)

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
