## 9.1. Warning

<br>

---
- Code No.: W00123
- Warning: Robot stop requested
- Details: During cooperative control, a stop command was received from a partner robot. In this case, the above message is displayed and the robot stops.
- Action:
    - Start the Slave robot drive first, then start the Master drive to resume the program.

---
- Code No.: W00124
- Warning: Slave robot jog operation not allowed
- Details: The robot is set to manual cooperative Slave state. A robot configured as Slave cannot be operated independently.
- Action:
    - To operate each robot individually in manual mode, change the manual cooperative state to 'Independent'. The manual cooperative state can be changed using user keys or the R351 code.

---
- Code No.: W00131
- Warning: Cooperative jog operation not allowed - Duplicate Master robots
- Details: More than one robot connected on HiNet is set as manual cooperative Master.
- Action:
    - Only one manual cooperative Master can be set. Please change the settings.

---
- Code No.: W00132
- Warning: Cooperative jog operation not allowed - Slave selection unavailable
- Details: An attempt was made to jog the Master robot while the Slave robot was not set to a cooperative-ready state.
- Action:
    - Confirm that the Slave robot is selected, prepare the Slave robot for cooperation (Enabling Switch On), and then operate.
---

- Code No.: W00133
- Warning: Slave jog setting changed - Stop
- Details: During Master cooperative jog operation, a Slave robot that was operating together was detected to have its manual cooperative state changed.
- Action:
    - Re-check the Slave's cooperative state before operating.
---

- Code No.: W00134
- Warning: Master Tool coordinate system not selected
- Details: This occurs when attempting to jog a Slave robot in cmov recording mode (R351,3). A Master robot is not specified. It may also occur when using the cmov step forward function. The currently set Master number differs from the Master number recorded in cmov.
- Action:
    - Set the correct Master robot to Manual Cooperative Master state.
---
