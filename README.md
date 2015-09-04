# Naga_KeypadMapper
This little linux xorg daemon allows you to map the side keypad of the Razer Naga series mice via a configuration file called mapping.txt under $HOME/.naga/ . requieres xdotool and a X server enviroment to work.

Currently tested only for Razer Naga Epic (pre-2014 version) in Ubuntu 14.04 and Razer Naga 2014 (thanks to Destroyer) in Ubuntu 15.04.


You can configure the daemon for any other Razer mice easily, see below.


For Naga epic just change the param in nagastart.sh to:
 sudo naga epic

More info and mapping syntax in README

Be adviced that I release this project without any sort of warranty. So use under your own responsability.

This daemon does not, in any case modify any system file nor propertie of any device. So the process is totally reversible just by deleting the files and at most rebooting. It is absolutely non invasive


#INSTALLATION

It does not need any dependencies besides having installed xdotool http://www.semicomplete.com/projects/xdotool/  (in the oficial ubuntu repositories)
and g++

Just run install.sh as sudo.
This will compile the source and copy the necesary files (see install.sh for more info)

 NOTE:
 
Change nagastart.sh to adapt the installation to some other device. You will also have to change a couple of lines in the source code if the device has more or less than 12 buttons of different key Codes than the naga, more information in naga.cpp.

#USAGE
The instalation process automatically executes the daemon in the background and set it to start at boot for you. But you can still run it manually as follows:

nagastart.sh does the below process automatically:

1) naga executable has to be called as sudo or have the s bit up with chmod u+s at least.
- I dont know how to overcome the need for sudo privileges, if you know let me know please!

2) Init the mapper by calling: $./naga epic or $./naga 2014

3) In order to get rid of the original bindings you have to disable the keypad using xinput as follows:

$ xinput set-int-prop [id] "Device Enabled" 8 0

where [id] is the id number of the keypad returned by $ xinput.

4) You have to also run 

$ xinput set-button-map [id2] 1 2 3 4 5 6 7 11 10 8 9 13 14 15

where [id2] is the id number of the pointer device returned by $ xinput - in case of naga 2014 you also have to check which of those two has more than 7 numbers by typing $ xinput get-button-map [id2]

This lasts until the x server is restarted (nagastart.sh is aware of this), but you can enable it back to completly restore the changes by changing the last 0 to a 1.

#UNINSTALATION

You just have to delete the files created:

$ sudo rm /usr/local/bin/naga ~/.config/autostart/naga.desktop /usr/local/bin/nagastart.sh
$ sudo rm -r ~/.naga
