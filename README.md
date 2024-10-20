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
$sudo apt update -y
$sudo apt upgrade -y

#INSTALL SOFTWARE
#elogind fixes pid error and shutdown error
$sudo apt install elogind 
#list of desktops:        https://packages.debian.org/unstable/task-desktop
$sudo apt install task-lxde-desktop
$sudo apt install xserver-xephyr -y
$sudo apt install nano -y

#DISABLE LIGHTDM
$sudo systemctl disable lightdm

#CREATE STARTUP SCRIPT
#"gol" is just a name, change it...
$sudo nano /usr/bin/gol
#Type IN NANO/GOL

Xephyr -br -fullscreen -resizeable :20 &

sleep 5

DISPLAY=:20 startlxde &

#CTRL+O TO WRITE
#ENTER TO SAVE
#CTRL+W TO EXIT NANO

#CHANGE SCRIPT PERMISSION TO EXECUTABLE
$sudo chmod+x /usr/bin/gol

#START LXDE
$gol

#Install Gnome Boxes
#Open LXDE Terminal
$sudo apt install libvirt-clients
$sudo apt install gnome-boxes

#[I](https://www.reddit.com/r/Crostini/comments/qtk3bm/run_ssh_server_on_chromebook/) 
I managed to log into my/our Chromebook(s) via ssh and have access to all the files on it (also outside of the Linux container) as long as folders are shared with the container.

Inside of Linux container:

first set passwords:
sudo su
passwd
passwd <user>
remove file
sudo rm /etc/ssh/sshd_not_meant_to_be_run
ensure these lines are activated in the server config file /etc/ssh/sshd_config:
AllowAgentForwarding yes
AllowTcpForwarding yes
Port 1088 (arbitrary, anything above 1024, port 22 and 2222 are banned for ssh)
=> In Chrome OS settings add port 1088 (Linux forwarding) and activate it
sudo systemctl start ssh
sudo systemctl enable ssh
maybe restart and connect from outside machine:
ssh -p 1088 <user>@<chromeOS-IP\_notLinuxContainerIP>
The IP address is not the IP of the container but of the Chromebook, like f.i.
ssh -p 1088 jo@192.168.100.5
