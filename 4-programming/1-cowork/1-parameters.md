### 4.1.1. 命令参数

`cowork` 命令标记程序中协作控制的开始和结束，并指定每个机器人的 MASTER 和 SLAVE 角色。

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
| param1| - 指定你的机器人角色（MASTER/SLAVE） <br>- 指定协作运动的结束（end） <br> m: 主机 <br> s: 从机 <br> end : 结束协作运动 <br> with : 与伙伴机器人位置同步；同步编号必须匹配 | <br> <br> `cowork m,s=...` <br> `cowork s,m=...` <br> `cowork end` <br> `cowork with, sync=1` |
| param2 | - 主管机器人控制器指定的操控器 ID <br> 如果你是 MASTER: <br> id = 0 表示机器人操控器 <br> id = 1 表示注册为辅助轴的定位器组 1（如果在主侧将定位器组设置为辅助轴） | `cowork m,id=1,s` <br> |
| param3 | - 指定合作伙伴机器人编号 <br> 如果你自己指定为 MASTER: <br> 合作伙伴成为 SLAVES，并指定它们的机器人编号（最多 3 个） <br> 如果你自己指定为 SLAVE: <br> 合作伙伴成为 MASTER，并指定 MASTER 的机器人编号 | `cowork m,s=[2,3,4]` <br> `cowork s,m=1` |
| param4 | - 主管机器人控制器指定的操控器 ID <br> 如果你是 SLAVE: <br> id = 0 是机器人操控器 <br> id = 1 是注册为辅助轴的定位器组 1（如果在主侧将定位器组设置为辅助轴） | `cowork s,m=1,id=0` |
| param5 | - 合作伙伴机器人等待时间（秒） < 0（无限等待） ~ 120 > <br> 如果你自己指定为 MASTER: <br> SLAVES 到达协作参考位置的等待时间 <br> 如果你自己指定为 SLAVE: <br> MASTER 到达协作参考位置的等待时间 | `cowork s,m=1,wait=30` |