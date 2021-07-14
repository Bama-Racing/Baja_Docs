# Welcome to the Bama Racing Computer Science & Electrical GitHub
### Last Updated: Summer 2021

This document will discuss the Bama Racing Electrical Sub Team, its capabilities, areas for expansion, and some skills (or interests) needed to continue work.

# Table of Contents
* [Current Team Members](#team-members)
* [External Documentation](#external-documentation)
* [Recommended Skills](#Recommended-Skills)
* [System Overview](#System-Overview)
  - HUD Overview
  - Kill Switches
  - Brakelight
  - Headlights
* [System Details](#System-Details)
  - HUD Overview
  - Kill Switches
  - Brakelight
* [Fabrication Methods & Notes](#Fabrication-Methods-&-Notes)
* [A Path Forward](#A-Path-Forward)

# Team Members
* Nathan Eads
* Jade Cartolano
* Emma Goldthorpe
* John Yordy
* Brendan Kuhlmann

# External Documentation
* [SAE Baja Rule Book (Download Latest Version)](https://www.bajasae.net/cdsweb/gen/DocumentResources.aspx)
* [Eel Documentation](https://github.com/ChrisKnott/Eel)
* [Link to JavaScript Dials](https://www.cssscript.com/canvas-based-html5-gauge-library-gauge-js/)
* [My HTML/CSS/JS Video Tutorial]()
* [W3 Schools HTML](https://www.w3schools.com/html/default.asp)
* [W3 Schools CSS](https://www.w3schools.com/css/default.asp)
* [W3 Schools JS](https://www.w3schools.com/js/default.asp)
* [Arduino Speedometer Examples](https://makersportal.com/blog/2018/10/3/arduino-tachometer-using-a-hall-effect-sensor-to-measure-rotations-from-a-fan)

# Recommended Skills or Interests
Since I had the liberty of building this project essentially from scratch, I used a method based around my own skillset. I hope that this does not cause problems down the road.

Moreover, I want to note that **no skills whatsoever are required** coming into this project and I encourage you to strive to add a skill of your own to this list before you hang up your hat.

That being said, the following is a list of programming languages, softwares, methods, etc. currently used in the Bama Racing Electrical System:
* Python3
* HTML/CSS
* JavaScript
* 3D Modeling (SolidWorks)
* 3D Printing
* Soldering
* GitHub
* Eel (Python Library)

# System Overview
### HUD Overview
The HUD is Electrical's show pony. It is currently comprised of a Raspberry Pi connected to a touch screen display and two Hall Effect Sensors (HES). These Hall Effect Sensors are able to detect magnetic fields. By placing magnets on the output shaft of the engine and one of the axles, we can derive engine and wheel RPM (and then calculate speed).

### Firmware
The firmware is what I have labeled the calculation code. This code begins by using a listener event called an interrupt to monitor the GPIO pins the Hall Effect Sensors are connected to.

When the voltage on this pin changes, the interrupt listener is triggered and calls the prescribed function. This function records the time between pulses in nanoseconds and uses this to calculate RPM. The speed function is then multiplied by a constant to account for wheel diameter.

### Software
The data from the speed and RPM functions is then saved to a variable. The software then displays these variables on the GUI.

### GUI
The GUI is generated using a library called Eel. Eel does a couple things:
* Launches a locally hosted website
* Connects the JavaScript (JS) file in this site to your main Python script

By connecting the JS and Python with Eel, the main Python script is able to call functions defined in your JavaScript... since JavaScript has built in features to modify HTML, using Eel as a proxy, your Python can modify the HTML GUI.  

Eel will be discussed in more depth [below]().  

### Kill Switches
Kill Switches are required by SAE.

Pressing **either** kill switch should stop the engine.

### Brakelight
The brakelight is also required by SAE. You should again double check the [SAE Rulebook] to make sure the following information is still accurate.

### Headlights
In the past, Baja has run a lightbar or similar headlight unit. This is not required and should take a lower priority than the items above, but it is a very simple circuit.

# System Details
### The HUD
The HUD is currently comprised of three major PCBs and one power distribution PCB (the power PCB simply gives more slots for 3v3 power and ground coming from the RasPi to power the HES).

In addition to the power distribution board, the RasPi is also connected to the Hall Effect Sensors with one data cable to each board.

These sensors have a binary digital output dependent on their proximity to magnetic fields. If you are unfamilair with Arduinos and RasPis, binary digital output simply means that the sensor can vary the voltage coming out of its signal pin; when there is a magnetic field detected by the sensor, the voltage will be set to 3.3V. When there is no magnetic field detected, the signal output pin is set to 0V.

We can then monitor the voltage set by these sensors which is transmitted to the Pi through their digital output pins. When the voltage changes, the firmware will trigger the calculation functions discussed above.

### Kill Switches
You should double check the [SAE Rulebook] for the latest rules, however currently, one button-switch is placed on the driver's left side near the middle of the side impact and another on the upper right side of the frame, just behind the firewall, when looking at the car from behind.

The kill switches work by shorting out the low-voltage end of the alternator's transformer. A car produces it's electricity using an alternator; the alternator sits on the engine and turns the motion of the shafts into electrical power. This electricity is then put into a transformer which provides adequate voltage/current to the sparkplug.

By shorting this transformer, we can halt the spark plugs from firing, thus "killing" the engine.

### Brakelight
There are two brakelight sensors integrated into the brakeline. When the brake is pushed, the pressure in the brakeline causes these switches to close an electrical circuit.

By connecting these sensors in parallel and then in series with a pair of 9V batteries in parallel, and assuming the brakes team did their job correctly, both brake lines should trigger the brake light. **You should test to make sure that both brake lines trigger the light by disconnecting one sensor at a time and pressing the brake pedal.**

# Fabrication Methods & Notes   
The following section will briefly touch on the recommended skills listed [above]() as well as some challenges in fabricating the HUD, should you choose to pursue fabricating a new unit.

### 3D Printing
I base a lot of my work around 3D printing. It's very fast, if I plan my day well, I can go through 10 - 15 iterations of a design per day, compared to a teammate who might go through a similar number in a year.

If you pick the right filament, and the right settings, you can produce some solid results, but you are limited to the durability of plastics.

* If you are not comfortable learning to use the printer in the office on your own, please reach out to Nathan Eads.

* If you do not want to learn how to use a printer and would just prefer to have your models produced for you, consider reaching out to the Cube. This will take longer, but it's free and a good choice for early prototypes.

*Even if you use the printer in the office, it might be wise to setup an account with the Cube. Sometimes you will be busy. Sometimes, you just need something made for you.*

### Waterproofing
*The kill switches, brakelight, and headlights do not need to be waterproofed.*

Any housing for the HUD will need to be waterproofed. I recommend a mix of window sealant and hotglue. Window sealant works well for long crevices and hotglue works well for large surface area holes. Optimally, whatever waterproof unit the HUD is placed in will also be covered by the front hood body panel. **DO NOT allow the HUD to be run if it is actively raining**, understand that any waterproof unit is prone to failure.

For 3D printed parts, please note that layer lines will leak under prolonged exposure. To compensate for this, maximizing the layer height (thereby minimizing the number of layers, and thus the number of gaps between layers) will reduce potential leak points. Likewise, increasing infill percentage (akin to density) will leave fewer internal structures for water to permeate.

### GitHub/Atom
The GitHub ecosystem makes it really easy to write and test code.

Atom is a code editor made by GitHub; by linking your GitHub account, and using GitHub Desktop, you can open a repository in Atom and then directly upload any changes you make to GitHub. Then, you can pull these changes to the RasPi with just one command.

You can find a plethora of videos on YouTube showing you how to setup both Atom and how to download from GitHub using the command line on a RasPi, so I won't go into further detail here.

### CAD
For 3D modeling, I prefer SolidWorks and all of my models are .SLDPRT or .SLDASM.

If you are new to CAD, SolidWorks is a great starting point, there are a ton of tutorials on YouTube and most of your teammates are proficient and are happy to answer questions or point you to some good resources.

Note that all of my files are in metric (millimeters). This is the standard unit for 3D printing, a tool I base much of my workflow around. I recommend using millimeters to keep things consistent for your future successors (sorry), but I will leave this to your discretion.

### Programming
This is where things might get a little daunting.

To start the HUD's software, you will run a Python3 script (make sure you run it with a virtual environment running Python 3.7 or later). This will be the main Python script found on the RasPi.

Assuming no one has touched the Pi since I last did, the last two commands in the console will start a Python3 virtual environment and the HUD firmware itself. You can run these commands by clicking on the console, and scrolling through history using the arrow keys.  

Where things get interesting is the Graphical User Interface (GUI). There is a reason for this - the GUI libraries that add directly into Python are ugly as hell.

Eel will ask for a folder containing the files needed for a website. By exposing functions in your Python or JavaScript, the function can be accessed by the other (exposing a function in Python makes it available in JavaScript and vice versa).

Eel's documentation is very well written, you can explore that [here]().

The downside is that some level of HTML/CSS proficiency is required to edit the GUI. To help compensate for this, I've put together a [video]() about HTML/CSS.

Please note that the main dials in the GUI are a library I pulled from the internet. As such, the majority of the settings are easily accessible in the attributes that load the dials.

### Soldering
Soldering will take practice, don't get frustrated. There are a million techniques and tutorials, explore YouTube, practice and you'll get better with time.  

Thankfully, by spending the school's money, you can buy yourself some tools that will help you out.
* [A nice soldering iron.](https://www.amazon.com/X-Tronic-3020-XTS-Digital-Display-Soldering/dp/B079VVHPPS/ref=sr_1_22?dchild=1&keywords=soldering%2Biron&qid=1621650649&sr=8-22&th=1)
* [Nice solder.](https://www.amazon.com/MAIYUM-63-37-Solder-Electrical-Soldering/dp/B075WBDYZZ/ref=sr_1_5?dchild=1&keywords=solder&qid=1621650669&sr=8-5&th=1)
* [A solder sucker for when you mess up.](https://www.amazon.com/Solder-Sucker-Desoldering-Removal-Soldering/dp/B08FDY2SGS/ref=sr_1_7?dchild=1&keywords=solder+sucker&qid=1621650674&sr=8-7)

# Code Video Tutorials

These tutorials are in no way meant to be comprehensive, but they should serve as a launch point for you to delve further into the subject areas that cause you trouble.

### HTML/CSS/JS
[Overview](https://www.youtube.com/watch?v=gT0Lh1eYk78)
[HTML (Short)](https://www.youtube.com/watch?v=bWPMSSsVdPk)
[HTML (Atom)](https://www.youtube.com/watch?v=bupWPZdXqIA)
[CSS](https://www.youtube.com/watch?v=1PnVor36_40)
[JavaScript](https://www.youtube.com/watch?v=W6NZfCO5SIk)

### Python3
[Python Overview](https://www.youtube.com/watch?v=kqtD5dpn9C8)
[Python Eel](https://www.youtube.com/watch?v=8eeUV1RHkmw)
[Python on a RasPi](https://www.youtube.com/watch?v=xTIBG_KD8Bk)
[Linux Virtual Environments](https://www.youtube.com/watch?v=Kg1Yvry_Ydk)

# A Path Forward
### Incomplete Features
###### Zero Timeout
Currently, neither the speedometer nor the tachometer will ever reach zero. Since these values are calculated by dividing a constant by a change in time, at no point in time will this function ever return zero.

Instead, what you have to do is decide that after a certain time that the engine has stopped.

###### File Recording
In order for the HUD to be put to use, the drivetrain team will need RPM and speed data from the car. This will allow them to preform some more calculations and tune the transmission.

The best way I found to do this, was to write to a .CSV file. This file type can easily be imported to Excel.

###### Radios
In an attempt to include some members into my hectic workflow, I asked some people to explore radio telemetry. The goal with this expansion was to receive data from the HUD remotely.

This team elected to use a radio platform called LoRa.

###### HUD Waterproof Unit
The HUD's waterproof unit was assembled faster than I would have liked. It could use a redesign and makeover.
