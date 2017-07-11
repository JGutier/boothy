
PHOTOBOOTH

This Project started as a fork from user Zoroloco's boothy program since it was the Raspberry Pi PhotoBooth program that most closely matched what I wanted for my photobooth for my wedding on July 2017. Mine differs from his in that I didn't use an LED Light and I utilized a Raspberry Pi 3 which has more computing power so I increased the photo resolution and final image output. 

This was my first Raspberry Pi Project and first tinkering with python so there was a lot of tinkering done and I tried to comment on the code wherever I found things to tinker with.   Also, I will note a lot of unnecessary steps for experienced RPi users but things that I found useful below. 

Issues I found and couldn't figure out in time:
 - The overlay piece of code is great but it layers over the live camera preview 100% of the screen. I wish it would jsut overlay the text that you want (for example the countdown, or the instructions of what to do for the user). If you tweak the transparency it does make the camera preview more visible but almost impossible to read the overlay text in bright sunlight. 
 - The 7 inch touchscreen has pretty awful viewing angles. I set this up at about a 4' height and if you're a 6' person your view of the screen would be very bad. This relates to my first issue as well about the overlay function. 
 - Couldn't figure out a function to display the generated collage of 4 images after merging them to the user and then ask if it was OKAY and to go forward with printing. I wanted to add that piece of code and then add a second button and third button for yes and no responses (or just use the touchscreen as input). That way I wouldn't waste the paper and ink to printout an erroneous image. I tried using the PILLOW library to show it but got errors accessing the collage image so I gave up. Like I said, I'm new to this. Maybe you can figure it out. 
 - The Selphy 1200 Printer is good, very nice quality pictures but if you buy the 108 ink/paper set box you will end up with a lot of extra paper. It comes with 6 packs of 18 pages of paper, and two ink cartridges. Ink cartridge #1 lasted me for 33 Pictures. YOu would think it would last 54. So beware of that. 
 - If a print fails or hangs try https://bbs.archlinux.org/viewtopic.php?id=202022
That works. 

Required materials:
   - Raspberry 3
   - 5-5.25v, 2.1-2.4 amp DC power adaptor for the Pi. 
   - Raspberry Pi v2 Camera module 
   - 7 inch LCD screen (https://www.element14.com/community/docs/DOC-78156/l/raspberry-pi-7-touchscreen-display)
   - Canon Selphy 1200 printer & Paper/Ink Combo Pack. Those two things are about $135 at amazon. 
   - One Button ( I bought a cheap $2 button at Microcenter with two prongs)
   - Stranded / Solid jumper wires
   - Some wood working tools (Dremel, drill, screwdrivers)
   - Wood Glue
   - Screws

1.) Install the latest Raspbian distribution to your Raspberry Pi. This has been tested on Jessie.
2.) Follow the install steps from INSTALL.txt file.  This will give you the necessary libraries.
3.) Connect the LCD and camera to the Pi and plug it in.
4.) Plug in the printer with USB connection and setup your CUPs config file by enabling port 631 and add the printer by going to      yourrpihostname:631 on your browser.

Noob Instructions:
	https://www.howtogeek.com/169679/how-to-add-a-printer-to-your-raspberry-pi-or-other-linux-computer/
	Follow the instructions there. 
	MAKE SURE you do the 
	Sudo usermod -a -G lpadmin pi 
	Command or else you won't be given access to the CUPS add a printer page with the default credentials: 
	User: pi
	Pass: raspberry
	
	To get the Raspberry pi IP address type in: ip addr
	If on WiFi find the address on WLAN. 
   In my case it was 192.168.1.70
	
	Open Chromium browser on pi and type in 192.168.1.70:631 to access CUPS main page. 

    Use the following driver file: Canon SELPHY CP900 - CUPS+Gutenprint v5.2.10.  You can verify with test page print.
    
5.) Diable Screen from going to sleep. 
Noob Instructions:

To Disable the screen going to sleep:
sudo apt-get install xscreensaver

Then go to the raspberry icon, go to preferences- screensaver. In display tab set it to DISABLE Screen saver

You can check it by running the command:
Xset q

Scroll down to Screen Saver line, that will be 0 and 0. From previosuly being 600 and 600 (10 minutes). 

From <https://www.raspberrypi.org/forums/viewtopic.php?f=91&t=57552> 

6) Download the Code. Either from here or your Repository. 
Git clone https://github.com/JGutier/boothy

7) Move the following items to your desktop
		a. QuitBoothy.sh
      b. startBoothy.sh
      
8) Copy or Move buildboothy.sh to /usr/local/src
		a. Open command line and type:
		cd boothy
		This moves from main pi directory to the boothy folder
		b. Type in sudo cp buildboothy.sh /usr/local/src
Because the directory is locked you have to access it thru the command line using that command.      

9) Run the Program.... 
Have to run it using Python 2. not 3. 3 spits out issues with prints and parenthesis. Since it lives in that locked folder (usr/local/src) you have to:
Sudo python2 /usr/local/src/boothy/pbooth.py

10) To exit, kill the program with Ctrl+C.

Being the noob that I am, my work sequence consisted of modifying the code in the main pi/boothy folder from which the initial download happened from Gihub and then deleting the code from the usr/local/src folder and copying it back in there again. Not ideal, I didn't use many of the scripts setup by Zoroloco, perhaps you know how to. So the commands I was using for that awful workflow were:
After modifying the pbooth.py text file in the /home/pi/boothy folder do this:
	1. Sudo rm -r /usr/local/src/boothy
	2. Sudo cp -r boothy/ /usr/local/src
   3. Sudo python2 /usr/local/src/boothy/pbooth.py

-----------------------------------------

Funcionality:
    Plug in the Raspberry Pi 3
    The LCD shows live video from the camera
    Press the red button
    You see countdown on the video screen
    First image taken
    Countdown again
    Second image taken
    Countdown again
    Final image taken
    Merge the 3 images to a pre-defined 4th image template
    Send new file to the printer

Image of the front:
https://drive.google.com/file/d/0B7EyXq1CH6WfVTJGTGxhYlRDTFE/view?usp=sharing

Image of the inside:
https://drive.google.com/file/d/0B7EyXq1CH6WfaVoybW5hY0thRGs/view?usp=sharing
