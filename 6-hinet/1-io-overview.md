## 6.1. HiNet I/O Overview

HiNet I/O is a function that shares information between robots via the cooperative control network. Each controller monitors information from cooperative robots, so the sections set to be shared can be used freely. The maximum data size each controller can use is 12 bytes, and it can receive 36 bytes excluding its own portion.
 

![[Figure 6-1] HiNet Group Structure](../_assets/6-1.png)

This function can be used via the robot language (HRScript), allowing various applications that meet user needs.


![ ](../_assets/6-3.png) 

<br>

For example, if configured as below, when ROBOT 1 is the local robot, its information is set to fb7.dob0 ~ fb7.dob3, ROBOT2's information is received at fb7.dib4 ~ fb7.dib7, ROBOT3's information at fb7.dib8 ~ fb7.dib11, and ROBOT4's information at fb7.dib12 ~ fb7.dib15.

<If your robot is ROBOT 1>

| Robot No. | Start Signal | Byte Count | Note |
| :---: | :---: |  :---: | :---: | 
| ROBOT 1 | fb7.0 | 4 | Output (fb7.dob0 ~ fb7.dob3) |
| ROBOT 2 | fb7.32 | 4 | Input (fb7.dib4 ~ fb7.dib7) |
| ROBOT 3 | fb7.64 | 4 | Input (fb7.dib8 ~ fb7.dib11) |
| ROBOT 4 | fb7.96 | 4 | Input (fb7.dib12 ~ fb7.dib15) |


![[Figure 6-2] HiNet I/O Usage Example (Group 1 - 4 Robots) ](../_assets/6-2.png)
