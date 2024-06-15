## Example Paths

### Introduction
A number of files containing example drone paths are available in the `Hardware/example_paths` file in the M-SET repository.  
These include:
1. `Hardware/example_paths/4drones_no_CA.txt` - an example path for 4 drones with **no collision avoidance applied (contains collisions)**.
2. `Hardware/example_paths/4drones_schedulingCA.txt` - an example path for 4 drones with our Basic Collision Avoidance algorithm applied.
3. `Hardware/example_paths/2drones_potentialFieldsCA.txt`- an example path for 2 drones with our Potential Fields Collision Avoidance algorithm applied.

### Example 1
To run the first example listed above, run the following code:  
**Note that this path has not had any collision avoidance algorithms applied to it, and so still contains collisions between the drones.**  
**This path should only ever be run in simulation, NOT on the real-life drones**

```bash
python3 Hardware/cdca_epos_executor.py --sim Hardware/example_paths/4drones_no_CA.txt
```

### Example 2
To run the second example listed above in simulation, run the following code:  
```bash
python3 Hardware/cdca_epos_executor.py --sim Hardware/example_paths/4drones_schedulingCA.txt
```
To run this path on physical hardware, run the following code (and ensuring that the `IN_SIMULATION` parameter in `Hardware/Hardware_constants.py` is set to `False`.
```bash
python3 Hardware/cdca_epos_executor.py --sim Hardware/example_paths/4drones_schedulingCA.txt
```

### Example 3
To run the third example listed above in simulation, run the following code:  
```bash
python3 Hardware/cdca_epos_executor.py --sim Hardware/example_paths/2drones_potentialFieldsCA.txt
```
To run this path on physical hardware, run the following code (and ensuring that the `IN_SIMULATION` parameter in `Hardware/Hardware_constants.py` is set to `False`.
```bash
python3 Hardware/cdca_epos_executor.py --sim Hardware/example_paths/2drones_potentialFieldsCA.txt