## 3.1. 切换独立模式和协作模式

### 3.1.1. 通过按键操作切换模式

在手动模式下，可以按如下方式更改协作控制操作模式。

- ② 使用 R CODE
  
操作如下表所示。

| Key Operation | Mode Switch |
|:--:|:--:|
| R351 -> 0 | 手动独立模式(INDIVIDUAL) |
| R351 -> 1 | 手动协作模式，指定 MASTER |
| R351 -> 2 | 手动协作模式，指定 SLAVE |
| R351 -> 3 | cmov 记录模式，指定 SLAVE Jog 模式 <br> (此模式仅能在前一个状态为 SLAVE 时进入) |

[Table 3-1] 通过按键操作切换模式  

### 手动模式独立 (INDIVIDUAL) 状态
 
![[Figure 3-3] 手动模式独立状态屏幕](../_assets/3-3.png)

<br>

   此状态允许每个机器人独立地进行 jog。	

 - 手动模式协作 (指定为 MASTER) 状态
 
![[Figure 3-4] 手动模式协作主状态屏幕](../_assets/3-4.png)

<br>

   这是在指定 Slave 时，根据 Master 的运动进行同步操作的状态。

 - 手动模式协作 (指定为 SLAVE) 状态
 
![[Figure 3-5] 手动模式协作从状态屏幕](../_assets/3-5.png)

<br>

    让 Slave 跟随 Master 的运动的状态。


 - cmov 记录模式，SLAVE Jog 模式状态
  

![[Figure 3-6] cmov 记录模式状态屏幕](../_assets/3-6.png)

<br>

在 cmov 记录模式中，您可以记录 cmov 或使用 cmov 前进/后退确认授教位置。请注意，要记录步骤或移动机器人，必须在协作机器人中设定一个作为 Master 的机器人。记录在 Slave 上的位置是基于 Master 的末端执行器坐标系的相对位置。

<br>

{% hint style="warning" %}
 - 未设置公共坐标系统时，无法从手动模式独立状态切换角色为 Master 或 Slave。
 - R351,3 'cmov 记录状态' R CODE 仅能从手动协作状态 (指定为 Slave 模式) (R351,2) 进入。
 
{% endhint %}