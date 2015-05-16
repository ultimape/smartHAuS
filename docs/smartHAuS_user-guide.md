#User Manual - smartHAuS
intelligent **_H_** ome **_Au_** tomation **_S_** ystem


##Preamble
This is a user manual/guide to the VTC Senior Project known as smartHAuS (Spring 2009).


----

Table Of Contents 
  
  
General Information 

&nbsp;&nbsp;&nbsp;&nbsp;System Overview 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;What is smartHAuS? 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Intelligence? 


System Summary 

&nbsp;&nbsp;&nbsp;&nbsp;Data Flows 


Getting Started 


Quick Start 


Advance/Technical Information 

&nbsp;&nbsp;&nbsp;&nbsp;the icanHAS protocol 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;The Protocol Basics 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Other Responses

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Initial icanHAS device connection 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Example of Types 

&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;icanHAS Protocol Example
 

Reference 

&nbsp;&nbsp;&nbsp;&nbsp;Products 

&nbsp;&nbsp;&nbsp;&nbsp;Guides 

##General Information 
###System Overview 
####What is smartHAuS? 
smartHAuS is a H.ome Au.tomation S.ystem developed as part of the "Senior Project" course offered at Vermont Technical College. Senior Project is a cumulative course intended to have seniors "demonstrate their mastery of the subjects covered in their program".

A basic set-up would consist of "the brain" (the central system controller), an Ethernet based network, and various devices connected to this network. Typically these devices will be small, low powered, micro-controllers all hooked up via a serial-to-Ethernet dongle. However any device that can communicate over ethernet is a potential smartHAuS device.

The system has basic features of a home automation system; it receives input from connected devices' sensors, and performs some automated task via a connected device's actuators.

 We have created a couple devices to show off connectivity. But for the most part, the actual implementation of the device(s) is left to the user.  smartHAuS is more to demonstrate connectivity features than actual hardware.  

We have coined the project smartHAuS because it is an "intelligent home automation system". The main premise behind the project was to develop it in such away that it was "aware" of the devices and gave it the ability to reconfigure itself as devices are added and removed. By doing so, convenience can be baked into the system by creating simple but powerful connections between inputs and outputs. 

----

####Intelligence? 
The "intelligence" is a side effect of two features in the project and it emerges out of the system because of an inherent semantic relationship between the two.

The first feature is the protocol: dubbed the "Interface for Connecting Atypical Nodes to Home Automation System" protocol, or simply icanHAS.  All devices in the system communicate on this protocol.  It is text based and allows devices to transmit what they are capable of.  Devices can say things like "ican:turn_on, ican:turn_off, ican:get_temperature_in_celsius",  which informs the brain what options you can send it.

By giving devices knowledge about themselves, and allowing the brain to receive this knowledge, we are essentially allowing the brain to "learn" about connected devices.  It may not exactly know that "turn_on" turns on the device, but it doesn't have to know what it does, only that it can.

The other feature that allows for a sense of intelligence is a tagging system for devices.  We've implemented a tagging system that allows users to "tag" devices with specific identifiers.  For example, you may want to tag a device "light, living room, overhead", and another device "light, kitchen, sink".

This lets the user refer to devices by tags instead of individually.  You can instruct the brain to "turn_on" all "kitchen light",  or when  a light sensor returns +50, "turn_off" all "light".  The brain is smart enough to handle the actual sending of messages to any connected device that matched those tags.

With these two systems in place, it becomes trivial to hook up another device to the system.  For most devices its a matter of simply: 

1.     Plug in to the network. 
2.     Authorize it in the brain 
3.     Tag it based on where it is or what it is. 
    
Nothing else needs be done because all the scripts referring to applicable tags will automatically adjust to account for your device. 
smartHAuS does the thinking for you! 

----

