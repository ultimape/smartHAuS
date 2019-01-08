# Device Ideas - smartHAuS
intelligent **_H_** ome **_Au_** tomation **_S_** ystem


## Preamble

This is a list of potential devices for the VTC Senior Project known as smartHAuS (Spring 2009).


## Device Ideas & Other misc features.

In this file, list off ideas and notes on things that \*Could\* be hooked up to the system.  This way we can compile them together and develop a communication protocol that allows a significant portion to be possible.


### Light control device

Using:

 * Hcs12
 * Serial -> ethernet converter.
 * Relay

I've got a remote controlled power relay that can shut off lights.

It'll take a bit to rip the thing apart, but should be easy enough to integrate.


### Door/Room counter

Using:

 * Hcs12
 * Serial -> ethernet converter.
 * Sensor http://www.radioshack.com/sm-matched-infrared-emitter-and-phototransistor-detector--pi-2049723.html

I've got some parts from radio shack to build a simple infra-red sensor.

The idea is to count how many people are in a room by keeping track of movement through doorways.

The device will allow the system to be aware of people's position, but in an anonymous way.


### Infrared Remote Control Emulator

Using:

 * Hcs12
 * Serial -> Ethernet converter
 * IR transmitter: http://www.smarthome.com/83613/Channel-Vision-Single-IR-Emitter-IR-3001/p.aspx

Wire up so that a pre-recorded ir signals can be sent through it.

Alternatively, get one that hooks up to a laptop just to get a demonstration of connectivity.


### Ambient Light Sensor

Using:

 * Hcs12
 * Serial -> Ethernet converter.
 * Photo-resistor

Have a device that allows for the system to detect light levels.


### MP3 player / mood music

Using:

 * Whatever the other Senior Project group makes.
 * http://www.vlsi.fi/en/products/vs1053.html

Be able to stream an mp3 from the NSLU2's attached harddrive.

Depends on how they set it up.

Might just make a simple streaming protocol with vlc or some such, and demo it with a pc attached to the system.


### Ambient Temperature Sensor

Using:

 * Hcs12
 * Serial -> ethernet converter.
 * Temperature sensor

Have a device that allows for the system to detect temperature levels and report them.


### Ambient Humidity Sensor

Using:

 * Hcs12
 * Serial -> ethernet converter.
 * Temperature sensor

Have a device that allows for the system to detect temperature levels and report them.


### Fan Controller

Using:

 * Hcs12
 * Serial -> Ethernet converter.
 * Larger fan (box fan?)

Be able to turn on/adjust fan speed.

Links well with temperature sensor.

Could be used to lower fan noise when sleeping/ watching movie etc.

Have different settings when people are in the room w/ preference of comfort vs noise.


### Video Camera

Using:

 * Laptop
 * Webcam

Connect/disconnect/record on commands from system.  Potentially multiple to display "room" sensing capabilities.


### Remote Conferencing

Allow people to communicate with others through the house without having to "yell".

Use server and room sensor to initiate hook up/notify when someone is in the room.

Would need to send audio data somehow, could be demonstrated with a laptop/computer set up.


### Window Shades

Keep dark room dark, and cool rooms cool.


### Noise Detector

Clap-on?

Interface with Voice Recognition - advanced feature.

Butler, turn on my tv... thank you butler.

Butler, dim the lights by 30%, shut down computer, play music sexy... thank you butler.


### IR sensor

Use to 'train' commands, as well as to control system.


### Connect to internet to get info:

Time, date, weather, sunrise/set, Google calendar events, etc.

