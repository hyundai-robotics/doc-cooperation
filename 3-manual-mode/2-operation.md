## 3.2. Manual Mode Cooperative Operation
### 3.2.1. Setting MASTER and SLAVE Robots

Use R351 to set robot roles to MASTER and SLAVE. The robot role is independent of the robot number.

 

![[Figure 3-7] Manual mode cooperative operation (Setting Master and Slave robots)](../_assets/3-7.png)

<br>
         
 - ① Confirm that both MASTER and SLAVE robots are in 'Manual Mode'.
 - ② Ensure both MASTER and SLAVE robots have Drive Ready ON and are in standby.
 - ③ Keep the Slave robot's ENABLE switch held so that Drive Ready ON is maintained, and confirm that the MASTER's Drive Ready is also ON.
 - ④ When the MASTER robot is operated, the SLAVE robot follows by tracking the relative position.

 
![[Figure 3-8] Manual mode cooperative operation (Master operation / Slave following)](../_assets/3-8.png)

<br>

{% hint style="warning" %}
 - Manual cooperative JOG is not possible in the following cases:
    - When more than one Master is designated and operated
    - When attempting to operate a robot set as Slave
    - When the Enable switches of Master or Slave are not pressed
    - When the inter-robot cooperative coordinate system is not configured
    - When cooperative control communication between robots is disconnected

 - In Manual Mode cooperative operation, JOG is not permitted on robots set as Slave. To jog a Slave, change the robot role to Manual Mode Independent.

 - If cooperative control is <Disabled>, the I:R# / S:R# / M:R# indicators will not appear at the top of the Manual Mode screen and cannot be configured, therefore Manual cooperative JOG is not possible.
{% endhint %}
