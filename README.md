# Go go Octopi!

##...Installing Octopi for the mere mortal

*Warning: This is certainly a work in progress. Please feel free to open issues (or issue a PR) if there is something wrong with the content*

The process a little bit fiddly but **you can do it!** After all, pretty much everyone getting into 3D printing has be prepared for getting into the fiddly bits every now and then.

From a hardware perspective, all you need is a pi 3B+, a micro SD-card (Which will come with an adapter so that you can use it with your existing SD card reader), a USB printer cable (USB-A Male to USB-B Male), a micro-USB cable (like an android phone charger) and a USB brick to plug it into the wall (At least 1AMP output).

Hardware List

- Pi
The 3B+ has built-in wifi and is pretty snappy (for a small little computer)<br>
[Amazon Link](https://smile.amazon.com/Raspberry-Pi-RASPBERRYPI3-MODB-1GB-Model-Motherboard/dp/B01CD5VC92/ref=sr_1_7?s=electronics&ie=UTF8&qid=1532567506&sr=1-7&keywords=raspberry+pi+3+b%2B#customerReviews)

- Micro-SD Card
Lots of options here..cheaper and smaller and slower, bigger and faster and more expensive, or even better one that you already have...make sure you get one with an adapter unless you have a micro reader<br>
[Amazon Link](https://smile.amazon.com/Samsung-MicroSDXC-Memory-Adapter-MB-MC64GA/dp/B06XFWPXYD/ref=sr_1_8?s=electronics&ie=UTF8&qid=1532567603&sr=1-8&keywords=micro+sd+card)

- USB Printer Cable<br>
[Amazon Link](https://smile.amazon.com/AmazonBasics-USB-2-0-Cable-Male/dp/B00NH11KIK/ref=sr_1_4?s=pc&ie=UTF8&qid=1532567277&sr=1-4&keywords=usb+printer+cable)

- Micro USB Cable and Charger<br>
Just use a phone charger you have lying around. If you need to buy another brick make sure it is at least 1AMP.

### Software

OK, whew....thats all the hardware out of the way. Now for the software, which is thankfully all free. 

- Install [Etcher](https://etcher.io/) to image the SD card.<br>

- Install a decent text editor ([Atom](https://atom.io/), [VSCode](https://code.visualstudio.com/), emacs, vim, etc.)<br>
If you use the builtin editor on Windows (Notepad) or the Mac (TextEdit) you will break stuff.<br>

- Download the latest version of [Octopi](https://octoprint.org/download/). This will be a zip file.

- If you are on Windows you will need an ssh client ([Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/)). If you are on a Mac this is already available via the Terminal application.<br>


To image the card, put it in your reader. Then...

1. Open Etcher
2. Drag the octopi zip file you downloaded on to etcher and click the "go" (or maybe "etch") button. 
3. After the image is done being written to the disk, you should be able to browse the memory card (Using Explorer on Windows or Finder on Mac) and it will have a boot folder. Open up that folder.
4. Edit the file in the folder called "octopi-wpa-supplicant.txt" using the Atom text editor (Warning: using Notepad or TextEdit will break this step) we downloaded and installed above.
5. Find the WPA2 configuration section in the file and change the SSID and Passphrase to match your Wifi-Network and password.
6. Save the file, close the editor, eject the card, and put it in the Pi. 


### Putting it all together

Ok, home stretch....

- Plug the USB Printer Cable into the Pi and the Printer.
- Plug the brick with the micro USB cable into power.
- Plug the micro USB into the Pi
  - You should get a red light right next to where you just plugged in the power
- Give it 2-3 minutes to boot up and connect to the network

Now we get to find out if we did everything correctly. 

##### We need to connect to the Pi's CLI 

*Note: You will rarely, if ever, have to do this again*

If you are on Windows open the Putty ssh client we downloaded and installed above. Add a new server to connect to and use the hostname `octopi.local` and set the username to `pi` and the password to `raspberry`. Click connect and accept any warnings that pop up about the certificate.

If you are on a Mac open the Terminal application. At the prompt type `ssh pi@octopi.local`. Accept the certificate warning. When you are prompted for a password enter `raspberry`.

If you made it here you are home free now. The wifi connection tends to be the part that flakes out on folks. If you cannot connect: unplug the Pi, pop-out the card. Put it back in your PC and go edit that file again (using the good text editor) and double check your SSID and Passphrase does not have any typos. 

You should see something similar to this come up:

```
The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
Individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Last login: Thu Jun 14 23:25:14 2018 from 192.168.1.26

------------------------------------------------------------------------------
Access OctoPrint from a web browser on your network by navigating to any of:

    http://octopi.local
    http://192.168.1.4

https is also available, with a self-signed certificate.
------------------------------------------------------------------------------
This image comes without a desktop environment installed because it's not
required for running OctoPrint. If you want a desktop environment you can
install it via

    sudo /home/pi/scripts/install-desktop
------------------------------------------------------------------------------
OctoPrint version : 1.3.9rc1
OctoPi version    : 0.14.0
------------------------------------------------------------------------------

pi@octopi:~ $
```

OK, we are now at the command line for the Raspberry Pi.

- Lets change the password<br>
  Type the command `passwd`. It will prompt you to enter your password which is `raspberry`. Change it to a good password, you'll have to type it in twice.
- Now lets tell the Pi to use the whole memory card instead of just the minimal image size. Type the command `sudo raspi-config`. This should bring up a text menu.
  - Select `Advanced Options`
  - Select `Expand Filesystem`. You should get a message saying something about the file system expanding after your next boot.
- Reboot the Pi by typing the command `sudo reboot`

Now your Pi is rebooting and you should lose your connection. Give it a couple of minutes to reboot and connect to the network.

<center>

#You did it!

</center>

Now browse to <http://octopi.local>. Octopi ships with a self signed certificate, so you will have to accept that. 

Here are some key resources:

- [Octopi download and install info](https://octoprint.org/download/)
  - Thomas Salander's video linked on this page can be enlightening, but it is definitely out of date on some of the steps and he uses an older Pi that does not have Wi-fi built in. Still a valuable resource though.
- [Octopi Github](https://github.com/guysoft/OctoPi#how-to-use-it)
  - The actual Octoprint Github repository with some terse "How-to" info on the first page...and some other useful links.
- [Raspberry Pi Install](https://www.raspberrypi.org/documentation/installation/installing-images/README.md)
  - This is the primary source for imaging the SD card.


