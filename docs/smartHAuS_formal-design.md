#Formal Design Proposal - smartHAuS
intelligent **_H_** ome **_Au_** tomation **_S_** ystem


##Preamble
This is the formal design for the VTC Senior Project known as smartHAuS (Spring 2009).


##Introduction 

For our senior project, we intend to develop a rudimentary home automation system. Our smartHAS, henceforth known as "the system", will incorporate a central "brain", as well as a multitude of satellite devices connected to it. Each device extends the system with added functionality in the form of either sensors, or manipulators. 
  
The main focus of the project will be on the complex interactions of these devices as orchestrated through the brain. It shall be the brain's responsibility to enable intelligent interoperability between devices. This allows the user to combine device features in interesting and novel ways. The brain should also provide a complete access solution for the system, allowing the user to administer and manage the connected devices, as-well-as set up customized actions for their particular uses. 
  
With this in mind, the devices we will create shall provide the system with highly practical sensor data. Deceives should focus on "what can it do for you?". A light sensor, for instance, can enable a multitude of other features when connected up to the brain. At bear minimum a light sensor would allow the brain to be aware of daylight and thus account for different user habits that occur after dark. Likewise, manipulators should provide features that integrate well with the sensors, perhaps a pneumatic door lock for automatically securing the house after dark. 
  
This system covers a unique niche in the home automation market. For most automation systems, central control is an after-thought, and interoperability of devices is rudimentary at best. There has been plenty of research in the development of network design, and tons of development in individual devices and simplistic remote control systems. However in our system, central control and interoperability is the primary goal. We are trying to show how incorporating a "brain" allows us to create useful and convenient setups with a small amount of devices. 

In summary: Most systems can "control the kitchen sink". Ours will "know" what a kitchen sink is, and go a step further: it will turn the sink on when your hands are dirty. 


##Functional Requirements. 


###The "Brain" 

 * Communicate with devices over a LAN using the icanHAS protocol. 
 * Look up individual devices connected to the system. 
 * Manage security settings 
 * Manipulate connected devices 
 * Set up triggering for sequencing device commands - "tasks" 
  - Timers 
  - Connected Sensor States 
  - Other triggers 
 * The ability to schedule tasks. 
 * Allow the user to setup up tags for grouping devices. 
 * Web based interface 

 
###Communication Protocol 

"icanHAS" = Interface for Connecting Atypical Nodes to Home Automation System 
  
 * Two way protocol 
 * Indicate features and capabilities of device 
 * Note types of data sent: scalar, text, percent, and on-off signals etc 
 * Transmit command signals to control devices 
 * Transmit query signals to access device's sensors 
 * Transmit emergency shutoff signals that over-ride default operation. 
 * Syncing capabilities for security 


###Satellite Devices

Implement a minimum of two devices, once sensor and one manipulator. 

Make them compatible with the icanHAS protocol/network. 

Transmit enough information to allow a simple level of orchestration from the brain 


###User-Interface

The web based interface should be accessible on firefox, and other conforming web browsers. It should provide convenient ways to instruct the brain on it's actions. It will have a tagging system to provide a more natural way to reference devices "indoor living-room lights". And it will provide a script like psudo-language to set up triggering of command sequences. 


##Non-Functional Requirements


###Security

Since the nature of this system is to deal with devices in a personal home, security is a high priority. To ensure the security of the system, there will be a large set of features for setting up your web interface. Some of these features will involve the features you would find on an everyday home router. For instance, remote access, user name and password, port and IP specification, and password encryption. Each device will also need to go through a syncing phase, and will not be accessible until the syncing is finished. The system should allow for multiple users with separate permission levels, this way children can have access to the control panel without being able to break things.


###Performance

The performance of the system is purely based on the latency that could occur between the "brain" and the peripheral device. We do not envision this being a problem since the network will be standard 10/100BaseT Ethernet setup. 

Depending on the throughput required, certain types of data (music, video) may need to be sent in alternate protocols on a per-device basis. This might be cut due to time.


###Easy of Use 

The smartHAS system will be void of most confusing hardware hookups required with a home automation system. The devices should be "plug 'n play", with very little user required configuration. The user interface will also be fairly simplistic in its use and at most require reading short documentation to get the system functional.


###User Characteristics

This device will appeal to home owners who want to quickly and easily automate mundane tasks. It will also appeal to home users who want a tasked oriented system that will make there lifestyle more efficient.


###Scale

The system should be easily expandable. Either by upgrading "Brain" hardware, or using multiple brains to keep track of the system.

Since the smartHAS system implements the icanHAS protocol and any manufacture can create peripherals for the smartHAS system.


###Internationalization 

No, this is a prototype and this would force a significant amount of overhead to get it working across language barriers. 


###Environment

The system is intended to be used in and around the home. The "brain", being a computer, will require a relatively dry area, and it must have enough ventilation to cool the device passively.

Most devices we envision as indoor devices, so they will require very little environmental proofing. Having open circuit boards would be the biggest thing to avoid, since animals and humans like to touch them.
 
Some devices may used outdoors, they will need to be appropriately weather-proofed, possibly in a sealed box and a coax based connection to the network. 

The system will require pre-established Ethernet Networks, otherwise it would become expensive to implement. 


###Expected Enhancements

The biggest enhancement would be the addition of other devices to the system to demonstrate the ease of expandability. By having 3 or more devices, the intelligence of the system should be demonstrate-able further.

It might also be feasible to hook up other group's systems to the brain and allow them as sensor sources, or unique control systems. There was mention of an mp3 player, which would enable the system to create mood music, for example. 

