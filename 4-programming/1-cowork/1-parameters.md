### 4.1.1. 命令参数

The `cowork` command marks the start and end of cooperative control in a program and specifies each robot's MASTER and SLAVE roles.

<br>

### 语法

```python
cowork {param1},{param2},{param3},{param4},{param5}

cowork m,id=0,s=2   
cowork s,m=1,id=0
cowork end
cowork with,sync=1
cowork m,id=0,s=[2,3,4],wait=5
```

<br>

### 参数
| param# | 含义 | 示例 |
| :--- | :--- | :--- |
| param1| - 指定您的机器人角色 (MASTER/SLAVE) <br>- 指定合作运动的结束 (end) <br> m: 主控 <br> s: 从控 <br> end : 结束合作运动 <br> with : 与合作机器人位置同步；同步编号必须匹配| <br> <br> `cowork m,s=...` <br> `cowork s,m=...` <br> `cowork end` <br> `cowork with, sync=1` |
| param2 | - 主控机器人控制器指定的操纵器ID <br> 如果您是 MASTER: <br> id = 0 表示机器人操纵器 <br> id = 1 表示注册为辅助轴的定位器组1 (如果在主控侧设置为辅助轴)| `cowork m,id=1,s` <br> |
| param3 | - 指定合作机器人编号 <Br> 如果您指定自己为 MASTER: <br> 合作伙伴成为 SLAVES，并指定其机器人编号（最多3个） <br> 如果您指定自己为 SLAVE: <br> 合作伙伴成为 MASTER，并指定 MASTER 的机器人编号 | `cowork m,s=[2,3,4]` <Br> `cowork s,m=1` |
| param4 | - 主控机器人控制器指定的操纵器ID <br> 如果您是 SLAVE: <br> id = 0 是机器人操纵器 <br> id = 1 是注册为辅助轴的定位器组1 (如果在主控侧设置为辅助轴) | `cowork s,m=1,id=0` |
| param5 | - 合作机器人等待时间 (秒) < 0 (无限等待) ~ 120 > <Br> 如果您指定自己为 MASTER: <br> 等待 SLAVES 到达合作参考位置的时间 <br> 如果您指定自己为 SLAVE: <br> 等待 MASTER 到达合作参考位置的时间 | `cowork s,m=1,wait=30` |