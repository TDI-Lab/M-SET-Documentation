## Introduction
This file describes how to troubleshoot issues when attempting to retrieve logging data from multiple Crazyflie drones in flight.

## Libraries Used
In our experiments, the Crazyswarm python library was used to control and monitor the drones. This library supports logging via ROS (Robot Operating System), and implements a number of variables which can be logged from the Crazyflie drones. The documentation for these logging variables can be found at the link below:
https://www.bitcraze.io/documentation/repository/crazyflie-firmware/master/api/params/  

### Alternatives
Logging of data from the Crazyflie drones can also be performed via the cflib python library the as described in the link below:
https://www.bitcraze.io/documentation/repository/crazyflie-lib-python/master/user-guides/sbs_connect_log_param/ 
However, we encountered issues when attempting to connect to the Crazyflie drones with both the cflib code for logging and then the crazyswarm module for controlling the drones at the same time. This was because both libraries attempted to connect to the drone via the same Crazyradio PA, and this caused a LIB_USB_ERROR when ROS was launched as part of crazyswarm, stating that the “resource <(the Crazyradio PA)> <was> already in use”. This meant that although cflib could be used to retrieve logging data from the drones when they were stationary, we were not able to use cflib to retrieve logging data from the drones while they were moving as we used the crazyswarm library to control the movement of the drones.

## Method

### Enabling logging
To enable logging with the Crazyswarm library, the following config variables must be set in the hover_swarm.launch file:
* enable_logging = True

### Creating a custom rostopic in Crazyswarm

Make the following additions to the hover_swarm.launch file:
* Specify the name of the log topic  
  Syntax: `genericLogTopics: ["<log topic name>"]`  
  E.g. `genericLogTopics: ["log1"]`  

* Specify the frequency that data should be published to the above log topic  
  Syntax: `genericLogTopicFrequencies: [<frequency in mHz>]  `
  E.g. `genericLogTopicFrequencies: [1000]`  
* Specify the variables thats values will be published to the log topic  
  Syntax: `genericLogTopic_log1_Variables: ["<variable 1 name>", "<variable 2 name>", …]`   
  E.g. `genericLogTopic_log1_Variables: ["pm.vbat"]`  

### Confirm successful setup via command line
To confirm that the log topics have been set up correctly, the `rostopic list` and `rostopic echo` commands can be used in the terminal.
    
    rostopic list
Executing `rostopic list` will print the list of active log topics to the terminal. You can then confirm that the custom log topic(s) you have created appear here and that they appear for all drones.
E.g. if you created a custom log topic called "log1", and you have 3 drones active (cf1, cf2, cf3), then you would expect to see the following somewhere in the terminal output:  
cf1/log1  
cf2/log1  
cf3/log1  
    
    rostopic echo <rostopic name>
Executing 'rostopic echo <log topic name>' will listen on the given log topic, and output any data retrieved from it to the terminal as it is retrieved.  
E.g. continuing the above example, then if you executed 'rostopic echo cf1/log1' in the terminal, then you would see the data retrieved from the cf1/log1 log topic.

If the output of 'rostopic list' is as expected, but executing 'rostopic echo' for some log topics for some drones does not produce any output, then this may be an issue caused by the limited bandwidth of the Crazyflies / Crazyradio PA (see 'Troubleshooting Bandwidth Issues' below). 

### Troubleshooting Bandwidth Issues
For the purposes of enabling logging, most variables can be left as they are after completing the initial setup of the Crazyflies. However, a significant challenge faced when attempting to retrieve logging data from multiple drones at once is that the drones / the Crazyradio PAs have a limited bandwidth and so can only successfully send a limited amount of logging data at each call. Since a separate rostopic is created for each drone in use (e.g. cf1/log1, cf2/log1, etc.), then when attempting to retrieve logging data when multiple drones are in use you may find that data can only be retrieved from a given rostopic for some drones and not others. It may also be possible that if enough logging data is published for a single drone then this data may exceed the bandwidth and mean that data will not be retrieved from all rostopics / that the data retrieved from some rostopics will be partial. 

To work around this and ensure the necessary data can be retrieved for all drones in use, then we need to reduce the amount of data published by each drone, which will free up the bandwidth to enable this.

Assuming that the number of drones in use is fixed, then there are two main methods to achieve this:
1. Reduce the number of rostopics
2. Reduce the amount of data sent in the rostopics 

Both methods can be achieved by changing config settings (see below). Method 2 can also be followed by controlling the number of variables added to the custom log topic created (see 'Creating a custom rostopic in Crazyswarm' above).

To reduce the logging data published, the following variables can be changed in the hover_swarm.launch file:
* send_position_only = True (disables logging of the orientation of the drones)
* Force_no_cache = True
* enable_parameters = True
* enable_logging_pose = False (disables logging of the pose of the drones)

### Set Up ROS Publishers and Listeners:
To retrieve the log topic data using code (as opposed to terminal commands), then you will need to set up ROS Publishers and ROS Subscribers in your code.  

The following tutorial from the ROS wiki explains how to do this in Python:  
http://wiki.ros.org/ROS/Tutorials/WritingPublisherSubscriber%28python%29

The topic name passed to the subscriber should be the same name as the custom log topic(s) created for each drone e.g. cf1/log1.