## 7.2.1. Enabling Arm Interference Prevention

Select 'System' → '4: Application Parameters' → '17: Cooperative Control' → '4: Inter-robot Interference Prevention' → '1: Interference Prevention Conditions'.

<br> 

![[Figure 7-7] Arm Interference Prevention Menu](../../_assets/7-8.png) 

<br>

To enable arm interference prevention, select the 'Interference Detection Partner Robot'. The 'expected maximum interference distance' is the distance from the arm interference area at which the system expects interference and can perform deceleration stop.

<br> 

![[Figure 7-8] Arm Interference Prevention Conditions Screen](../../_assets/7-9.png)

<br>

| Error Message | E0244 Robot (0)'s arm interference detection is not possible |
|:--|:--| 
| Possible Causes | - If the cooperative control of the partner robot set for interference detection is set to 'Disabled' on the partner robot. <br> - The partner robot is not participating in the cooperative control network. <br> - The partner robot has not configured arm interference prevention conditions. <br> - The partner robot's common coordinate system is not set. |
| Action | Check your robot's and the partner robot's cooperative control status, common coordinate settings, participation in the cooperative control network, and interference prevention conditions. |
