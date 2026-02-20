## 3.1. Switching Between Independent and Cooperative Modes

### 3.1.1. Mode switching by key operation

In manual mode, cooperative control operation mode can be changed as follows.

- ② Using R CODE
  
The operations are as shown in the table below.

| Key Operation | Mode Switch |
|:--:|:--:|
| R351 -> 0 | Manual Independent Mode(INDIVIDUAL) |
| R351 -> 1 | Manual Cooperative Mode, designate MASTER |
| R351 -> 2 | Manual Cooperative Mode, designate SLAVE |
| R351 -> 3 | cmov Recording Mode, designate SLAVE Jog Mode <br> (This mode can only be entered if the previous state was SLAVE) |

[Table 3-1] Mode switching by key operation  

### Manual Mode Independent (INDIVIDUAL) state
 
![[Figure 3-3] Manual Mode Independent state screen](../_assets/3-3.png)

<br>

   This state allows each robot to be jogged independently.	

 - Manual Mode Cooperative (MASTER designated) state
 
![[Figure 3-4] Manual Mode Cooperative Master state screen](../_assets/3-4.png)

<br>

   This is the state for synchronized operation according to the Master's movement when a Slave is designated.

 - Manual Mode Cooperative (SLAVE designated) state
 
![[Figure 3-5] Manual Mode Cooperative Slave state screen](../_assets/3-5.png)

<br>

    The state for the Slave to follow the Master's movement.


 - cmov Recording Mode, SLAVE Jog mode state
  

![[Figure 3-6] cmov Recording Mode state screen](../_assets/3-6.png)

<br>

In cmov recording mode, you can record cmov or verify taught positions using cmov step forward/back. Note that to record steps or move the robot, there must be a robot set as Master among the cooperative robots. The position recorded on the Slave is the relative position of the Slave robot based on the Master's end effector coordinate system.

<br>

{% hint style="warning" %}
 - Without a common coordinate system set, it is not possible to switch roles to Master or Slave from Manual Mode Independent state.
 - The R351,3 'cmov recording state' R CODE can only be entered from manual cooperative state (Slave designated mode) (R351,2).
 
{% endhint %}