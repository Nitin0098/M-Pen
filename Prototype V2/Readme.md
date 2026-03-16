



Version 2 of M-Pen prototype, in this version I am using stm32f4 to read and send data of  magnetometers and accelerometer to my laptop vis serial communication 


Hardware changes: 

1. replaced jumper cables by JST XH connectors for stable connections.

2. distance between the magnetometers and spherical magnets is reduced, distance matters because magnetic field changes with distance as 1/r^3.

software changes:

1. updated STM32 firmware to increase sensor data output rate to 100hz.

2. 




problems:

1) both magnetometer are arranged in a straight line so they observe magnetic field across 1 axis only, we need to observe magnetic field in atleast 2 axes.

2) algorithm that predicts the orientation of dipole and it's rotation is flawed.

3) python script that plots the orientation of dipole in x and y plane needs improvements in


