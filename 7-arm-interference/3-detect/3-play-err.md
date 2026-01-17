## 7.3.3. Errors Occurring During Playback

When two robots move from S1 to S2 on a rail as shown below, if the S2 positions of the two robots are separated by more than the sum of the tool interference area and the expected maximum interference distance, no W0147 or E0237 will occur. This represents a normal program.

<br> 

![[Figure 7-25] Example of a normal program](../../_assets/7-25.png)

<br>

If, as in the figure below, the S2 point is slightly outside the configured tool interference area but within the expected maximum interference distance, an error (W0147 or E0237) may occur. In this case, adjust the expected maximum interference distance or change the teach points.

<Br>
 
![[Figure 7-26] Incorrect program example 1](../../_assets/7-26.png)

<br>
 
If the S2 point is taught so that it completely invades the defined tool interference area, an error (W0147 or E0237) will occur when the robots move to S2.


<br>

![[Figure 7-27] Incorrect program example 2](../../_assets/7-27.png)

<br>

In such cases, reduce the 'tool interference area' or the 'expected maximum interference distance' to prevent the error.


{% hint style="warning" %}

Setting the tool interference area too small—smaller than the actual tool—may cause collisions between robots.

{% endhint %}
