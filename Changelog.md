## 2.2.1

### Bug fixes
- Fixed an issue with the coppelia scene resetting halfway through the automatic preprocessing changes.
- Fixed an issue with the number of models being uninitialized in **preprocessing** and **environment**.

## 2.2.0

### Major changes
- Gas sensor and anemometer nodes now use <node_name> as the prefix for their published topics (*e.g.* `/Anemometer1/WindSensor_reading`). This allows you to more easily have multiple nodes of the same type, each publishing to its own topics.
- Added a node to **gaden_preprocessing** to set the initial position of the robot in the coppelia scene. Can be used a single time to permanently change the position and serialize the change, or launched every time you start the simulation to set the position for that run only.

### Minor changes
- Removed outdated **gaden_gui** package. Maybe it will be replaced with a working version in the future. Maybe.
- Changed the error message when giving an incorrect path to the **gaden_player** node. Now there is a single error telling you the folder does not exist, and then the node exits, rather than constantly spamming that each individual iteration is missing.

### Bug fixes
- Fixed a bug causing the execution rate of the simulated gas sensor to be unitialized.

## 2.1.0

### Major changes:
- Filament simulator no longer appends a long description of the simulation (`"FilamentSimulator_gas_type_source_location..."`) to the specified path for the results folder. This can break existing launch files, as the **filament_simulator** node and the gaden_player node used to require different parameters to account for this extra subfolder. 
</br>While breaking changes are obviously undesirable, the fact that from now on both nodes will expect the same string (the actual path of the results folder) should make things far less confusing.

### Minor changes
- Removed the "number of models" parameter from **environment** and **preprocessing**. The total count is now inferred from the indices of the existing parameters.
- Improved console logging from preprocessing.
- Changed the structure of test_env to include the "simulation" yamls. This will be explained in more detail in the tutorial.

## 2.0.0
### Ported Gaden to ROS2!