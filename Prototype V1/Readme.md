This is the first and most basic version of the M-Pen. I made this on breadboard with jumper cables.

Working: basically two 3 axis magnetometes(MMC5603) lined up against a 5 mm magnetic sphere, 
STM32f401CCU6 is used as the microcontrolled and two magnetometers are connected vis seprate I2C connections. MPU6050 was also configured on I2C1 for testing purpose.

The magnetometers continously monitor the magnetic field of the magnetb and predict its dipole orientation. the magnetic sphere is free to rotate along any arbitary axis, but it cannot move so the distance between dipole and magnetometers remains constant (because magnetic strength falls by 1/r^3 with distance, so a small movement can cause major mis calculations).
for calculating change in angle I used cosine to calculate angle between two magnetic vectors. 

Problems: 1) Cosine method is highly inaccurate for calculating change in angle because the magnetic field of the sphere has shape similar to torus, A methametical proof reinforcing the inaccuracy concept is also included in the images directory.

2) Two magnetometers and magnet sphere are placed in a line , this cofiguration creates a blind axis for the magnetometers which affects dipole orientation mechanism amd causes inaccuracies.

3) Since i made this on bread board loose jumper conections were interupting I2C connections.

4) Current fails to predict orienation of dipole in real time accurately.




