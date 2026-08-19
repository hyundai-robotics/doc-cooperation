## 3.4. cmov Recording Mode Jog

The cmov recording mode is a mode for teaching Slave positions for jigless cooperative motion.

 - How to set cmov recording mode:
    - Set the Master's manual cooperative state to "Master". (R351, 1)
    - Select the manual cooperative state for the robot as "Slave". (R351, 2)
    - Select the manual cooperative state for the robot as "cmov". (R351, 3) <br>
    Regarding recording conditions, when the master robot is Robot 3, the `cmov` command is automatically recorded with `R31..` if the master robot's coordinate system is set to "Sync S1," with `R32..` if set to "Sync S2," and with `R30..` for any other coordinate system.
    - Even in Cartesian coordinate jog state, jogging is performed relative to the robot's Cartesian coordinate system regardless of the Master coordinates.

<Br>

![[Figure 3-10] cmov recording mode jog](../_assets/3-10.png)

<br>
 
<br>

 {% hint style="warning" %}
- The drive axes of cooperative control systems should be installed as parallel as possible between Master and Slave.
- When the Slave is in cmov recording mode, jogging of the robot set as Master in manual cooperative state is not allowed.
{% endhint %}
