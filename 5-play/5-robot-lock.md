## 5.5. 로봇 락 기능(Robot Lock Playback)


『조건 설정』 → 『5: 로봇 Lock』을 <유효>로 설정합니다.  

 
<br>

![[그림 5-8] 로봇 lock 유효 설정  ](../_assets/5-8.png)

<br>


로봇 Lock을 선택하면 화면 상단의 메커니즘 창에 좌물쇠 표시가 나타납니다.  

<br>

![[그림 5-9] 로봇 lock 설정 확인  ](../_assets/5-9.png)

<br>


Master 로봇을 로봇 Lock <유효>로 설정하고 재생하면 Slave는 협조 동작을 수행하고 Master 로봇은 동작하지 않고 축 데이터 모니터는 변경됩니다.  


<br>

![[그림 5-10] 로봇 Lock 기능(Master Lock)   ](../_assets/5-10.png)

<br>


Slave 로봇을 로봇 Lock <유효>로 설정하고 Master 로봇을 <무효>로 설정한 경우 Master 로봇은 정상 동작하고 Slave 로봇은 정지한 채 모니터링 데이터만 움직입니다.  

<br>

![[그림 5-11] 로봇 Lock 기능(Slave Lock)     ](../_assets/5-11.png)

<br>

 

Master와 Slave를 모두 로봇 Lock <유효>로 설정하면 Master/Slave 모두 정지한 채 프로그램을 실행합니다.  
 
<br>

![[그림 5-12] 로봇 Lock 기능(Master, Slave Lock)     ](../_assets/5-12.png)

<br>



{% hint style="warning" %}

 -	협조 대기시간은 적당한 길이로 설정하십시오.
 - 	로봇 Lock <유효> 설정한 로봇은 움직이지 않으므로 다른 로봇과 간섭이 되지 않는 위치로 이동 후 프로그램을 실행하여 주십시오. 
 -	로봇 Lock 설정을 다시 <무효>로 변경 후 실행할 때는 로봇의 위치와 스텝의 위치가 대응하지 않으므로 프로그램 처음부터 실행시켜 주십시오. 

{% endhint %}