## 4.3. cmov Command

<br>

```python
cmov {param1},{param2},{param3},{param4},{param5}

cmov R20,L,tg=po1,spd=60%,accu=0,tool=1
cmov R20,L,tg=po1,spd=60%,accu=0,tool=1 until di1
```


<br>

### Parameters
| param# | Meaning | 
| :--- | :--- | 
| param1| - Master robot system manipulator identifier <br> Format: R(#1)(#2) <br> #1 : Master robot system number (1~4) <br> #2 : Master manipulator identifier of the robot system <br> (0: Robot, 1: Positioner Group 1, 2: Positioner Group 2)| 
| param2 | - Interpolation type <br> Specifies the interpolation mode for the slave robot; only linear and circular are supported <br> (L: Linear, C: Circular)|
| param3 | - Movement speed (Speed) <Br> Specify the relative speed compared to the workpiece | 
| param4 | - Accuracy (0~7)|
| param5 | - Tool number (0~31) |


![[Figure 4-3] Method for distinguishing ID identifiers](../_assets/4-3.png)
