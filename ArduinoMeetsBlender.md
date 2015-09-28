# Arduino Meets Blender #
<pre>
by Chris B Stones<br>
January 13, 2010<br>
http://welcometochrisworld.com<br>
<br>
This project demonstrates how to use the Arduino to<br>
control items in Blenders Game Engine via the OSC protocol.<br>
It was initially created for real time digital puppetry.<br>
But it can be used as a starting example for any project that needs<br>
to communicate with Blender's GameEngine via the OSC (Open Sound Control) protocol.<br>
<br>
Since it uses the OSC protocol this project also demonstrates<br>
how any OSC enabled app can send data to the Blender GameEngine.<br>
</pre>

## REQUIREMENTS ##
<pre>
oscP5 library by Andreas Schlegel (included)<br>
http://www.sojamo.de/libraries/oscP5/index.html<br>
<br>
Python SimpleOSC  (included)<br>
SimpleOSC is a simple API for the Open Sound Control for Python<br>
by Daniel Holth, Clinton McChesney<br>
<br>
You'll need the Arduino IDE, Processing IDE and Blender to<br>
run this project.<br>
<br>
You will also need an Arduino board, 3 wires, a potentiometer, breadboard and a USB cable.<br>
</pre>
## PROCESS ##

### 1 Hardware ###
<pre>
Basically, one Arduino and one 3 pin potentiometer, 3 wires and the USB<br>
cord make up the demo circuit. The middle pin of the potentiometer<br>
the middle pin is wired to the Analog 3 INPUT pin of the Arduino.<br>
The outside pins are wired to 5 Volt and GND.<br>
Values you read from this pin will return the full range of levels.<br>
( 0 to 1023, 0 to 5 Volts)<br>
<br>
You'll have to hook up the Arduino and select the proper Arduino device<br>
name. On Mac OS X you can find that in /dev/ looking for something like<br>
"/dev/tty.usbserial-A7006Rjr" after you connect the Arduino up.<br>
You'll need to hard code that into the processing sketch so take note.<br>
<br>
Upload the code from arduino_code/ folder to the board.<br>
</pre>
### 2 Processing ###
<pre>
You need to install the oscP5 by andreas schlegel<br>
(http://www.sojamo.de/oscP5) in processing.<br>
You go into the Processing App (Right click Show Package Contents)<br>
It's in Contents/Resources/Java/libraries.<br>
Place the oscP5 folder in there, restart processing.<br>
You should be able to import oscP5.*;<br>
<br>
Change the line in oscarduino.pde to match your Arduino dev file.<br>
String portname = "/dev/WHATEVER_YOUR_SERIAL_DEVICE_NAME";  You can<br>
find out what it is by opening Terminal.app and cd /dev then ls and search<br>
for something that starts with tty.YattaYatta<br>
<br>
Note the varibles TO_PORT and FROM_PORT in the oscarduino.pde file.<br>
The Blender code is going to be listening on a PORT. PORT should match<br>
the TO_PORT varible in the processing sketch.<br>
<br>
You'll also need to change HOST varible to match your localhost.<br>
You can open the Terminal.app and type in ifconfig to find that information.<br>
It should be up near the top around eth0. Goto System Preferences and then to Network.<br>
This will also show you the IP Address of your local computer.<br>
</pre>

### 3 Blender ###
<pre>
This demo was created with Blender 2.49b on a Mac OS X 10.6 Intel Machine.<br>
Inside of the blender_code/ folder you'll find a demo blend file.<br>
It should have the file arduino_to_blender.py already loaded inside.<br>
In tha text file you will need to match the PORT to the TO_PORT from<br>
the processing sketch.<br>
<br>
The OSC SimpleOSC python module is in the same directory as the .blend file so you shouldn't<br>
have to install it inside blender. It's recommened that you install OSC in blender (place inside scripts/)<br>
or open all the files from blender_code/OSC into the blend file if you wish to make your blend file<br>
portable or standalone later.<br>
</pre>
You'll need to adjust:
```
# Check that you don't have a firewall blocking ports on your computer
# Must match part Processing is sending OSC message with
PORT = 2014  # ;) 

# Most be set to same IP as localhost
HOST = "10.0.0.3"
```
in the arduino\_to\_blender.py text file.

### 4 Test Run ###
<pre>
Once all that is done you should be able to run the processing example<br>
and then Press P in Blender's View3D window to run the example in the<br>
GameEngine.<br>
<br>
Try turning the control knob. You should see the gauge move.<br>
</pre>
## DEVELOPMENT NOTES ##
<pre>
Try using higher port numbers if the project doesn't work.<br>
And make sure you don't have any firewall blocking ports.<br>
Also check the HOST matches your localhost IP.<br>
<br>
The processing sketch has a test mode in case you suspect somethings<br>
wrong with your Arduino. Set TEST = true; if you want to test send<br>
data to Blender by moving the mouse in your sketch.<br>
</pre>

## REFERENCES ##
Blender Game Logic
http://www.blender.org/documentation/pydoc_gameengine/PyDoc-Gameengine-2.34/index.html