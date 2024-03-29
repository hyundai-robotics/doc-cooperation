﻿## 7.3.3. 재생 동작 중 에러가 발생하는 경우




아래 그림과 같이 두 로봇이 주행축 위의 S1에서 S2로 각각 이동하는 경우 두 로봇의 S2위치가 툴 간섭영역과 간섭 예상 최대거리를 합한 것 보다 떨어져 있는 경우 W0147이나 E0237이 발생하지 않습니다. 이러한 작업 작업프로그램이 정상적인 경우입니다.

<br> 

![[그림7-25] 정상적인 작업 프로그램의 예](../../_assets/7-25.png)

<br>

아래의 그림과 같이 설정한 툴 간섭영역과는 약간 떨어져 있으나 간섭 예상 최대 거리 이내에 S2가 교시되어 있는 경우입니다. 이 경우 에러(W0147이나 E0237)가 발생하므로 간섭 예상 최대거리를 조정하거나 교시점을 바꿔주십시오.

<Br>
 
![[그림7-26] 잘못된 프로그램 예1](../../_assets/7-26.png)

<br>
 
아래의 그림과 같이 설정한 툴 간섭영역을 완전히 침범하도록 S2를 교시한 경우에는 로봇이 서로 S2로 이동할 때 에러(W0147이나 E0237)가 발생합니다.


<br>

![[그림7-27] 잘못된 프로그램 예2](../../_assets/7-27.png)

<br>

상기와 같은 경우 ‘툴 간섭 영역’을 축소하거나 ‘간섭 예상 최대 거리’를 축소하여 에러가 발생하지 않도록 조치할 수 있습니다. 


{% hint style="warning" %}

툴 간섭 영역을 너무 축소해서 실제 툴 보다 작게 설정하면 로봇 간에 충돌이 발생할 수 있습니다. 

{% endhint %}
