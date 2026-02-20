### 7.2.1. 启用臂干扰预防

选择 'System' → '4: Application Parameters' → '17: Cooperative Control' → '4: Inter-robot Interference Prevention' → '1: Interference Prevention Conditions'。

<br> 

![[Figure 7-7] 臂干扰预防菜单](../../_assets/7-8.png) 

<br>

要启用臂干扰预防，请选择 'Interference Detection Partner Robot'。 '预期的最大干扰距离' 是系统预期干扰的臂干扰区域与该距离之间的距离，系统可以执行减速停靠。

<br> 

![[Figure 7-8] 臂干扰预防条件屏幕](../../_assets/7-9.png)

<br>

| 错误信息 | E0244 机器人 (0)的臂干扰检测不可用 |
|:--|:--| 
| 可能原因 | - 如果设定为干扰检测的合作控制的伙伴机器人在伙伴机器人上设定为 'Disabled'。 <br> - 伙伴机器人未参与合作控制网络。 <br> - 伙伴机器人未配置臂干扰预防条件。 <br> - 伙伴机器人的公共坐标系统未设定。 |
| 操作 | 检查您和伙伴机器人的合作控制状态、公共坐标设置、参与合作控制网络及干扰预防条件。 |