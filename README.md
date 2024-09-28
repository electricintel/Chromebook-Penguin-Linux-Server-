#Desktop Install Overview

#-Update Debian
#-Install software
#-Disable LightDM greeter
#-Create script for starting up the desktop

#UPDATE 
sudo apt update -y
sudo apt upgrade -y

#INSTALL SOFTWARE
sudo apt install task-lxde-desktop
sudo apt install xserver-xephyr -y
sudo apt install nano -y

#DISABLE LIGHTDM
sudo systemctl disable lightdm

#CREATE STARTUP SCRIPT
sudo nano /usr/bin/gol
#INSERT IN NANO/GOL
Xephyr -br -fullscreen -resizeable :20 &
sleep 5
DISPLAY=:20 startlxde &
#CTRL+O TO WRITE
#ENTER TO SAVE
#CTRL+W TO EXIT NANO

#CHANGE SCRIPT PERMISSION TO EXECUTABLE
sudo chmod+x /usr/bin/gol

#START LXDE
gol
