This file explains how to troubleshoot issues when setting up the Bitcraze AI deck 1.1 used in our experiments.  

## Method: 

To set up the AI deck, follow the instructions given in the ‘Getting Started with the AI deck’ guide: 
https://www.bitcraze.io/documentation/tutorials/getting-started-with-aideck/  

When completing these steps, the following things should be noted: 

* When selecting a firmware version to download in step 5 of the ‘Update Crazyflie and AIdeck firmware’ section, we encountered issues when attempting to download and use the latest release.  
**We instead selected the 2023.11 release** which then worked correctly.
* The ‘Gap8 bootloader’ step should be initially skipped, and instead the ‘Flash Wifi Example step’ should be attempted first. If this step fails, then you will need to complete the ‘Gap8 bootloader’ step (see below). 
* If the ‘Gap8 bootloader’ step needs to be completed, then you will need to create a connection between the AIdeck and a native Linux machine or virtual machine (not WSL) with a jtag enabled programmer (as explained in the guide). See the 'Completing the 'Gap8 bootloader' step' section below for how to do this.

## Completing the 'Gap8 bootloader' step:
We were able to complete this step using the following setup of components as described below: 

* Bitcraze Aideck 1.1 
* 10-pin JTAG-SWD cable  
* Debug Adapter Kit (Bitcraze) 
* ARM-USB-TINY-H 
* USB-A to USB-B 2.0 Cable 

These should be connected in the arrangement described below and in Fig 1. 

Port numbers given here refer to the labels given in Fig 1. 

1. Connect the **AI deck (port 1)** to the **Debug Adapter Kit (port 2)** using a **10-pin JTAG-SWD cable** using the ports indicated in Fig 1. 
2. Connect the **ARM-USB-TINY-H cable (port 4)** directly into the **Debug Adapter Kit (Bitcraze) (port 3)** using the ports indicated in Fig 1. 
3. Connect the USB-B male connector on the **USB-A to USB–B cable (port 6)** to the USB-B female connector on the **ARM-USB-TINY-H cable (port 5)**. 
4. Connect the USB-A connector of the **USB-A to USB–B cable (port 7)** to the USB port on the Linux machine running the Gap8 bootloader. 

![Aideck flashing connection diagram](https://github.com/TDI-Lab/M-SET-Documentation/assets/158288212/ff895b5d-c95d-49de-b9cc-a81072cea8e4)  
Fig 1: Diagram showing the connections between components used to perform the Gap8 bootloader step of the ‘Getting Started with the AI deck’ guide   

 
Once the components are arranged as above, the terminal commands listed in the ‘Gap8 bootloader’ step should be executed in a Linux terminal to clone, build and flash the bootloader. 

Finally, confirm that the AI deck has now been set up correctly by re-attempting the ‘Flash Wifi Example’ step at the end of the ‘Getting Started with the AI deck’ page. 
If this is successful, then the AI deck has been set up correctly. 