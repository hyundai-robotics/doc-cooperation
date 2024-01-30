4.3. CMOV 명령

<br>

```python
cmov {param1},{param2},{param3},{param4},{param5}

cmov R20,L,tg=po1,spd=60%,accu=0,tool=1
cmov R20,L,tg=po1,spd=60%,accu=0,tool=1 until di1
```



<br>

### 파라미터
| param# | 의미 | 
| :--- | :--- | 
| param1| - 마스터 로봇 시스템의 매니퓰레이터 식별자 <br> 형태: R(#1)(#2) <br> #1 : 마스터 로봇 시스템 번호 (1～4) <br> #2 : 로봇 시스템의 마스터 매니퓰레이터 식별자 <br> (0: Robot, 1: Positioner Group 1, 2: Positioner Group 2)| 
| param2 | - 보간 종류 (interpolation)  <br> 슬레이브 로봇의 보간 방식 지정, 직선과 원호만 가능 <br> (L: Linear, C: Circular)|
| param3 | - 보간 속도 (Speed) <Br> 작업물 대비 상대적인 속도 지정 | 
| param4 | - Accuracy (0~7)|
| param5 | - Tool 번호 (0~31) |


![[그림 4-3] ID 식별자 구분 방법](../_assets/4-3.png)