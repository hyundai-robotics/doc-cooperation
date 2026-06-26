### 7.2.1. 启用机械臂干涉预防

选择 'System' → '4: Application Parameters' → '17: Cooperative Control' → '4: Inter-robot Interference Prevention' → '1: Interference Prevention Conditions'.

<br> 

![[Figure 7-7]机械臂干涉预防菜单](../../_assets/7-8.png) 

<br>

要启用机械臂干涉预防，选择 'Interference Detection Partner Robot'。 'expected maximum interference distance' 是系统预计干涉发生的机械臂干涉区域的距离，系统可以执行减速停车。

<br> 

![[Figure 7-8]机械臂干涉预防条件屏幕](../../_assets/7-9.png)

<br>

| 错误信息 | E0244 Robot (0)的机械臂干涉检测不可用 |
|:--|:--| 
| 可能原因 | - 如果设置为干涉检测的合作机器人在其上设置为 'Disabled'。 <br> - 合作机器人未参与合作控制网络。 <br> - 合作机器人尚未配置机械臂干涉预防条件。 <br> - 合作机器人的公共坐标系未设置。 |
| 操作 | 检查您的机器人及合作机器人的合作控制状态、公共坐标设置、参与合作控制网络以及干涉预防条件。 |