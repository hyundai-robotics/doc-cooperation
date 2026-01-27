### 5.2. Program Check in Manual Mode

(1) In manual mode, set the Master robot's manual cooperative state to I (Indiv.) or M (Master), and set the Slave robot's manual cooperative state to I (Indiv.) or S (Slave).
(2) Turn Drive Ready On and press the 'Step Forward' key on both sides.
(3) To verify synchronous motion between Master and Slave, press the Master and Slave step forward keys until cooperative motion is completed.
 
 <br>
 
![](../_assets/4-prg23.png)

![[Figure 5-5] Program check in manual mode](../_assets/5-5.png)

<br>
 

{% hint style="warning" %}
 
 - If the Slave is in cmov recording mode, manual mode cooperative operation with the Master will not be possible.
 - When executing step forward/backward, set 'Execute function on step forward' in Condition Settings to On.
 - The Master and Slave robots check the execution position only at the moment the cowork command is executed; they do not synchronize Master and Slave step positions outside of that. Therefore, the relative positions of Master and Slave checked using step forward/back may differ during automatic mode playback.
 - To synchronize the positions of the two robots, use the `cowork with, sync=1` statement.

{% endhint %}
