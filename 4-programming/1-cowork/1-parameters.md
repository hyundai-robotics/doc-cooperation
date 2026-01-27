### 4.1.1. Command Parameters

The `cowork` command marks the start and end of cooperative control in a program and specifies each robot's MASTER and SLAVE roles.

<br>

### Syntax

```python
cowork {param1},{param2},{param3},{param4},{param5}

cowork m,id=0,s=2   
cowork s,m=1,id=0
cowork end
cowork with,sync=1
cowork m,id=0,s=[2,3,4],wait=5
```

<br>

### Parameters
| param# | Meaning | Example |
| :--- | :--- | :--- |
| param1| - Designate your robot role (MASTER/SLAVE) <br>- Specify end of cooperative motion (end) <br> m: Master <br> s: Slave <br> end : End cooperative motion <br> with : Position synchronization with partner robot; sync number must match| <br> <br> `cowork m,s=...` <br> `cowork s,m=...` <br> `cowork end` <br> `cowork with, sync=1` |
| param2 | - Manipulator ID that the master robot controller designates as Master <br> If you are MASTER: <br> id = 0 indicates robot manipulator <br> id = 1 indicates the positioner group 1 registered as an auxiliary axis (if a positioner group is set as an auxiliary axis on the Master side)| `cowork m,id=1,s` <br> |
| param3 | - Specify partner robot number <Br> If you designate yourself as MASTER: <br> the partners become SLAVEs and their robot numbers are specified (up to 3) <br> If you designate yourself as SLAVE: <br> the partner becomes MASTER and specify the robot number of the MASTER | `cowork m,s=[2,3,4]` <Br> `cowork s,m=1` |
| param4 | - Manipulator ID that the Master robot controller designates as Master <br> If you are SLAVE: <br> id = 0 is robot manipulator <br> id = 1 is the positioner group 1 registered as an auxiliary axis (if a positioner group is set as an auxiliary axis on the Master side) | `cowork s,m=1,id=0` |
| param5 | - Partner robot wait time (sec) < 0 (infinite wait) ~ 120 > <Br> If you designate yourself as MASTER: <br> Wait time for SLAVEs to reach the cooperative reference position <br> If you designate yourself as SLAVE: <br> Wait time for MASTER to reach the cooperative reference position | `cowork s,m=1,wait=30` |
