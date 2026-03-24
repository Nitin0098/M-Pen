#Progress update: the direction issue is solved, prototype works ,it can track simple shapes like line and circle,
however for complex shapes and text it requires some plot algorithm changes.



#What is changed: 

1. previously I used |rotation vector| ≈ dα to calculate the change in rotation of dipole
in a small time dt but the full equation is  |rotation vector| ≈ dα x sin(theta), so i have updated
the code to correct equation for better accuracy and low noise.
2. Updated the IMU unit now it can detect the direction of gravity and north pole accurately, which is necessary for canvas plotting of the rotation of ball.
3. the orientation of sensors(magnetometer, Accelerometer, gyroscope and compass) is optimised.
4. direction issue is solved, previously during tests when I draw a line in right direction using prototype
it tracks the line but in random direction on python simulation due to lack of directional information,
 now with a compass onboard, the prototype tracks the line in correct direction.



#Issues with current version:

1. The directional accuracy falls significantly after some use due to currently unknown reasons and I am working to solve it.
2. The blind axis problem remains unsolved, maybe gyroscope can help solve this issue.
3. the line length tracked by the prototype has some errors , sometimes its larger than real length and sometimes smaller than real length,
   the reason behind the issue is,

   since  |rv| = dα × sin(θ)          rv is rotation vector, cross product of previous dipole orientation(M_previous) and new dipole orientation(M_new).
   therefore,
   θ = 90°   →   |rv| = dα × 1     = dα        ← full signal, perfect
   θ = 45°   →   |rv| = dα × 0.707 = 0.707·dα  ← 30% underestimate
   θ = 10°   →   |rv| = dα × 0.174 = 0.174·dα  ← 83% underestimate
   θ = 0°    →   |rv| = dα × 0     = 0          ← blind spot, total signal loss

   this issue can be solved methamatically.


   
   
