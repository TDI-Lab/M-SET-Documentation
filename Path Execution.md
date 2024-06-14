## Execution of Paths

### Crazyswarm Setup
Before drone paths can be executed (in simulation or on physical hardware) the Crazyswarm python library must be installed and configured following the instruction in the `Crazyswarm Setup` section of the documentation.

### Path Execution Config File
The configuration file for path execution can currently be found in Hardware/Hardware_constants.py

| Parameter          | Description                                                             |
|--------------------|-------------------------------------------------------------------------|
|HOVER_HEIGHT | Vertical height that the drones fly at (m). When the drones take off they will fly to this height.|
|SPEED | Horizontal speed of the drones (m/s)|
|INPUT_MODE | Should be set to "cdca" when executing paths output by the Collision Avoidance system, or "default" if executing paths produced directly by the Path Generation system (with no collision avoidance applied). CAN BE OVERWITTEN AT COMMAND LINE by including "cdca" or "default" as a command line argument (see below).|
|ENABLE_LOGGING | Enable logging in the path execution code. |
|PRINT_LOG_MESSAGES | True: log messages will be printed to the terminal running the path execution code. False: log messages will not be printed to the to the terminal running the path execution code. Does not affect anywhere else that the log messages are output to.|
|LOG_OUTPUT_FILE | If ENABLE_LOGGING=True, then any logging data retrieved will be written to the file specified here. |
| IN_SIMULATION | Will be set automatically by --sim in command line|
|TRAVEL_TIME_MODE | =2: Default, drones will fly at the speed given by the SPEED parameter. =0: The speed of the drones will be set such that eac movement between 2 points will have a duration equal to the value of the GLOBAL_TRAVEL_TIME parameter.|
|USE_CELL_COORDS | False: Default, path coordinates will be interpreted as actual positions in the physical testing environment. True: Path coordinates will be interpreted as testbed grid coords (which may differ from the actual physical distances)|
| TIMESTEP_LENGTH | Length of one timestep in the path execution code (s), should be <<1. To avoid floating point precision errors, this should always be a value that can be represented by 2^{x}, where x is an integer|
| GLOBAL_TRAVEL_TIME | Not required unless TRAVEL_TIME_MODE=0, in which case it is used as the duration of any movement between two points by the drones (s). |
| SENSING_TIME | Time in seconds. |
| CRAZYSWARM_SCRIPTS_FILE_PATH | Path to the Crazyswarm installation. Needs to be set on the individual system. |

### Simulation
To execute a given path in simulation, the following command can be used in the terminal:

```bash
  python Hardware/cdca_epos_executor.py <file containing drone path> --sim
```
**Note**: it is inportant to include the `--sim` here, as this is what instructs the code to launch the simulation.  
This will execute the given drone path in a simulated environment, provided by matplotlib by default.  

### Hardware
In order to execute the path on the physical hardware (the drones), then some more steps are required.

**Prerequisites**:
1. The physical testing environment must be set up for the drones to fly in, and the drones must be configured in Crazyswarm. Instructions of how this was done in our experiments can be found in the `Hardware Setup` section of the documentation.
2. ROS must be installed and configured as described in the `ROS Setup` section of the documentation.

  
**Method**:
1. Navigate to the `crazyswarm/ros_ws` folder in the terminal, and run the following code:
```bash
source devel/setup.bash 
```
This will source ROS in the terminal, which is required for running applications which make use of ROS from this terminal. **Note** that this has to be done every time for every new terminal opened.  

3. Execute the following command in the terminal
```bash
roslaunch src/crazyswarm/launch/hover_swarm.launch
```
This will launch ROS in the terminal for use with Crazyswarm. If this runs successfully, then you are now ready to execute the drone paths on hardware.

4. **Before performing this step, please ensure that the drones are in position and ready to fly. The drones will begin executing the path immediately after this command is run.**  
  
To execute the path on the hardware, execute the following code in the terminal:  
```bash
python Hardware/cdca_epos_executor.py <file containing drone path>
```
(Note: This is the same command as is used to execute the drone paths in simulation, but without the `--sim`.)