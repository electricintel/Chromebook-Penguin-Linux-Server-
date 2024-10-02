#Desktop Install Overview

#-Install Linux Environment
#-Update Debian
#-Install software
#-Disable LightDM greeter
#-Create script for starting up the desktop

#Install Linux Environment with mouse clicks:
Open Settings
Search for Linux
Install Environment

#From Penguin Terminal:

#UPDATE 
sudo apt update -y
sudo apt upgrade -y

#INSTALL SOFTWARE
#elogind fixes pid error and shutdown error
sudo apt install elogind 
#list of desktops:        https://packages.debian.org/unstable/task-desktop
sudo apt install task-lxde-desktop
sudo apt install xserver-xephyr -y
sudo apt install nano -y

#DISABLE LIGHTDM
sudo systemctl disable lightdm

#CREATE STARTUP SCRIPT
#"gol" is just a name, change it...
sudo nano /usr/bin/gol
#Type IN NANO/GOL
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
