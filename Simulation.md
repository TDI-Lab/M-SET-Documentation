# Simulation Overview

We have implemented two methods of visualising the execution of drone paths in simulation:
1. Swarm Control visualisation (implemented within the Collision Avoidance module)
* Renders a visualisation of the drone paths in a matplotlib FuncAnimation
* Requires little setup
* Can be run on Windows or Linux
* Separate to the code used to execute the drone paths on physical hardware (real-life drones)

2. Path Execution simulation
* Uses the visualisation engine provided by the Crazyswarm python library
* Requires more setup
* Can only be run on Linux (due to the requirements of the Crazyswarm python library)
* Closely linked to the code used to execute the drone paths on physical hardware (real-life drones)

## Swarm Control Visualisation
The code for the Swarm Control visualisation can be found in the `cdca` folder.

## Path Execution Simulation
The code for the Path Execution simulation can be found in the `Hardware` folder.  
Documentation for the Path Execution simulation can be found in the [Path Exectution](https://github.com/TDI-Lab/M-SET-Documentation/blob/main/Path%20Execution.md) section.
