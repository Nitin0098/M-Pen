
Version 2 of M-Pen prototype,


Hardware changes: 

1. Replaced jumper cables by JST XH connectors for stable connections.
2. Distance between the magnetometers and spherical magnets is reduced, distance matters because magnetic field changes with distance as 1/r^3.

software changes:

1. Updated STM32 firmware to increase sensor data output rate to 100hz.
2. Used atan2 method to calculate rotation of dipole along arbitary axis instead of cos(thetha).
3. Enabled set reset cycles in the magnetometers to clear residual magnetic remanance from previous operations.


problems:

1) Both magnetometer are arranged in a straight line so they observe magnetic field across 1 axis only, we need to observe magnetic field in atleast 2 axes.
2) Algorithm that predicts the orientation of dipole and it's rotation is somehow not roducing expected results.
3) Python script that plots the orientation of dipole in x and y plane needs improvements in stability and smoothness of plots.


