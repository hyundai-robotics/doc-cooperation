## 7.2.4. Arm Interference Status Monitoring

<Br>

![[Figure 7-21] Cooperative control monitoring](../../_assets/7-21.png)


<br>

You can check the arm interference state in 'Cooperative Control Monitoring'. The arm interference state displays the potential interference axis and the interference distance.

 - Potential Interference Axis: The axis of your robot that has the smallest distance to the partner robot
 - Interference Distance [mm]: Distance between potential interference axes
      - Display range: 10 times the expected maximum interference distance (if expected maximum interference distance is 0, display range is 1000 mm)
      - If interference distance exceeds the display range, it is shown as ----.

If the monitored arm interference state differs from the actual state, check the cooperative control common coordinate system and the arm interference detection configuration.
