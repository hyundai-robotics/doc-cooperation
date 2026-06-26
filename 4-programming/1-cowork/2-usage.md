### 4.1.2. 如何使用 `cowork` 命令

(1) 在 MASTER 机器人上，`cowork ~ cowork end` 部分的动作被视为协作段命令。SLAVE 不能插入动作命令。

(2) 在 SLAVE 机器人上，标准的 `移动 (move)` 命令不能在协作部分使用；请改用 `cmov` 命令（协作移动）。

(3) 在处理从属跟随主控的应用程序时，如下面的示例，Slav会保持相对于主控的相对位置，并在执行 `cowork` 命令时相应移动，即使在 Slave 上没有插入 `cmov` 命令。

![](../../_assets/4-prg1.png)

(4) 在 Slave 上，您可以插入 `cmov` 命令，这些命令在 Master 末端执行器坐标系统中进行插值；`cmov` 记录的位置是相对于 Master 的工具末端执行器坐标系统的。如果像下面的示例那样教授，在 `cowork ~ cowork end` 内，Slave 执行协作运动，并沿着 Master 末端执行器坐标系统中记录的 `cmov` 路径跟随 Master 的运动。

![](../../_assets/4-prg2.png)

{% hint style="warning" %}

 - 必须在协作运动结束时插入 `cowork end` 命令。
 - 对于 SLAVE 机器人，不能在协作部分中插入 `移动 (move)` 命令；对于 MASTER 机器人，不能插入 `cmov` 命令。

{% endhint %}