## 5.4. Stop/Resume of Cooperative Playback

If the user inputs a stop command (external stop, internal stop) during cooperative motion, all robots engaged in cooperative motion will stop.


<br>

![[Figure 5-6] Warning displayed when a partner robot stops](../_assets/5-6.png)

<br>



After stopping during cooperative motion, changing the step number and replaying is only possible when cooperative playback is disabled. If you stop during cooperation, change the step, and then attempt to replay, a [Yes/No] confirmation is required from the user.

<br>

![[Figure 5-7] Message when changing step after stopping during cooperative motion](../_assets/5-7.png)

<br>

 

If a cooperative control state reset is input, it releases the cooperative state and operates. To operate while keeping the cooperative state, specify the stopped step number and start.
