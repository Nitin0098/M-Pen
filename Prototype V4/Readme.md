PROGRESS REPORT: prototype works partially, it can detect orientation of dipole and its rotation in real time accurately for most part.


Improvements I made
1. placed both magnetometers at 90 degrees to each other , so now they monitor different axes, so nnow the blind axis nproblem is solved.
2. magnetometer axes and its distance from magnet configured carefully, earlier i did not considered magnetometer axes into consideration which was causing significant misscalculations.
3. Distance between the magnetometers and magnet reduced and carefully adjusted to certain values, which resulted in increased signat to magnetometers.

PROBLEM 1:
when magnet ball rotates along the dipole axis, it produces no change in magnetic field, so magnetometers cannot detect rotation of magnet along dipole axis, its like a smooth cylinder rotating along its axis, practically no sensor arrangement can detect it. also known as blind axis problem.

How I solved it:
I have 2 solutions for this problem;
1. the scenerio in which axis of rotation perfectly alligns with dipole axis is very rare, as the sphere is continously rotating, that scenerio won't last long, so first solution is ignore this problem.
2. switching to gyroscope when this scenerio occurs is another solution.

PROBLEM 2:
The rotating dipole has no directional reference, which leads to random directions in the plot which occured in previous prototypes, 
we can track the rotation of dipole, but the device has no way to identify which way is east or which way is down.

How I am planning to solve it: A accelerometer tat senses gravity will provide the up and down directional reference,
A seprate magnetometer placed far from dipole will act as a compass and provide directional reference. 



