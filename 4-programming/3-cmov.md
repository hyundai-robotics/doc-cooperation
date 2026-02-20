## 4.3. cmov 命令

<br>

```python
cmov {param1},{param2},{param3},{param4},{param5}

cmov R20,L,tg=po1,spd=60%,accu=0,tool=1
cmov R20,L,tg=po1,spd=60%,accu=0,tool=1 until di1
```


<br>

### 参数
| param# | 意义 | 
| :--- | :--- | 
| param1| - 主机器人系统操作器标识符 <br> 格式：R(#1)(#2) <br> #1 : 主机器人系统编号 (1~4) <br> #2 : 机器人系统的主操作器标识符 <br> (0: 机器人, 1: 定位器组 1, 2: 定位器组 2)| 
| param2 | - 插值类型 <br> 指定从属机器人的插值模式；仅支持线性和圆形插值 <br> (L: 线性, C: 圆形)|
| param3 | - 运动速度 (速度) <Br> 指定相对于工件的相对速度 | 
| param4 | - 精度 (0~7)|
| param5 | - 工具编号 (0~31) |


![[图 4-3] 区分 ID 标识符的方法](../_assets/4-3.png)