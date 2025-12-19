## 5.5. Robot Lock Function (Robot Lock Playback)

Set 'Condition Settings' → '5: Robot Lock' to <Enabled>.

 
<br>

![[Figure 5-8] Robot Lock Enable Setting](../_assets/5-8.png)

<br>

When the Master robot is set to Robot Lock <Enabled> and playback is performed, the Slave performs cooperative motion while the Master robot does not move and only the axis data monitor changes.


<br>

![[Figure 5-10] Robot Lock Function (Master Lock)](../_assets/5-10.png)

<br>

If the Slave robot is set to Robot Lock <Enabled> and the Master robot is set to <Disabled>, the Master robot operates normally while the Slave robot remains stopped and only monitoring data moves.

<br>

![[Figure 5-11] Robot Lock Function (Slave Lock)](../_assets/5-11.png)

<br>

 

When both Master and Slave are set to Robot Lock <Enabled>, the program runs with both Master and Slave stopped.
 
<br>

![[Figure 5-12] Robot Lock Function (Master, Slave Lock)](../_assets/5-12.png)

<br>


{% hint style="warning" %}

 - Set the cooperative waiting time to an appropriate length.
 - Robots set to Robot Lock <Enabled> will not move, so move them to a position where they will not interfere with other robots before running the program.
 - When changing the Robot Lock setting back to <Disabled> and running, the robot positions and step positions may not correspond; please run the program from the beginning.

{% endhint %}
