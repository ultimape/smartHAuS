#Initial Design Proposal - smartHAuS
intelligent **_H_** ome **_Au_** tomation **_S_** ystem


##Preamble
This is a project proposal for Nicholas Perry's Senior Project (Spring 2009).


##Design Notes: 


###Major Goal:
Develop a home automation system that is controllable via website / computer software / attached hardware. 


###Focus: 

Easy to use -> Usability of a product leads to a good user experience.

Expandable -> Flexibility improves value proposition.

Cheap Hardware -> Consumer adoptions requires low cost implementation.

Power Efficient -> Intended to run continuously.


###Intended Features: 

 * Develop a protocol that allows hooking up multiple sensor/slave/manager/interface devices in a single network. 
    - Include an easy to use network awareness setup. 
    - Device may implement multiple features, (e.g. luminosity sensor and light controller) 
    - Attempt to be as physical network agnostic as possible. 
 * Have a tiered system of permissions and adjustable automata. 
    - Different permissions for children, adults, guests, mom, dad, little bobby, etc. 
    - Assume possible extension to voice commands for hands free operation. 
 * Context sensitive options for lighting/controls based on what room you are in 
    - "lights on <room>" defaults to current room/location, as example. 
 * Highly task oriented 
    - Preset options grouped together and set to trigger under conditions. 
    - If I'm watching a movie, dim lights AND lower blinds. 
    - When there is no one in the room, turn off the lights if its the bathroom, etc. 
 * Use open standards and open api to allow other people to develop and use system. 


###Possible Features: 

 * Intelligent task management 
    - Prompt to save certain combinations of devices and also attempt to give good suggestions. 
 * Consider expansion to voice control for hands free automation. 
 * Modular design to allow different levels of commitment 
    - Add hardware as desired, automatically updates system 
    - Easy way to append modules into already established tasks. 


##Proof of concept: 

 * Develop simple controller for "room counting", and light switch manipulation. 
    - Hardware that reliably counts the number of people in a room. 
    - Must ignore pets,and perhaps count kids and adults separately. 
    - Overrides for night-time (sleep), always on mode, etc. 
    - Must consider directionality 
    - Should ignore doors 
    - Account for multiple entrances 
 * Sends count to computer, and computer sends commands to switches. 
 * computer has a website displaying current stats for each device. 
    - asynchronously with ajax? 
 * Possibly support Power-over-Ethernet for an all in one connection option. 


##Planned Direction:

I'd like to model the systems around the way that the home is used at my father's house, creating intelligence in the setup that allows for convenience on top of the typical power saving features of light control.

I have yet to get the idea of orchestrating the devices written down concisely, but I've got an example that covers the basic ideas. The project would ultimately be designed to be capable of doing something similar, and depending on how many people I can rally together, might even be presentable.

**Task:**

*Movie night.*

**Intelligence aspect:**

*Orchestrating the system allows the devices to understand what a bathroom break is, and automatically adjust itself without user intervention.*

**Having these devices:**

 - A room sensor; a device that counts how many people are in the room.
 - A light controller, which can at minimum turn on and off the light in the room.
 - A device capable of sending IR signals to a tv/dvd set-up.
 - The central computer.
 - Some interface to control it (laptop w/ web-browser connected to central computer).

**The situation would play out like this:**

 1. Tell the system that "we are starting a movie", so it knows the context of the situation.
 1. Tell the system "play".
 1. the system then records how many people are in the room.
 1. the system waits a predefined time (3...2...1...play) then turns on tv, sets volume, turns on dvd, and plays the movie.
 1. Triggers the central computer to listen for events: 
- When count of the people in the room decreases: the movie is automatically paused, the light is raised, and the volume is muted.
- When the person returns: the system resumes watching the movie after a short timeout.


##Hardware: 

Linksys NSLU2 ~$45 with shipping 

 * We're interested in using it as the central management unit for the home automation system. 
   *it runs Linux and you can control toasters with it* 
 * The linksys nslu2 is a network attached storage device. 
 * It can be flashed to become a very small form-factor Linux device. 
 * Chad Loseby has field tested it's features and has a working model of his own already hooked up to an hcs12. 
 * Once flashed, it supports USB connectivity, as well as SSH and other basic features of a *nix based host. 

URL: http://www.buy.com/retail/product.asp?sku=10361254&listingid=24695417&dcaid=17902 
   
   
xPort Direct ~$28 - ~$47 (shipping cost unknown) 

 * Serial to Ethernet 
  *"turnkey system"* 
 * Optionally 115$ for the eval kit (no hardware to build). 
 * Cheap and relatively simple way to enable serial communication over Ethernet. 
 * Multiple versions available if needs arise, from an on-board web configuration, to a complete wifi package. 
 * Going with the cheapest model because all that extra stuff isn't necessary (but nice). 
 
URL:  http://www.gridconnect.com/xportdirect.html 

  
##Discussion:
It definitely is an ambitious project, but at the same time it's features are naturally modular. I figure the first week or two will be lots of brainstorming on design goals, then how the devices should communicate. But once that is out of the way, the main hub and the external devices should be able to develop independently. 

From looking into home automation systems, there seems to be a lot of technologies that are really good at doing one thing. I'd like to focus on creating novel uses of these systems by orchestrating them through the central hub. Making decisions on data necessitates a reasonably capable computer along with a good deal of data to base those decisions on. 

I've thought about using the system as a data logger. Once everything is hooked together, it would be relatively trivial to log the data as it feeds into the NSLU2. We worked with a temperature sensor with data logging capabilities in Micro II, this would be a logical next step in that project.

I'd rather not get into the nitty gritty of the connectivity. If I had someone interested, it would possible to make a simple bridge device. But for the most part, I'd like to stick with serial and Ethernet, Its cheap and simple and allows the project to focus more on getting things done.

Using Ethernet allows the integration of the computer (along with the devices) on a high bandwidth system. Lots of homes have Ethernet already, so I see it as a viable starting point for the network. Making the system wireless is trivial, as there is a drop in module that replaces the serial over Ethernet with a serial over 802.11 etc.

I've looked into a few of the major names in home monitoring systems, (basically anybody who is actually selling a serious product.)  X10 and INSTEon seem to be the dominating devices in the marketplace. They both use the power lines in the home to send data, with the INSTEON system using them in conjunction with wireless signals to get around certain hurdles. Insteon supports 16bytes per second, and x10 is only a fraction of that.

##Initial Name ideas:

smartHAS - Intelligent Home Automation System 

smart Hauss (kinda like "smart ass") 

Origin: "smarthas" (pronounced with a "th" as in "the") is a Hindu philosophy of the connected and oneness of what might otherwise be separate deities. This approaches the idea of connecting separate systems into a more powerful and intelligent "being".






   