##System Summary 
###Data Flows 
Behind the web-interface is the device manager. The manager handles connection to available devices and the sending/receiving of signals using the icanHAS protocol. Initially everything runs through the Authenticator, which will wait until the user "authorizes" the device. Then it dumps the device facilities to the database, logs the authentication, and lets the device know that its OK to start doing its function(s).  

During authorization, the user can set up access levels for the device and override it for individual features. Signals from the authenticated devices are sent to the Scripter which the user can configure and send commands to operate the devices. There are some basic scripts that just log the data for the user. The system also has auto-generated scripts for each output that the user can run on command. Inputs and outputs are queued, and are sent as soon as the system is ready.

![alt text][devicemang]



[devicemang]: ./images/devicemang.png "Device Management Flow"

----

##Getting Started 
At this time, the system is not readily installed, as it is in the prototyping stage.  We hope to eventually have a simple installer for the brain software.  Devices should be plug-and-play as design.

For creating your own devices, please see section 5.1 to learn more about interfacing with the icanHAS protocol.

##Quick Start 
On a working system* simply plug in an icanHAS compatible device, login into the brain, and navigate to the management page. Once there, you should be prompted to authenticate the device with your system. If the authentication dialog does not pop up, you can choose to "find new devices", (this will run a device detection routine).

After the device has been authenticated, it will be usable in any of the other sections (scripting, tagging, etc).  The first thing you may want to do is to set up permissions for whatever features the device provides since the defaults are rather restrictive.

\* a working system would involve having a webserver properly configured to serve up the smartHAuS front-end.  At this time no help information is availible for the install process, as the system is not in a production state.

----

##Advance/Technical Information 
####the icanHAS protocol 
A major feature of smartHAuS is that the protocol is a simple open standard.  Any device that can be made to communicate the protocol will be able to interface with smartHAuS's brain. 

####The Protocol Basics 

The protocol can be broken down into 3 basic communication elements.  Each element consists of an identifier, an action token, and any message contents.  Individual messages are denoted as "finished" when a single newline character is transmitted.

* Identifiers are used to denote what the message is referring to. 
  * May not contain spaces unless it is wrapped in double quotes. 
* Action tokens are like verbs, they denotes what the message is trying to do.   
  * '?', denotes query'ing 
      * this is used when a device/brain wants to know something. 
  * ':', denotes responding (listing?) 
      * this is a generic response method, and can be used for assigning values. 
  * '!', denotes exlaiming 
      * this is used to let the listening device know that there is nothing else left to say when a response might span multiple messages. 
      * if the device is not in a long message, this can be used to push notifications that weren't asked for.  
* Message contents are double quoted strings, with their format pre-specified during the initial set up of the device-brain connection. 

####Other Responses

OK:"message" responses are sent to ensure that messages are properly transmitted. If this fact can be inferred by other content, they are optional. 

REMARK:"error_level;reason;message" usually indicates that the message was unexpected or malformed for some reason.  Errors are most likely due to a misconfiguration of the device's initial setup.  Messages of these type may be alerted to the user, and can be sent from a device as well as the brain.

The error_level can be one of the following: 

* FATAL - unrecorverable error, these will be alerted to the user upon log-in. 
* ERROR - a problem exists, and should be fixed. 
* WARNING - not an error per-se, but should be taken a look at. 
* NOTE - Things like battery life or other interesting information that is relevant to the health of the device 
* INFO - any statistical information and other communication not previously mentioned. 
* DEBUG,DEBUG1,DEBUG2 - Debugging information for troubleshooting the development of a device. 

Please note that while the brain may understand carriage returns, they are not considered part of the protocol and will typically be dropped.  Also, messages containing newlines should have that character broken out in a standard c like fashion.  Anything not inside a double quote should be made case-insensitive, defaulting to all upper-case to make it stand out.

####Initial icanHAS device connection 
First, all devices must be capable of responding (on port 10,001) to the query:

    icanHAS?
    
with the response of: 

    icanHAS:"cheeseburger" 
    
