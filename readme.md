# Welcome to the Bama Racing Computer Science & Electrical GitHub
### Last Updated: Summer 2021

This document will discuss the Bama Racing HUD, its capabilities, areas for expansion, and some skills (or interests) needed to continue work. 

# Table of Contents
* [Team Members](#team-members)
  * Test  
* [Recommended Skills, Languages & Tools](#Recommended-Skills,-Languages-&-Tools)
* [Software](#Software)
* [Hardware](#Hardware)


# Team Members
* Nathan Eads
* Emma Goldthorpe
* John Yordy
* Brendan Kuhlmann 

# External Documentation
* SAE Rule Book 
* W3 Schools HTML
* W3 Schools CSS
* Other Speedometer 

# Brief System Overview
### The HUD
The HUD is Electrical's show pony. It is currently comprised of a Raspberry Pi 3B connected to a touch screen display and two Hall Effect Sensors. These Hall Effect sensors are able to detect magnetic fields. By placngin 
























# Hardware
### The HUD 
The HUD is currently comprised of three major PCBs and one tertiary power distribution PCB (I know that might sound scary, just stick with me). 

The firmware in repositories under this Organization is run off of the main PCB, a Raspberry Pi 3B+ (RasPi). 

The RasPi is then connected to two Hall Effect Sensors. These sensors have a binary digital output dependent on their proximity to magnetic fields. If you are unfamilair with Arduinos and RasPis, binary digital output just means that the sensor can vary the voltage coming out of its signal pin. When there is a magnetic field detected, the voltage will be set to 3.3V. When there is no magnetic field detected, the signal output pin is set to 0V. 

We can then monitor this voltage using the RasPi so when the Hall Effect Sensors detect a magnetic field, the firmware will begin to calculate speed or RPM respectively. 

### Other Electrical Systems 
##### Kill Switches
Kill switches are mandated by SAE and are expected to halt the engine when they are pushed. 

The kill switches work by shorting out the low-voltage end of the alternator's transformer. A car produces it's electricity using an alternator; the alternator sits on the engine and turns the motion of the shafts into electrical power. This electricity is then put into a transformer which provides adequate voltage/current to the sparkplug. 

By shorting this transformer, we can halt the spark plugs from firing, thus killing the engine. 

##### Brakelight 
The brakelight is also required by SAE. 

There are two brakelight sensors integrated into the brakeline. When the brake is pushed, the pressure in the brakeline causes these switches to close an electrical circuit. 

By connecting these sensors in parallel and then in series with a pair of 9V batteries in parallel, and assuming the brakes team did their job correctly, both brake lines should trigger the brake light. **You should test to make sure that both brake lines trigger the light by disconnecting one sensor at a time and pressing the brake pedal.**

##### Headlights
Some of our cars run headlights, they are not required, but what do rednecks love more than light bars? 

This circuit is pretty easy, just a batter, the light itself, and a switch to control it. 

### 3D Printing 
I base a lot of my work around 3D printing. It's very fast, if I plan my day well, I can go through 10 - 15 iterations of a design per day, compared to a teammate who might go through a similar number in a year. 

If you pick the right filament, and the right settings, you can produce some solid results, but you are limited to the durability of plastics. If you are not comfortable learning to use the printer in the office on your own, please reach out to me (Nathan Eads) (I'm the one who donated it). If you do not want to learn how to use a printer and would just prefer to have your models produced for you, consider reaching out to the Cube. This will take longer, but will still be beneficial. 

Even if you learn to use the printer in the office, it might be wise to setup an account with the Cube. Sometimes you will be busy. Sometimes, you just need something made for you.

### Waterproofing 
The kill switches, brakelight, and headlights do not need to be waterproofed. 

Any housing for the HUD will need to be waterproofed. I recommend window sealant and hotglue.

For 3D printed parts, please note that layer lines will leak under prolonged exposure. To compensate for this, maximizing the layer height (therby minimizing the number of layers, and thus the number of gaps between layers) will reduce potential leak points. 

# Recommended Skills, Languages & Tools

This section will discuss my workflow and the skills being used in the current build of the Bama Racing HUD. No proficiency is required in the following areas, but I would recommend at least being interested - Baja should be fun!

### Software
##### GitHub/Atom 
Clearly, I use GitHub. This ecosystem makes it really easy to write and test code.

Atom is a code editor made by GitHub; by linking your GitHub account, and using GitHub Desktop, you can open a repository in Atom and then directly upload any changes you make to GitHub. Then, you can pull these changes to the RasPi with just one command. 

##### CAD 
For 3D modeling, I prefer SolidWorks and all of my models are .SLDPRT or .SLDASM. 

If you are new to CAD, SolidWorks is a great starting point, there are a ton of tutorials on YouTube and most of your teammates are proficient and are happy to answer questions or point you to some good resources. 

Note that all of my files are in metric (millimeters). This is the standard unit for 3D printing, a tool I base much of my workflow around. I recommend using millimeters to keep things consistent for your future successors (sorry), but I will leave this to your discretion. 

### Hardware/Fabrication Skills
* Soldering 
* 3D Printing (FDM/FFF)
* Laser Cutting (just 3D printing in 2D)

### Programming 
This is where things might get a little daunting. 

When you run the HUD, you will run a Python3 script (make sure you run it with a virtual environment running Python 3.7 or later). 

This Python file contains all the math for the HUD as well as all of the interrupts for the Hall Effect Sensors. 
* Interrupts are a type of listener function, in our case, they are attatched to the digital out pins of the Hall Effect Sensors.
* When the pin on the RasPi detects a change in voltage, a function is called to begin our calculations.

These calculations are pretty simple; RPM is calculated for both sensors and then the speed sensor gets a multiplier for the circumfrence of the wheel. 

Where things get interesting is the Graphical User Interface (GUI). There is a reason for this - the GUI libraries that simply add onto Python are ugly as hell.

Instead, I used a library called Eel. Eel does two things: 
* Launches a local website 
* Connects the JavaScript from the website to the original Python script

Eel will ask for a folder containing the files needed for a website. By exposing functions in your Python or JavaScript, the function can be accessed by the other (exposing a function in Python makes it available in JavaScript and vice versa).

The downside is that some level of HTML/CSS profficiency is required to edit the GUI. To help compensate for this, I've put together a video about HTML/CSS. 

Please note that the main dials in the GUI are a library I pulled from the internet. As such, the majority of the settings are easily accessible in the attributes that load the dials. 

### Fabrication

### Programming 

# Software

