## 7.3.1. Deceleration Stop

If the robot decelerates and stops after invading the user-configured arm interference area and tool interference area, due to deceleration distance and robot inertia, a collision may occur even if an error is detected. Therefore, the detection area is expanded taking robot speed into account to detect interference earlier.

The figure below illustrates the concept of generating an expected interference area (Level 2 detection area) when robots move toward each other. The dashed area indicates the expected interference area, and the solid line indicates the user-configured interference area.
 
![[Figure 7-22] Interference area invasion 1](../../_assets/7-22.png)


<br>

The expected interference area is automatically set by calculating the robot's travel speed and stopping time, but the user can set the maximum value as the 'expected maximum interference distance.'
The expected interference distance calculated by the controller, when the robot moves at high speed, is the configured interference area plus the expected maximum interference distance to detect interference. In the expected interference distance range, the robot performs deceleration stop, and if it enters the interference area, it performs an immediate stop without deceleration. If the robot moves at low speed and the controller-calculated expected distance is smaller than the 'expected maximum interference distance', it will not detect interference even if it is within the expected maximum interference distance.

 ![[Figure 7-23] Arm interference prevention conditions](../../_assets/7-23.png)


<br>

| Error Message | - W0147 Robot 0) expected arm interference and stopped  <br> - E0237 Robot 0) ARM interference area detected |
|:--|:--|
| Possible Causes | When a robot invades another robot's expected interference area during movement, the above warning and error messages may occur simultaneously and stop the robot. |
| Action | If the above warning occurs during normal program playback, re-check the work program. |

