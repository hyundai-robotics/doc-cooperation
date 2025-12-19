## 9.3. Operation Error

---

- Code No.: E01340
- Error: Inappropriate robot cooperation conditions (WD, common coordinate)
- Details: The controller is configured in a state unsuitable for executing the cowork command.
- Action:
    - Check that communication status is normal, verify that the partner's common coordinate system is set, and confirm the manual cooperative state matches the robot role required by the cowork command.
---

- Code No.: E01341
- Error: Cooperative playback wait time exceeded
- Details: In the cowork command, the waiting time for partner robots to become ready for cooperation exceeded the time set in the command.
- Action:
    - Set the wait time considering the time required for all cooperative robots to reach the cooperation positions.
    - If set to 0, it will wait indefinitely until all robots are ready for cooperation.

---

- Code No.: E01342
- Error: Robot cooperation state or common coordinate invalid
- Details: The robot cooperation state is invalid or the common coordinate system is not set, so the cowork command cannot be executed.
- Action:
    - In System → Control Parameters → Network → Service → Cooperative Control dialog, set the cooperative control function to <Enabled> and then set the common coordinate system.
---

- Code No.: E01343
- Error: cowork function execution mismatch
- Details: This occurs when the cowork command was executed redundantly or the program ended without a cowork end command.
- Action:
    - Program so that cowork and cowork end commands are paired.
    - When re-executing the cowork command after a step change, initialize the cooperative control state.

---

- Code No.: E01344
- Error: cowork parameter (m/s, robot number) error
- Details: The partner robot number in the cowork command is incorrectly set to the robot's own number.
- Action:
    - Change the robot number in the cowork command to the partner robot number.
---

- Code No.: E01345
- Error: Slave robot is already in cooperative state
- Details: The Slave robot is cooperating or stopped at the cowork end position.
- Action:
    - Do not perform artificial step changes to ensure normal cooperative operation between Master and Slave.
---

- Code No.: E01355
- Error: Cooperative partner robot fault - Stopped
- Details: The cooperative partner robot is stopped in a state where cooperative motion is not possible. It stops because cooperative motion cannot be performed.
- Action:
    - Confirm that the operation modes among robots are the same.
    - If restarting after a stop during cooperative motion, start the Slave first and then the Master.
---
