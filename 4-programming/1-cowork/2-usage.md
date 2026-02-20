### 4.1.2. How to Use the `cowork` Command

(1) On the MASTER robot, the actions within the `cowork ~ cowork end` section are treated as cooperative segment commands. SLAVEs cannot insert action commands.

(2) On SLAVE robots, standard `move` commands cannot be used within the cooperative section; use the `cmov` command (cowork move) instead.

(3) In handling applications where the Slave follows the Master, as in the example below, the Slave will maintain the relative position to the Master and move accordingly when the `cowork` command is executed even if no `cmov` commands are inserted on the Slave.

![](../../_assets/4-prg1.png)
 
(4) On the Slave, you can insert `cmov` commands that interpolate in the Master end effector coordinate system; `cmov` recorded positions are relative to the Master's tool end effector coordinate system. If taught as in the example below, within `cowork ~ cowork end` the Slave performs cooperative motion and follows the Master's movement along the `cmov` path recorded in the Master end effector coordinate system.

 ![](../../_assets/4-prg2.png)

{% hint style="warning" %}

 - A `cowork end` command must be inserted at the end of cooperative motion.
 - For SLAVE robots, `move` commands cannot be inserted within the cooperative section; for MASTER robots, `cmov` commands cannot be inserted.

{% endhint %}
