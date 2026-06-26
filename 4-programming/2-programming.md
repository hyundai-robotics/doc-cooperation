## 4.2. 教授和编写协作处理程序

(1) 操作员的数量必须与协作机器人数量相等；因此，每个操作员为每个被协作的机器人参与。

(2) 验证协作机器人公共坐标系统是否已配置。

(3) 将 MASTER 和 SLAVE 机器人移动到各自的合作起始位置，并将起始位置记录为参考。

![](../_assets/4-prg3.png)

<br>

![[Figure 4-1] 记录协作运动起始参考位置](../_assets/4-1.png)

<br>

(4) 通过输入 R351 代码为 MASTER 和 SLAVE 机器人分配机器人角色。

(5) 注册协作控制启动命令 (`cowork m/s`)。`cowork` 命令指定 Master/Slave 并分配 Slave/Master 编号。只能设置一个 Master，并且最多可以指定三个 Slaves。

![](../_assets/4-prg4.png)

(6) 通过慢移 (JOG) 操作 MASTER 机器人。Slave 相对跟随 Master 工具尖端的位置。在协作慢移过程中，Slave 必须按下启用开关。仅在 Master 上记录步态位置；不要在 Slave 控制器上记录。

![](../_assets/4-prg5.png)

![[Figure 4-2] MASTER 机器人操作](../_assets/4-2.png)

(7) 在 MASTER 上记录协作运动步骤。设置 Master's 插值类型和速度。在协作运动命令中使用标准 `移动 (move)` 命令（不能使用 cmov）。

![](../_assets/4-prg6.png)

(8) 当协作运动完成后，在 Master 和 Slave 上插入 `cowork end` 命令以结束协作控制。

![](../_assets/4-prg7.png)

<br>

{% hint style="warning" %}
	在手动协作操作期间，不要将 Slave 的启用开关更改为 OFF。硬件信号优先于通信，可能导致协作机器人之间的位置不匹配。在严重情况下，这可能导致工件或机器人手的损坏。

{% endhint %}