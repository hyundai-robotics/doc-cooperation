### 2.4.4. Common Coordinate System Setup

If a common coordinate system is not set, manual cooperative jog operations and cooperative replay are not possible. When the common coordinate system is set, it is recommended to verify the setup using cooperative jog operations before proceeding with full operations.

The common coordinate system setup requires accurate knowledge of the robots' tool-tip positions. Otherwise, synchronization position errors may occur during cooperative control between robots. Therefore, calibration is required to set the robot origins and the exact tool positions. The ${cont_model} controller provides an automatic calibration function when a 3D position measurement device is not available (System → 6: Automatic Calibration → 1: Axis Origin and Tool Length Optimization). If a 3D position measurement device is available, more accurate calibration is possible; in that case, use the 9: Robot and Tool Calibration function. For more details, refer to the ${cont_model} operation manual.

- Example of common coordinate system setup for a two-robot environment (ROBOT1, ROBOT2)

    - ① Select the program number for common coordinate system setup on both ROBOT1 and ROBOT2 controllers.
    - ② Jog ROBOT1 and ROBOT2 and sequentially record three points in steps 1, 2, and 3 to form as large a triangle as possible. The recorded positions must correspond to the same spatial points; interpolation method and speed do not matter, but choose a tool number whose tool tip position is known accurately.
    - ③ In Manual mode, select System → 4: Application Parameters → 3: Common Coordinate Setup.
    - ④ In Automatic Calculation, enter the program number used for common coordinate setup.
    - ⑤ The execution result displays the common coordinate system position and orientation as seen from the robot base.
    - ⑥ Press the Confirm key to complete the setup.

![[Figure 2-7] Per-robot program for common coordinate setup](../../_assets/2-7.png)

![[Figure 2-8] Teaching method for common coordinate setup](../../_assets/2-8.png)

![[Figure 2-9] Common coordinate setup result screen](../../_assets/2-9.png)

{% hint style="warning" %}
- Enter either the correct tool specifications or obtain tool data using automatic calibration for common coordinate setup. It is recommended that each point be recorded with the same robot posture.
- Record the three points so they form as large a triangle as possible. If the points are too close or nearly collinear, errors may occur.
- The orientation transformation of the common coordinate system Rx, Ry, Rz relates to the robot coordinate system as follows:

    - ① Rotate your robot (number 2) coordinate frame (ref) around the X-axis by γ.
    - ② Rotate your robot (number 2) coordinate frame (ref) around the Y-axis by β.
    - ③ Rotate your robot (number 2) coordinate frame (ref) around the Z-axis by α.
    - ④ The pose obtained by rotating your robot (number 2) base coordinate frame by γ, β, α is the orientation of the common coordinate system in space.

![[Figure 2-10] Orientation transformation of the common coordinate system](../../_assets/2-10.png)

{% endhint %}