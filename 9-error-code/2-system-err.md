## 9.2. System Error

---

- Code No.: E00200
- Error: Exceeded maximum speed during cooperative motion
- Details: A command that exceeds the robot's maximum speed was received while following cooperative motion.
- Action:
    - For the Slave performing cooperative motion, change the robot posture at the reference position, modify the recorded cooperative positions, or lower the recorded speed and replay.
---

- Code No.: E00201
- Error: Cooperative motion start error
- Details: There is an error in sending/receiving synchronization signals among cooperative robots. The playback modes are different.
- Action:
    - Check communication status. Match the playback modes of the cooperative robots and then start cooperative motion.
---

- Code No.: E00203
- Error: Cooperative partner robot fault - Emergency stop
- Details: During cooperative motion, the partner robot's drive-ready state turned Off. The operation is stopped with drive-ready Off.
- Action:
    - Resolve the cause of the partner robot's stop, set drive-ready On, and restart.
---

- Code No.: E00204
- Error: Robot cooperative control communication error
- Details: A communication error occurred with a partner robot during cooperative jog or playback.
- Action:
    - Check the cooperative control communication cables and connector connections.
---

- Code No.: E00227
- Error: Cooperative control synchronization sequence error
- Details: A sequence difference occurred between the master robot and slave robot commands during cooperative control.
- Action:
    - Check the cooperative control communication cables and connector connections.
---
