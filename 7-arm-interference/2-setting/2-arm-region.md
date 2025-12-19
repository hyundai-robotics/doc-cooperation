## 7.2.2. Setting Arm Interference Areas

The arm interference area model is a cylinder composed of hemispheres on both ends. For example, for the H-axis, you can model the radius from the H-axis joint position to the V-axis joint position as shown below.


<br>

![[Figure 7-10] Hemispherical and cylindrical arm interference area](../../_assets/7-10.png)

<br>

The cylindrical link model for the robot body arm applies to S, H, V, and B axes. The default radius values for each axis are determined as follows. If additional equipment is mounted on the robot, set the radius for the corresponding axis larger than the default value.

 - S-axis radius: Set to twice the distance from the S-axis rotation center to the H-axis joint
 - H-axis radius: 1.8 times the distance from the B-axis rotation center to the flange face
 - V-axis radius: Distance from the B-axis rotation center to the flange face

<br>

![[Figure 7-11] Axis-specific interference radius settings](../../_assets/7-11.png)

<br>

Currently, arm interference detection supports detecting all axes using the S, H, and V axis settings.

<br>

![[Figure 7-12] H-axis offset radius](../../_assets/7-12.png)

<br>

{% hint style="warning" %}
If you intend to set values smaller than the defaults, exercise extreme caution. For example, the H-axis of a serial-link robot such as the HS220 has an offset to the right from the S-axis center as shown in the figure. The H-axis interference detection area is set based on the segment from the S-axis rotation center along the H-axis link to the V-axis rotation center, so the H-axis radius must be set large enough to include the entire H-axis link from the S-axis rotation center.
{% endhint %}
