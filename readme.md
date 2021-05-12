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

# Hardware Overview
### The HUD 
The HUD is currently comprised of three major PCBs and one tertiary power distribution PCB (I know that might sound scary, stick with me). 

The firmware in repositories under this Organization is run off of the main PCB, a Raspberry Pi 3B+ (RasPi). 

The RasPi is then connected to two Hall Effect Sensors. These sensors have a binary digital output dependent on their proximity to magnetic fields. 

When they detect a magnetic field, the firmware will begin to calculate speed or RPM respectively. 

### Other Electrical Systems 


# Recommended Skills, Languages & Tools

This section will discuss my workflow and the skills being used in the current build of the Bama Racing HUD. No proficiency is required in the following areas, but I would recommend at least being interested - Baja should be fun!

### Software
##### GitHub/Atom 
Clearly, I use GitHub. This ecosystem makes it really easy to write and test code.

Atom is a code editor made by GitHub; by linking your GitHub account, and using GitHub Desktop, you can open a repository in Atom and then directly upload any changes you make to GitHub. Then, you can pull these changes to the RasPi with just one command. 

##### CAD 
For 3D modeling, I prefer SolidWorks. If you are new, SolidWorks is a great starting point, there are a ton of tutorials on YouTube and most of your teammates are proficient and are happy to answer questions or point you to some good resources. 

Note that all of my files are in metric (millimeters). This is the standard unit for 3D printing, a tool I base much of my workflow around. I recommend using millimeters to keep things consistent for your future successors (sorry), but I will leave this to your discretion. 

### Fabrication

### Programming 

# Software

