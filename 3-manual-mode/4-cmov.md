## 3.4. cmov Recording Mode Jog

The cmov recording mode is a mode for teaching Slave positions for jigless cooperative motion.

 - How to set cmov recording mode:
    - ① Select the robot role as Slave.
    - ② Set the Master's manual cooperative state to MASTER.
    - ④ Even in Cartesian coordinate jog state, jogging is performed relative to the robot's Cartesian coordinate system regardless of the Master coordinates.

<Br>

![[Figure 3-10] cmov recording mode jog](../_assets/3-10.png)

<br>
 
<br>

 {% hint style="warning" %}
- The drive axes of cooperative control systems should be installed as parallel as possible between Master and Slave.
- When the Slave is in cmov recording mode, jogging of the robot set as Master in manual cooperative state is not allowed.
{% endhint %}
