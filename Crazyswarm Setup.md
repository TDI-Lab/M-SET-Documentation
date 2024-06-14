# Crazyswarm Setup

## Installation
To install Crazyswarm, follow the instructions in the documentation given at the following link:  
https://crazyswarm.readthedocs.io/en/latest/installation.html 

**Note**: Please ensure that you select the "Physical Robots and Simulation" section if you wish to execute drone paths on physical drones (as opposed to just in simulation).

**This will also require you to install ROS if you have not already done so.**  
This can be done by following the instructions [here](http://wiki.ros.org/ROS/Installation).

## Configuration
Continue following the steps in the Crazyswarm documentation, this time working through the steps in the Configuration section:  
https://crazyswarm.readthedocs.io/en/latest/configuration.html

See below for further notes on how to complete this section:

### Adjusting Configuration Files
When completing the [Adjusting Configuration Files](https://crazyswarm.readthedocs.io/en/latest/configuration.html#adjust-configuration-files) section of the guide, please choose the configurations most appropriate for your system.  

If you wish to replicate our setup in this section:  
* In the [Select Hardware Make](https://crazyswarm.readthedocs.io/en/latest/configuration.html#select-hardware-make) section, follow the instructions in the 'LPS/LightHouse/FlowDeck' tab.  
* Ensure `object_tracking_type` is set to "libobjecttracker", and `motion_capture_type` is set to "none" in the `hover_swarm.launch` file.

