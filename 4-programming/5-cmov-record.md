## 4.5. Checking cmov Recorded Positions

The cmov steps are a useful feature that allows you to verify taught positions using the step forward/back functions in cmov recording mode. The cmov step records positions and orientations relative to the Master end effector coordinate system, so verify and execute based on the Master's tool position.

 - (1) Set the robot taught as Master (cowork m) to Manual Cooperative Master state (R351,1).
 - (2) Set the robot taught as Slave (cowork s) to cmov recording state (R351,3).
 - (3) Move the Master robot to the step position to be cooperated and leave it stopped.
 - (4) On the Slave, select the cmov step to move to and press the step forward key; the Slave will move to the position recorded in the Master end effector. For example, if the cmov recording position is recorded as the origin (0,0,0) of the Master end effector coordinate system as shown below, the Slave will move to the Master end effector origin regardless of the Master's global position when executing cmov.

 
![[Figure 4-6] Checking cmov recorded positions](../_assets/4-6.png)

{% hint style="warning" %}
 - In cmov recording state (R351,3), the robot will move to the recorded step position regardless of cowork command execution.
 - Master jogging is not allowed in cmov recording state.
 - Because real-time cooperative motion does not occur in cmov recording state, do not operate step forward/back on the Master simultaneously; keep the Master stopped.
 - If you change and then stop the Master's position while in cmov recording state, stepping forward to the cmov step will move to the updated position.
{% endhint %}
