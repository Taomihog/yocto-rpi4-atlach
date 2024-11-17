1. update system and install tools:  
>sudo apt update  
>sudo apt upgrade  
>sudo apt install -y git gcc g++ make unzip texinfo wget chrpath diffstat bc cpio diffstat texinfo gawk build-essential libsdl1.2-dev xterm python3 python3-pip libssl-dev libsdl1.2-dev libncurses5-dev liblzma-dev zlib1g-dev lz4  

use gedit or vi to edit the ~/.bashrc, add at the end:  

alias python=python3  

close the file, then source it:  
>source ~/.bashrc  

2. clone poky ref distro and checkout ‘kirkstone’ (or other LTS branches):  
>cd ~  
>mkdir Projects  
>cd Projects  
>git clone git://git.yoctoproject.org/poky.git  
>git branch -r  
>git checkout kirkstone  

3. clone rpi bsp, then checkout ‘kirkstone’ (or other LTS branches):  
>git clone https://github.com/agherzan/meta-raspberrypi  
>git checkout kirkstone  

4. source environment:  
>source poky/oe-init-build-env build-rpi4  

show layers included:  
>bitbake-layers show-layers  

5. use gedit to edit bblayers.conf:  
>gedit conf/bblayers.conf  

then add ‘meta-raspberrypi’ to BBLAYERS, the result text should be similar to this:  

BBLAYERS ?= " \\   
  /home/xx/Projects/yocto/poky/meta \\  
  /home/xx/Projects/yocto/poky/meta-poky \\  
  /home/xx/Projects/yocto/poky/meta-yocto-bsp \\  
  /home/xx/Projects/yocto/meta-raspberrypi \\  
  "

6. use gedit to edit:  
>gedit conf/local.conf  

then change this:  

\# This sets the default machine to be qemux86-64 if no other machine s selected:  
MACHINE ??= "qemux86-64"  

to this (or the other machine you need that listed in ‘meta-raspberrypi/conf/machine’ folder):  

\# This sets the default machine to be qemux86-64 if no other machine s selected:  
\# MACHINE ??= "qemux86-64"  
MACHINE ??= "raspberrypi4"  

7. build menuconfig to make changes to your kernel:  
>bitbake menuconfig virtual/kernel  




Reference:  

1. Shawn Hymel’s YouTube Tutorial Series “ Introduction to Embedded Linux” on Digi-Key channel:  

2. https://git.yoctoproject.org/meta-raspberrypi/about/  

3. ChatGPT  




