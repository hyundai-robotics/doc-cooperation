## 2.4.1. Overview of Common Coordinate System Settings

To perform cooperative operations, the relative positions between robots must be known accurately. The robot controller computes the tool tip position with respect to each robot's base coordinate frame, and additional information about the other robots must be registered. The positional relationship between robots is established by configuring a common coordinate system.

To mutually recognize the positions of Robot 1 and Robot 2, a common coordinate system is set (Figure 2.4). The setup is performed by teaching three identical points in space on each robot.

![[Figure 2-4] Common coordinate system setup between cooperative robots](../../_assets/2-4.png)

{% hint style="warning" %}
- Perform robot calibration before setting the common coordinate system.

{% endhint %}