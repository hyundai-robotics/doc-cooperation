## 4.1.1. 함수의 파라미터


COWORK 함수는 프로그램에 함수로 기록되어 협조제어의 시작 및 종료를 표시하여 주고, 각 로봇의 MASTER 및 SLAVE를 지정하는 함수입니다.  

<br>

### 문법

```python
cowork {param1},{param2},{param3},{param4},{param5}

cowork m,id=0,s=2   
cowork s,m=1,id=0
cowork end
cowork with,sync=1
cowork m,id=.,s=[2,3,4],wait=5
```

<br>

### 파라미터
| param# | 의미 | 용례 |
| :--- | :--- | :--- |
| param1| - 자신의 로봇 역할 (MASTER/SLAVE) 지정 <br>- 협조 동작의 종료(end) 지정 <br> m: 마스터 <br> s: 슬레이브 <br> end : 협조동작의 종료 <br> with : 상대 로보과 위치 동기, sync 번호 동일| <br> <br> cowork m,s=... <br> cowork s,m=... <br> cowork end <br> cowork with, sync=1 |
| param2 | - 마스터 로봇 제어기가 마스터로 지정할 매니퓰레이터 ID번호  <br>  자신이 MASTER인 경우: 	 <br>ID = 0 은 로봇 매니퓰레이터 (이 때는 생략 파라미터 2를 가능) <br>  ID = 1 은 부가축으로 등록되어 있는 포지셔너 그룹 1 <br> (마스터 측에 부가축으로 포지셔너 그룹이 설정되어 있는 경우)|cowork m,id=1,s  <br> <br> <br>|
| param3 | - 상대의 로봇 번호 지정 <Br> 자신을 MASTER로 지정한 경우:   	 <br> 상대는 SLAVE가 되며, SLAVE의 로봇 번호를 지정(최대 3개) <br> 자신을 SLAVE로 지정한 경우:	<br> 상대는 MASTER가 되며, MASTER가 되는 로봇 번호를 지정 | cowork m,s=2,3,4 <Br> <Br>cowork s,m=1 |
| param4 | - 마스터 로봇 제어기에서 마스터로 지정할 매니퓰레이터 ID번호 <br> 자신이 SLAVE인 경우: <br> ID = 0 은 로봇 매니퓰레이터  <br>     ID = 1 은 부가축으로 등록되어 있는 포지셔너 그룹 1 <Br>  (마스터 측에 부가축으로 포지셔너 그룹이 설정되어 있는 경우)  | cowork s,m=1,id=0  <br> <br> <br>|
| param5 | - 협조상대 로봇 대기시간(Sec) < 0(무한대기) ~ 120 > <Br> 자신을 MASTER로 지정한 경우:  <br> SLAVE의 협조 기준위치로 올 때까지의 대기시간 <br> 자신을 SLAVE로 지정한 경우: 	 <br> MASTER의 협조 기준위치로 올 때까지의 대기시간  | cowork s,m=1,wait=30 <Br> <Br>cowork s,m=1,wait=30 |


