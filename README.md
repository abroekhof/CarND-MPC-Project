# MPC Project Submission

## Cost function
It uses a cost function based on Cross Track Error, path angle deviation, and velocity error. The cost function also incorporates the actuator inputs, to minimize their usage. Furthermore, the difference between successive actuations is included to prevent chattering between different actuator inputs.

These costs were weighted, with CTE having the highest priority, followed by the path angle deviation. This provided good results, and is an intuitive decision, given that the main priority is to center the car, and have it point in the correct direction.

## Model
The car model is given as a constraint to the non-linear optimizer. This model is the same car model that was given in class, where the car is defined by its x and y cooridinates and its heading. The velocity and heading are affected by acceleration and steering angle inputs, which are given on lines 98-103.

## Implementation details
A 100 ms latency was used to model real-life actuator delays. To account for this delay, the car was projected forward in space based on its current velocity. Also, the MPC time step was set to 100 ms, to replicate the actual control frequency. 

The horizon was set to 10 timesteps, which provided a balance between sufficient look-ahead to provide good results, without diminishing the importance of early actuator movements. This also could have been addressed by having decaying weights for later timesteps. 

A 3rd-order polynomial was used to estimate the trajectory of the path based on the provided waypoints. This gave a more realistic path for the cross-track error and path angle deviation.