and they may be prompted with this query at nearly any time they aren't in the middle of another conversation. This is necessary for the dynamic nature of IP based networks, and allows the brain to distinguish between icanHAS capable devices and other unrelated machines.

Upon connection of devices, the brain will ask the device for more information.  During this query, the device will either respond with it's U.nique ID.entifier, or with a UID of "0".

If the UID is non-zero, the device is considered to be simply reconnected and operations should proceed as normal.  This may happen if the device is turned off, or the brain loses connection with the device due to network issues.
    
On a UID of "0" however, the brain considers it a new device, and will assigns a UID. Further, the brain asks the device for more information about itself.  The device should respond with it's name (or rather, what it thinks it is), a description, and a set of inputs and outputs.  See section 5.1.4 to read an example of this type of connection. 

Each input/output also should have a name and a description.  Further, they should include information about the input/output's capabilities. The more specific a device's input/output is described, the more the brain is capable of doing with the data.   For instance, by declaring an output as pre-specified, the brain will present the user with a drop down box of the choices, instead of an arbitrary text box.  

----

####Example of Types 
Below is an example of what types the brain is capable of recognizing.   
	
    Device: 
        Name: "Example" 
        Description: "A hybrid device built by soraplex industries" 
        Inputs:  
            ID: "1" 
                Name: "Temperature" 
                Description: "A simple temperature sensor" 
                Type: "Scalar, floating point" 
                Range: "-100 to +120" 
                Units: "c" 
            ID: "2" 
                Name: "Room Count" 
                Description: "A simple room counter" 
                Type: "Scalar, integer" 
                Range: "0 to unbounded" 
                Units: "people" 
            ID: "3" 
                Description: "Status" 
                Type: "String, pre-specified" 
                Responses: "'off' 'on' 'disabled' 'delayed'" 
            ID: "4" 
                Description: "User PIN" 
                Type: "String, unspecified-short" 
                length: "30" 
            ID: "5" 
                Description: "Misc User Commands" 
                Type: "String, unspecified-long" 
                length: "30" 
                EOT symbol: "<FIN>" 
        Outputs: 
            ID: "1" 
                Description: "Light Control" 
                Type: "String, pre-specified" 
                Signals: "'off' 'on'" 
      

----

#### icanHAS Protocol Example 

    SEQ# BRAIN                        DEVICE 
    ---  ----------                   ----------
    x)   icanHAS?                     icanHAS:"cheeseburger"\n
    
    1)   Device?\n                    Name:"device name"\n
    2)   OK:"device name"\n
    3)                                UID:"0"\n
    4)   OK:"0"\n 
    
                    If UID == 0
    5)   UID:"10"\n                   OK:"10"\n 
    
    6)   Inputs?\n                    ID:"1"\n
    7)   OK:"1"\n
    8)                                Name:"Temperature"\n
    9)   OK:"Temperature"\n
                       (etc)
    23)                               ID!"1"\n
    24)  OK:"1"\n
                   (maybe more ID's)
    30)                               Inputs!\n
    31)  OK! 
    
                    If UID =/= 0 
    1)   OK!
             (nothing; device is reconnected) 
    
                    Querying Input
    1)   Input?"1"                    "1":"50"\n
    
                    Specifying Output
    1)   "1":"on"                     OK:"on"


In future versions of the protocol we will be specifying required inputs thoroughly (things like mandatory soft-resets etc). Standardizing these things will allow brain scripts can be written in a generic fashion. 

----

##Reference 
###Products 

- Arduino:
    http://www.adafruit.com/index.php?main_page=product_info&cPath=17&products_id=50 

- Adafruit Ethernet Sheild for Arduino:
    http://www.adafruit.com/index.php?main_page=product_info&cPath=17&products_id=83

- XPort Direct: 
    http://www.gridconnect.com/xportdirect.html 
- Eee PC 1000: 
    http://www.newegg.com/Product/Product.aspx?Item=N82E16834220368 
  
###Guides 
- Arduino Guide:
    http://arduino.cc/en/Guide/HomePage





