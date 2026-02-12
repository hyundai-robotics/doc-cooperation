
[__SOURCE](README.md)
# ${cont_model} Controller Function Manual - Cooperative Control

[__SOURCE](1-intro/README.md)
# 1. Overview

[__SOURCE](1-intro/1-overview.md)
## 1.1. Overview of Robot Cooperative Features

<br>

{% hint style="info" %}
A separate license is required to use this feature; please contact us. <br>
This feature is supported from V60.26-00.
{% endhint %}

<br>

Robot cooperative features enable multiple robots to perform tasks that a single robot cannot accomplish.

This feature applies in cases such as:

- When two robots with simple hands cooperate to handle a workpiece
- When a workpiece is too large to be handled by a single robot
- When a Master robot handles the workpiece while a Slave performs jigless tasks such as arc welding or sealing on the workpiece
 
This feature allows synchronization of up to 4 robots.
Each robot can perform independent tasks and cooperative tasks within a single program.


<br>

![[Figure 1.1] Robot cooperative features](../_assets/1-1.png)

[__SOURCE](1-intro/2-main-func/README.md)
## 1.2. Main Features

[__SOURCE](1-intro/2-main-func/1-specs.md)
### 1.2.1. Key Feature Specifications

<br>

| Key Feature Specification | Remarks | 
| :---: | :---: | 
| Number of cooperative robots | Up to 4 |
| Communication method | General Ethernet (UDP) |
| Communication speed | 100 Mbps |
| Number of Masters supported | 1 |
| Number of Slaves supported | Up to 3 Slaves per Master |
| Drive Axis | Drive axis cooperation supported |
| HiNet I/O | 12 bytes per robot (I/O signals) |
| Jigless cooperation | Supports jigless cooperation between robot and positioner |

[Table 1-1] Cooperative control specifications


<br>

![[Figure1-2] Jigless cooperative control](../../_assets/1-2.png)
[__SOURCE](1-intro/2-main-func/2-features.md)
### 1.2.2. Feature Characteristics

- Communication
  The cooperative control feature uses UDP (General Ethernet) communication to coordinate up to 4 robots.

- Common Coordinate System between Robots
  Provides a function to determine relative positions between robots. The common coordinate system is obtained by teaching the same three points in the workspace on each robot.

- Manual Mode Cooperative Operation
  Allows users to easily teach in manual mode. After assigning Master and Slave roles for each robot, handling applications can be taught by operating only the MASTER. For jigless cooperation, the Slave's positions can be taught relative to the Master's workpiece.

- Positioner Master Support
  You can assign a positioner as the Master robot, enabling cooperative control. Up to 4 robots can cooperate with a positioner simultaneously.

- Teaching
  Each controller needs an independent program. Split a program into parts for independent robot actions and cooperative actions to enable flexible and easy programming.

- Cooperative Playback
  According to the `cowork` command, the system waits for partner robots to be ready and begins cooperation when all robots are ready.

- HiNet I/O
  Provides the capability to share your robot's information with other cooperative robots using I/O signals so that robot states can be checked without a separate interlock control panel.
[__SOURCE](1-intro/3-operation-seq.md)
## 1.3. Operation Sequence

This section describes the sequence for using cooperative robot features. Detailed instructions are provided in subsequent sections.

- (1) Robot Calibration
Ensure each robot's axis origin and tool data are correctly set for cooperative control. See the automatic calibration feature for details.

- (2) Hardware Installation
Connect hardware required for the controller's communication. Connect the network hub and Ethernet cable.

- (3) Control Environment Settings
Set whether to use cooperative control for your robot and assign the robot number.

- (4) Communication Settings
Set network IP addresses for cooperative robots. To use HiNet I/O, set the start index and byte count for input/output signals. Your robot's signals are outputs and partner robots' signals are inputs.

- (5) Common Coordinate System Setup
Perform calibration to provide relative positional information between cooperative robots.

- (6) Teaching
Use R351 (Manual Cooperative State Setting) to assign Master and Slave roles and teach cooperative motions by operating the Master robot.

- (7) Operation Check
Verify cooperative motion in manual mode. Start cooperative robots by stepping forward simultaneously.

- (8) Continuous Operation
Switch to automatic mode. Place the program at the lead step and press the start switches on all controllers designated as cooperative robots.

[__SOURCE](2-system-setting/README.md)
# 2. System Settings

[__SOURCE](2-system-setting/1-install/README.md)
## 2.1. Hardware Installation

[__SOURCE](2-system-setting/1-install/1-wiring.md)
### 2.1.1. Emergency Stop Wiring

If an emergency stop occurs during cooperative motion, robots monitor each other's state via communication so that partner robots also stop, but hardware signals take precedence and positional mismatches between cooperative robots may occur. To minimize cooperative position mismatches during emergency stop, wire the controller's external emergency stop.

The ${cont_model} controller provides a user external emergency stop. The external emergency stop wiring is shown below.

When using the robot cooperative feature, install a dedicated emergency stop switch so that emergency stop signals can be input to each controller simultaneously. Use the user-provided external emergency stop wiring to integrate them into a single emergency stop as shown below. This minimizes cooperative position mismatches during an emergency stop.

<br>

![[Figure 2-1] Emergency stop wiring for robot cooperation](../../_assets/2-1.png)


<br>

{% hint style="warning" %}
- A positional mismatch during cooperative motion may occur when an emergency stop happens.
- For handling applications, install a floating mechanism to absorb cooperative mismatches during cooperative motion (errors on emergency stop, synchronization errors, calibration errors, trajectory errors).
- For handling applications with 2 cooperative robots, it is recommended to install at least one floating mechanism.
- Use a Safety Relay when using external emergency stop relays.
    Example product: Omron G7S-4A2B

{% endhint %}

[__SOURCE](2-system-setting/1-install/2-network-config.md)
### 2.1.2. Network Configuration

<br>

| Component | Specification | 
| :---: | :---: | 
| ${cont_model}COM | Main CPU board | 
| UTP cable | Hub connection: direct LAN cable <br> Direct connection of two units: cross LAN cable |
| Network Hub | Company-specified switching hub |


[Table 2-1] Cooperative control requirements


<br>

- Connection method
Connect one of the COM module's network sockets (LAN 1-3) to the general-purpose network using a UTP cable (direct), and connect the other end to the network hub. Up to 4 units can be connected to the hub this way.
If connecting two robots without a hub, use a network UTP CROSS cable and connect it to the universal network sockets.

[__SOURCE](2-system-setting/1-install/3-net-check.md)
### 2.1.3. Network Connection Check

Check the network when the following situations occur:
- During initial installation
- When a network anomaly is detected during cooperative control operation

<br>
<br>

- Check items:
    - Verify the network cable connection.
    - The ${cont_model}COM network socket LED should be blinking green.
    - Verify cable integrity.
    - Check network status in [Inter-robot Cooperative Control] monitoring.

<br>

![[Figure 2-2] Cooperative control status check](../../_assets/2-2.png)

<br>

{% hint style="warning" %}
- It is recommended that the cooperative control network be configured separately and independently from other networks.

{% endhint %}

[__SOURCE](2-system-setting/2-ctrl-setting.md)
## 2.2. Control Environment Settings

Set whether to use the cooperative control function and the robot number, etc.

(1) Select 'System' → '4: Application Parameters' → '17: Cooperative Control'.

(2) Select '1: Control Environment Settings'.

(3) Set the dialog parameters. The purpose of each parameter is as follows:

- Cooperative Control Function: <Disabled, Enabled>
Select whether to use the cooperative control function.
- Robot Number: <1~4>
Set the robot number. The robot number is the identifier for your controller on the cooperative control network. The ${cont_model} controller supports a maximum of 4 robots in a cooperative network. Ensure robot numbers are not duplicated.

<br>

![[Figure 2-11] Control environment settings](../_assets/2-11.png)


<br>

{% hint style="warning" %}
- For special robots and robots with fewer than 6 degrees of freedom, only HiNet communication is applicable and the `cowork` command cannot be used.
- Cooperative control is an optional feature. Therefore, a license key registration is required to use this function. A temporary key can be issued for one month; for continued use beyond that, contact the company.

<br>

![[Figure 2-3] Cooperative control license key option settings](../_assets/2-3.png)

{% endhint %}
[__SOURCE](2-system-setting/3-comm-setting.md)
## 2.3 Communication Settings

Set the network IP addresses for cooperative control and the information for HiNet I/O usage.

(1) Select 'System' → '4: Application Parameters' → '17: Cooperative Control'.

(2) Select '2: Communication Settings'.
- Add robots using the "+" button for the number of robots to be cooperated. (For example, if the number of cooperative robots is 3, robot1, robot2, robot3 should be equally added on all robots as shown below.)

(3) Set the dialog parameters. Each parameter's purpose is as follows:

- IP Address: Set network IP addresses for each cooperative robot. (For example, if robot1=192.168.1.150, robot2=192.168.1.151, robot3=192.168.1.152, set the same on all robots.)
- HiNet I/O: Set the start index and byte count for input/output signals.
HiNet I/O transmits your robot's information to other cooperative robots to check robot states without a separate interlock control panel; your robot info is used as output signals and other cooperative robots' info as input signals. (For example, robot1=fb7.0 with byte count 4, robot2=fb7.32 with byte count 4, robot3=fb7.64 with byte count 4; set the same on all robots. For more details, see "[6. HiNet I/O Features](../6-hinet/1-io-overview.md)")
<br>

![[Figure 2-12] Usage settings](../_assets/2-12.png)

<br>
[__SOURCE](2-system-setting/4-coordinate/README.md)
## 2.4. Common Coordinate System Settings

[__SOURCE](2-system-setting/4-coordinate/1-setting-outline.md)
### 2.4.1. Overview of Common Coordinate System Settings

To perform cooperative operations, the relative positions between robots must be known accurately. The robot controller computes the tool tip position with respect to each robot's base coordinate frame, and additional information about the other robots must be registered. The positional relationship between robots is established by configuring a common coordinate system.

To mutually recognize the positions of Robot 1 and Robot 2, a common coordinate system is set (Figure 2.4). The setup is performed by teaching three identical points in space on each robot.

![[Figure 2-4] Common coordinate system setup between cooperative robots](../../_assets/2-4.png)

{% hint style="warning" %}
- Perform robot calibration before setting the common coordinate system.

{% endhint %}
[__SOURCE](2-system-setting/4-coordinate/2-common-coord.md)
### 2.4.2. Setting a Common Coordinate System for Two or More Robots

A common coordinate system for cooperative robots is defined by teaching identical points between robots, so all cooperating robots must be able to indicate the same three points. Therefore, when the distance between robots is large, it may not be possible to set a common coordinate system. In such cases, a separate tool should be fabricated so that identical points between the robots can be taught.

![[Figure 2-5] Setting a common coordinate system for two or more robots](../../_assets/2-5.png)

[__SOURCE](2-system-setting/4-coordinate/3-base-axis.md)
### 2.4.3. Travel-Axis System

When configuring the travel-axis system for cooperative control, install travel axes with the same specifications as parallel as possible.

![[Figure 2-6] Travel-axis system configuration for cooperative control](../../_assets/2-6.png)

{% hint style="warning" %}
- Systems with travel axes should set the travel-axis specification to 'arbitrary' and perform travel-axis calibration before use.
- Install the travel axes of cooperative robots as parallel as possible.
- Large synchronization errors during travel-axis movement may be caused by inaccurate travel-axis calibration.
- For details about the travel-axis calibration function, refer to the '${cont_model} controller operation manual'.
- Travel-axis calibration should be performed for both MASTER and SLAVE.

{% endhint %}
[__SOURCE](2-system-setting/4-coordinate/4-common-coord-set.md)
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
[__SOURCE](3-manual-mode/README.md)
# 3. Manual Mode Cooperative Operation

[__SOURCE](3-manual-mode/1-mode-switch.md)
## 3.1. Switching Between Independent and Cooperative Modes

### 3.1.1. Mode switching by key operation

In manual mode, cooperative control operation mode can be changed as follows.

- ② Using R CODE
  
The operations are as shown in the table below.

| Key Operation | Mode Switch |
|:--:|:--:|
| R351 -> 0 | Manual Independent Mode(INDIVIDUAL) |
| R351 -> 1 | Manual Cooperative Mode, designate MASTER |
| R351 -> 2 | Manual Cooperative Mode, designate SLAVE |
| R351 -> 3 | cmov Recording Mode, designate SLAVE Jog Mode <br> (This mode can only be entered if the previous state was SLAVE) |

[Table 3-1] Mode switching by key operation  

### Manual Mode Independent (INDIVIDUAL) state
 
![[Figure 3-3] Manual Mode Independent state screen](../_assets/3-3.png)

<br>

   This state allows each robot to be jogged independently.	

 - Manual Mode Cooperative (MASTER designated) state
 
![[Figure 3-4] Manual Mode Cooperative Master state screen](../_assets/3-4.png)

<br>

   This is the state for synchronized operation according to the Master's movement when a Slave is designated.

 - Manual Mode Cooperative (SLAVE designated) state
 
![[Figure 3-5] Manual Mode Cooperative Slave state screen](../_assets/3-5.png)

<br>

    The state for the Slave to follow the Master's movement.


 - cmov Recording Mode, SLAVE Jog mode state
  

![[Figure 3-6] cmov Recording Mode state screen](../_assets/3-6.png)

<br>

In cmov recording mode, you can record cmov or verify taught positions using cmov step forward/back. Note that to record steps or move the robot, there must be a robot set as Master among the cooperative robots. The position recorded on the Slave is the relative position of the Slave robot based on the Master's end effector coordinate system.

<br>

{% hint style="warning" %}
 - Without a common coordinate system set, it is not possible to switch roles to Master or Slave from Manual Mode Independent state.
 - The R351,3 'cmov recording state' R CODE can only be entered from manual cooperative state (Slave designated mode) (R351,2).
 
{% endhint %}
[__SOURCE](3-manual-mode/2-operation.md)
## 3.2. Manual Mode Cooperative Operation
### 3.2.1. Setting MASTER and SLAVE Robots

Use R351 to set robot roles to MASTER and SLAVE. The robot role is independent of the robot number.

 

![[Figure 3-7] Manual mode cooperative operation (Setting Master and Slave robots)](../_assets/3-7.png)

<br>
         
 - ① Confirm that both MASTER and SLAVE robots are in 'Manual Mode'.
 - ② Ensure both MASTER and SLAVE robots have Drive Ready ON and are in standby.
 - ③ Keep the Slave robot's ENABLE switch held so that Drive Ready ON is maintained, and confirm that the MASTER's Drive Ready is also ON.
 - ④ When the MASTER robot is operated, the SLAVE robot follows by tracking the relative position.

 
![[Figure 3-8] Manual mode cooperative operation (Master operation / Slave following)](../_assets/3-8.png)

<br>

{% hint style="warning" %}
 - Manual cooperative JOG is not possible in the following cases:
    - When more than one Master is designated and operated
    - When attempting to operate a robot set as Slave
    - When the Enable switches of Master or Slave are not pressed
    - When the inter-robot cooperative coordinate system is not configured
    - When cooperative control communication between robots is disconnected

 - In Manual Mode cooperative operation, JOG is not permitted on robots set as Slave. To jog a Slave, change the robot role to Manual Mode Independent.

 - If cooperative control is <Disabled>, the I:R# / S:R# / M:R# indicators will not appear at the top of the Manual Mode screen and cannot be configured, therefore Manual cooperative JOG is not possible.
{% endhint %}

[__SOURCE](3-manual-mode/3-jog.md)
## 3.3. Cooperative Drive Axis Jog

Cooperative drive axis jogging is operated the same way as standard cooperative jogging. As shown in Figure 3-5, when operating the Master drive axis in cooperative jog state, the Slave's drive axis moves compensating the relative position.

 
![[Figure 3-9] Cooperative drive axis jog](../_assets/3-9.png)

<br>

{% hint style="warning" %}
 - The drive axes of cooperative control systems should be installed as parallel as possible between Master and Slave.  
- Cooperative control drive axis systems support only a single axis.   
- To use cooperative drive axis functionality, perform drive axis calibration first.  
{% endhint %}

[__SOURCE](3-manual-mode/4-cmov.md)
## 3.4. cmov Recording Mode Jog

The cmov recording mode is a mode for teaching Slave positions for jigless cooperative motion.

 - How to set cmov recording mode:
    - ① Select the robot role as Slave.
    - ② Set the Master's manual cooperative state to MASTER.
    - ④ Even in Cartesian coordinate jog state, jogging is performed relative to the robot's Cartesian coordinate system regardless of the Master coordinates.

<Br>

![[Figure 3-10] cmov recording mode jog](../_assets/3-10.png)

<br>
 
<br>

 {% hint style="warning" %}
- The drive axes of cooperative control systems should be installed as parallel as possible between Master and Slave.
- When the Slave is in cmov recording mode, jogging of the robot set as Master in manual cooperative state is not allowed.
{% endhint %}

[__SOURCE](3-manual-mode/5-arm-interfere/README.md)
## 3.5. Detection of Arm Interference and Soft Limits Between Cooperative Robots

[__SOURCE](3-manual-mode/5-arm-interfere/1-counter-err.md)
### 3.5.1. Detection of Partner Errors

If a partner robot stops due to an arm interference error or soft limit error during cooperative motion, the system stops while maintaining relative positions. If the error occurs on a Slave, the Master will also stop and cannot be operated.

 
<br>
 
![[Figure 3-11] Soft limit error detection](../../_assets/3-11.png)

[__SOURCE](3-manual-mode/5-arm-interfere/2-err-clear.md)
### 3.5.2. Error Clearance

Press the Master's jog key in a direction that does not cause the error to be released, and the error will be cleared. After clearing the error, pressing the jog key again in a direction that does not cause the error allows operation.

 
<br>
 
![[Figure 3-12] Clearing soft limit error](../../_assets/3-12.png)

[__SOURCE](4-programming/README.md)
# 4. Cooperative Motion Teaching

[__SOURCE](4-programming/1-cowork/README.md)
## 4.1. cowork Command

[__SOURCE](4-programming/1-cowork/1-parameters.md)
### 4.1.1. Command Parameters

The `cowork` command marks the start and end of cooperative control in a program and specifies each robot's MASTER and SLAVE roles.

<br>

### Syntax

```python
cowork {param1},{param2},{param3},{param4},{param5}

cowork m,id=0,s=2   
cowork s,m=1,id=0
cowork end
cowork with,sync=1
cowork m,id=0,s=[2,3,4],wait=5
```

<br>

### Parameters
| param# | Meaning | Example |
| :--- | :--- | :--- |
| param1| - Designate your robot role (MASTER/SLAVE) <br>- Specify end of cooperative motion (end) <br> m: Master <br> s: Slave <br> end : End cooperative motion <br> with : Position synchronization with partner robot; sync number must match| <br> <br> `cowork m,s=...` <br> `cowork s,m=...` <br> `cowork end` <br> `cowork with, sync=1` |
| param2 | - Manipulator ID that the master robot controller designates as Master <br> If you are MASTER: <br> id = 0 indicates robot manipulator <br> id = 1 indicates the positioner group 1 registered as an auxiliary axis (if a positioner group is set as an auxiliary axis on the Master side)| `cowork m,id=1,s` <br> |
| param3 | - Specify partner robot number <Br> If you designate yourself as MASTER: <br> the partners become SLAVEs and their robot numbers are specified (up to 3) <br> If you designate yourself as SLAVE: <br> the partner becomes MASTER and specify the robot number of the MASTER | `cowork m,s=[2,3,4]` <Br> `cowork s,m=1` |
| param4 | - Manipulator ID that the Master robot controller designates as Master <br> If you are SLAVE: <br> id = 0 is robot manipulator <br> id = 1 is the positioner group 1 registered as an auxiliary axis (if a positioner group is set as an auxiliary axis on the Master side) | `cowork s,m=1,id=0` |
| param5 | - Partner robot wait time (sec) < 0 (infinite wait) ~ 120 > <Br> If you designate yourself as MASTER: <br> Wait time for SLAVEs to reach the cooperative reference position <br> If you designate yourself as SLAVE: <br> Wait time for MASTER to reach the cooperative reference position | `cowork s,m=1,wait=30` |

[__SOURCE](4-programming/1-cowork/2-usage.md)
### 4.1.2. How to Use the `cowork` Command

(1) On the MASTER robot, the actions within the `cowork ~ cowork end` section are treated as cooperative segment commands. SLAVEs cannot insert action commands.

(2) On SLAVE robots, standard `move` commands cannot be used within the cooperative section; use the `cmov` command (cowork move) instead.

(3) In handling applications where the Slave follows the Master, as in the example below, the Slave will maintain the relative position to the Master and move accordingly when the `cowork` command is executed even if no `cmov` commands are inserted on the Slave.

![](../../_assets/4-prg1.png)
 
(4) On the Slave, you can insert `cmov` commands that interpolate in the Master end effector coordinate system; `cmov` recorded positions are relative to the Master's tool end effector coordinate system. If taught as in the example below, within `cowork ~ cowork end` the Slave performs cooperative motion and follows the Master's movement along the `cmov` path recorded in the Master end effector coordinate system.

 ![](../../_assets/4-prg2.png)

{% hint style="warning" %}

 - A `cowork end` command must be inserted at the end of cooperative motion.
 - For SLAVE robots, `move` commands cannot be inserted within the cooperative section; for MASTER robots, `cmov` commands cannot be inserted.

{% endhint %}

[__SOURCE](4-programming/2-programming.md)
## 4.2. Teaching and Writing Programs for Cooperative Handling

(1) Operators are required equal to the number of cooperative robots; therefore, each operator participates for each robot to be cooperated.

(2) Verify that the cooperative robot common coordinate system is configured.

(3) Move the MASTER and SLAVE robots to their respective cooperation start positions and record the start positions as reference.

![](../_assets/4-prg3.png)
 
 <br>

![[Figure 4-1] Recording cooperative motion start reference positions](../_assets/4-1.png)

<br>

(4) Assign robot roles by entering R351 codes for MASTER and SLAVE robots.

(5) Register the cooperative control start command (`cowork m/s`). The `cowork` command specifies Master/Slave and assigns the Slave/Master numbers. Only one Master may be set, and up to three Slaves may be specified.

 ![](../_assets/4-prg4.png)
 

(6) Operate the MASTER robot by jogging (JOG). The Slave follows the Master tool-tip position relatively. During cooperative jogging, the Slave must have the Enable switch pressed. Record step positions only on the Master; do not record them on the Slave controller.

 
![](../_assets/4-prg5.png)
      

 
![[Figure 4-2] Master robot operation](../_assets/4-2.png)

(7) Record cooperative motion steps on the MASTER. Set the Master's interpolation type and speed. Use standard `move` commands within cooperative motion commands (cmov cannot be used).

 
![](../_assets/4-prg6.png)

(8) When cooperative motion is finished, insert `cowork end` commands on both Master and Slave to end cooperative control.

 
![](../_assets/4-prg7.png)
 

<br>

{% hint style="warning" %}
	Do not change the Slave's Enable switch to OFF during manual cooperative operation. Hardware signals take priority over communication and can cause position mismatches between cooperative robots. In severe cases, this may result in damage to the workpiece or the robot hand.

{% endhint %}

[__SOURCE](4-programming/3-cmov.md)
## 4.3. cmov Command

<br>

```python
cmov {param1},{param2},{param3},{param4},{param5}

cmov R20,L,tg=po1,spd=60%,accu=0,tool=1
cmov R20,L,tg=po1,spd=60%,accu=0,tool=1 until di1
```


<br>

### Parameters
| param# | Meaning | 
| :--- | :--- | 
| param1| - Master robot system manipulator identifier <br> Format: R(#1)(#2) <br> #1 : Master robot system number (1~4) <br> #2 : Master manipulator identifier of the robot system <br> (0: Robot, 1: Positioner Group 1, 2: Positioner Group 2)| 
| param2 | - Interpolation type <br> Specifies the interpolation mode for the slave robot; only linear and circular are supported <br> (L: Linear, C: Circular)|
| param3 | - Movement speed (Speed) <Br> Specify the relative speed compared to the workpiece | 
| param4 | - Accuracy (0~7)|
| param5 | - Tool number (0~31) |


![[Figure 4-3] Method for distinguishing ID identifiers](../_assets/4-3.png)

[__SOURCE](4-programming/4-arc-sealing.md)
## 4.4. Teaching for Arc Welding and Sealing (Jigless Cooperative Control)

(1) Set the manual cooperative roles of Master and Slave robots to 'Independent', record the start steps for cooperation, and insert the cowork command at the cooperation start position.
 
![](../_assets/4-prg8.png)

![[Figure 4-4] Step start and target positions](../_assets/4-4.png)


(2) Set the Manual Cooperative states for Master and Slave according to their roles.

![](../_assets/4-prg9.png)


(3) When you jog the Master, the Slave follows. Record the Master step at the desired position.

 ![](../_assets/4-prg10.png)

(4) Switch the Slave to cmov recording state using R351,3. The robot role indicator at the top of the screen changes from white to red.

 ![](../_assets/4-prg10.png)

(5) Jog the Slave robot to the target position and press the 'Record' key.
 

![[Figure 4-5] Recording cmov target positions](../_assets/4-5.png)

 
![](../_assets/4-prg11.png)  


(6) The cmov positions are recorded on the Slave. The recorded cmov positions are coordinates relative to the Master tool end effector coordinate system. Press the [Properties] key to view or modify the recorded coordinates.
  
(7) The recorded coordinate system will be shown as 'Master'. 

(8) Similarly, move the Slave and record multiple cmov steps.

 ![](../_assets/4-prg12.png)

(9) Note that the movement planning for recorded steps is executed separately by Master and Slave, so the timing when Master and Slave reach their target positions may differ. To align the start timings of the Master's move position and the Slave's cmov position in the cooperative section, use mutual interlocks implemented with HiNet I/O or use `cowork with, sync=1`. The `cowork with` command performs synchronized motion only if the sync numbers match; encountering a `cowork with` with a different number will cause an error.

(10) For example, to synchronize the start of step 5 (S5) for Master and Slave, you can use an _mb memory variable to check whether each robot has reached its step position.

 ![](../_assets/4-prg13.png)

* Using this method, after Master and Slave reach step 4 (S4), they verify that the partner robot has reached step 4 before moving to the next step (S5).

(11) When cooperative motion is finished, insert `cowork end` commands on both Master and Slave to end cooperative control teaching.

![](../_assets/4-prg14.png)     

(12) The entire program example described above is shown below, and timing control such as ⓐ, ⓑ, ⓒ may be applied for cooperative timing control.

 ![](../_assets/4-prg15.png)

(13) The `cowork with` command is used during cooperative control (between `cowork` and `cowork end`) to synchronize positions between Master and Slave. When a `cowork with` command is encountered during cooperative control, it waits until all cooperating robots reach that `cowork with`. Therefore, the earlier program can be modified as follows.

 ![](../_assets/4-prg16.png)


{% hint style="warning" %}

 - When using cmov weaving motion, reference points (refp) must be recorded within the cooperative control region (`cowork ~ cowork end`).
 - Seam-tracking of cmov trajectories using laser vision sensors is not supported.
 - In the cooperative control region (`cowork ~ cowork end`), the number of `cowork with` commands must be the same for both Master and Slave.
 - `cowork with` commands performed jointly by cooperating robots must use the same sync number.

{% endhint %}

[__SOURCE](4-programming/5-cmov-record.md)
## 4.5. Checking cmov Recorded Positions

The cmov steps are a useful feature that allows you to verify taught positions using the step forward/back functions in cmov recording mode. The cmov step records positions and orientations relative to the Master end effector coordinate system, so verify and execute based on the Master's tool position.

 - (1) Set the robot taught as Master (cowork m) to Manual Cooperative Master state (R351,1).
 - (2) Set the robot taught as Slave (cowork s) to cmov recording state (R351,3).
 - (3) Move the Master robot to the step position to be cooperated and leave it stopped.
 - (4) On the Slave, select the cmov step to move to and press the step forward key; the Slave will move to the position recorded in the Master end effector. For example, if the cmov recording position is recorded as the origin (0,0,0) of the Master end effector coordinate system as shown below, the Slave will move to the Master end effector origin regardless of the Master's global position when executing cmov.

 
![[Figure 4-6] Checking cmov recorded positions](../_assets/4-6.png)

{% hint style="warning" %}
 - In cmov recording state (R351,3), the robot will move to the recorded step position regardless of cowork command execution.
 - Master jogging is not allowed in cmov recording state.
 - Because real-time cooperative motion does not occur in cmov recording state, do not operate step forward/back on the Master simultaneously; keep the Master stopped.
 - If you change and then stop the Master's position while in cmov recording state, stepping forward to the cmov step will move to the updated position.
{% endhint %}

[__SOURCE](4-programming/6-positioner/README.md)
## 4.6. Positioner Master System

<br>

This feature allows assigning a positioner as the cooperative Master so that Slave robots can cooperate with the Master positioner. Positioner groups 1-3 are supported.

[__SOURCE](4-programming/6-positioner/1-jog.md)
### 4.6.1. Positioner Master Jog

<Br>

(1) Perform positioner group setup and positioner calibration for the robot that has a positioner installed to enable positioner synchronization.

(2) Use R351,1 or a user key to set the robot with the positioner to Manual Cooperative Master (M:G#R#).

(3) Press the 'Mechanism' key to select the positioner mechanism.

![](../../_assets/4-7.png)

(4) Press the 'Coordinate System' key so that the synchronization coordinate system S1 (or S2) is selected.

 ![](../../_assets/4-8.png)


(5) Set the Slave robot to SLAVE using R351,2 (S:G#R#).

(6) When performing positioner synchronized jog, both Robot 1 and Robot 2 are operated synchronized with the positioner.

[__SOURCE](4-programming/6-positioner/2-teaching.md)
### 4.6.2. Positioner Master Teaching and Playback

Teach Master and Slave using the `cowork` command. On the Slave side, set `id=1` (positioner group number) to select the Master's positioner as Master.

While the positioner is set as Master (Master robot coordinate system 'Sync S1'), record the Slave positions. Recorded positions are stored in the positioner end effector coordinate system.

![](../../_assets/4-prg20.png) 

To have the Master robot cooperate with the positioner, teach smov steps in the same way as for an ordinary positioner. When the Slave records a step while the Master's positioner is set as Master (Master robot coordinate system 'Sync S1'), it is recorded using a robot number that reflects the Master ID.

 
![](../../_assets/4-prg21.png)

The Master uses the same positioner synchronization function, and the Slave is recorded with R11.

Teach Master and Slave in the same way as described in (3) above and finish with `cowork end`.
     
![](../../_assets/4-prg22.png)

After confirming operation in manual mode, operate in automatic mode.

    
![[Figure 4-7] Simulation of positioner synchronized operation per robot](../../_assets/4-9.png)


<br>

{% hint style="warning" %}

 - Jigless cooperative control supports positioner groups 1-3. When positioner jogging or in `cmov`, select the positioner group number 1-3.
 - If values set in the Slave with `cowork s,m=#1,id=#2` differ from the `cmov R#1#2` values, an `E1365 cmov Master No. ID is invalid.` error occurs.

{% endhint %}

[__SOURCE](5-play/README.md)
# 5. Cooperative Motion Playback

[__SOURCE](5-play/1-overview.md)
## 5.1. Overview of Cooperative Playback

This section provides an overview of cooperative playback and its main behaviors, including manual verification and automatic playback procedures. Refer to subsequent sections for detailed instructions.

[__SOURCE](5-play/2-program-check.md)
## 5.2. Program Check in Manual Mode

(1) In manual mode, set the Master robot's manual cooperative state to I (Indiv.) or M (Master), and set the Slave robot's manual cooperative state to I (Indiv.) or S (Slave).
(2) Turn Drive Ready On and press the 'Step Forward' key on both sides.
(3) To verify synchronous motion between Master and Slave, press the Master and Slave step forward keys until cooperative motion is completed.
 
 <br>
 
![](../_assets/4-prg23.png)

![[Figure 5-5] Program check in manual mode](../_assets/5-5.png)

<br>
 

{% hint style="warning" %}
 
 - If the Slave is in cmov recording mode, manual mode cooperative operation with the Master will not be possible.
 - When executing step forward/backward, set 'Execute function on step forward' in Condition Settings to On.
 - The Master and Slave robots check the execution position only at the moment the cowork command is executed; they do not synchronize Master and Slave step positions outside of that. Therefore, the relative positions of Master and Slave checked using step forward/back may differ during automatic mode playback.
 - To synchronize the positions of the two robots, use the `cowork with, sync=1` statement.

{% endhint %}

[__SOURCE](5-play/3-auto-mode.md)
## 5.3. Playback in Automatic Mode

(1) Switch all cooperative robots to automatic mode.

(2) Verify that all cooperative robots have Drive Ready ON.

(3) Start the program from the beginning.

(4) Start each cooperative robot. (The start order of MASTER and SLAVE may be arbitrary.)



{% hint style="warning" %}

 - Do not arbitrarily move the cursor and execute from cowork m (or cowork s) unless you are at the cooperative playback reference position. Cooperative motion calculates the relative position of Master and Slave from the cowork m (cowork s) position, so it must be executed from the cooperative reference position.
 - Set the cooperative waiting time appropriately. If one of MASTER or SLAVE reaches the cooperative reference position first and the partner robot does not arrive within the 'cooperative waiting time', an error occurs. To wait indefinitely, set the cooperative waiting time to 0.


{% endhint %}

[__SOURCE](5-play/4-resume.md)
## 5.4. Stop/Resume of Cooperative Playback

If the user inputs a stop command (external stop, internal stop) during cooperative motion, all robots engaged in cooperative motion will stop.


<br>

![[Figure 5-6] Warning displayed when a partner robot stops](../_assets/5-6.png)

<br>



After stopping during cooperative motion, changing the step number and replaying is only possible when cooperative playback is disabled. If you stop during cooperation, change the step, and then attempt to replay, a [Yes/No] confirmation is required from the user.

<br>

![[Figure 5-7] Message when changing step after stopping during cooperative motion](../_assets/5-7.png)

<br>

 

If a cooperative control state reset is input, it releases the cooperative state and operates. To operate while keeping the cooperative state, specify the stopped step number and start.

[__SOURCE](5-play/5-robot-lock.md)
## 5.5. Robot Lock Function (Robot Lock Playback)

Set 'Condition Settings' → '5: Robot Lock' to <Enabled>.

 
<br>

![[Figure 5-8] Robot Lock Enable Setting](../_assets/5-8.png)

<br>

When the Master robot is set to Robot Lock <Enabled> and playback is performed, the Slave performs cooperative motion while the Master robot does not move and only the axis data monitor changes.


<br>

![[Figure 5-10] Robot Lock Function (Master Lock)](../_assets/5-10.png)

<br>

If the Slave robot is set to Robot Lock <Enabled> and the Master robot is set to <Disabled>, the Master robot operates normally while the Slave robot remains stopped and only monitoring data moves.

<br>

![[Figure 5-11] Robot Lock Function (Slave Lock)](../_assets/5-11.png)

<br>

 

When both Master and Slave are set to Robot Lock <Enabled>, the program runs with both Master and Slave stopped.
 
<br>

![[Figure 5-12] Robot Lock Function (Master, Slave Lock)](../_assets/5-12.png)

<br>


{% hint style="warning" %}

 - Set the cooperative waiting time to an appropriate length.
 - Robots set to Robot Lock <Enabled> will not move, so move them to a position where they will not interfere with other robots before running the program.
 - When changing the Robot Lock setting back to <Disabled> and running, the robot positions and step positions may not correspond; please run the program from the beginning.

{% endhint %}

[__SOURCE](6-hinet/README.md)
# 6. HiNet I/O Features

[__SOURCE](6-hinet/1-io-overview.md)
## 6.1. HiNet I/O Overview

HiNet I/O is a function that shares information between robots via the cooperative control network. Each controller monitors information from cooperative robots, so the sections set to be shared can be used freely. The maximum data size each controller can use is 12 bytes, and it can receive 36 bytes excluding its own portion.
 

![[Figure 6-1] HiNet Group Structure](../_assets/6-1.png)

This function can be used via the robot language (HRScript), allowing various applications that meet user needs.


![ ](../_assets/6-3.png) 

<br>

For example, if configured as below, when ROBOT 1 is the local robot, its information is set to fb7.dob0 ~ fb7.dob3, ROBOT2's information is received at fb7.dib4 ~ fb7.dib7, ROBOT3's information at fb7.dib8 ~ fb7.dib11, and ROBOT4's information at fb7.dib12 ~ fb7.dib15.

<If your robot is ROBOT 1>

| Robot No. | Start Signal | Byte Count | Note |
| :---: | :---: |  :---: | :---: | 
| ROBOT 1 | fb7.0 | 4 | Output (fb7.dob0 ~ fb7.dob3) |
| ROBOT 2 | fb7.32 | 4 | Input (fb7.dib4 ~ fb7.dib7) |
| ROBOT 3 | fb7.64 | 4 | Input (fb7.dib8 ~ fb7.dib11) |
| ROBOT 4 | fb7.96 | 4 | Input (fb7.dib12 ~ fb7.dib15) |


![[Figure 6-2] HiNet I/O Usage Example (Group 1 - 4 Robots) ](../_assets/6-2.png)

[__SOURCE](6-hinet/2-example.md)
## 6.2. Examples

It is not possible to list all applications that can be implemented with the robot language, but a simple example application is shown in the following figure. Because input/output signals can be used, it has the advantage of supporting various applications.

![](../_assets/6-4.png)

[__SOURCE](7-arm-interference/README.md)
# 7. Arm Interference Detection Features

[__SOURCE](7-arm-interference/1-overview/README.md)
## 7.1. Overview of Arm Interference Detection Features

[__SOURCE](7-arm-interference/1-overview/1-purpose.md)
### 7.1.1. Purpose of the Feature

<br>

The purpose is to prevent accidents by stopping the robot in advance when a collision between robot arms and tools is predicted due to program errors or user mistakes (jogging or program creation errors).

[__SOURCE](7-arm-interference/1-overview/2-coverage.md)
### 7.1.2. Scope of the Feature


 <Br>

![[Figure 7-1] Interference between robots](../../_assets/7-1.png)
 <br>

Interference between robot tools and arms is detected using a simplified cylindrical model, and it can also be applied to robots that use drive axes.

- Robots that support the interference detection feature must be connected to the cooperative control network.
- The supported groups and number of robots are the same as for cooperative control.

[__SOURCE](7-arm-interference/1-overview/3-restiction.md)
### 7.1.3. Limitations of the Feature

This feature cannot intelligently and automatically avoid interference between robots nor automatically determine and execute robot drive priorities.

- It does not support automatic arm interference avoidance without mutual interlocks.
- It does not support automatic deadlock avoidance between robots.
- It does not detect interference between a robot's own arm and tool.

[__SOURCE](7-arm-interference/2-setting/README.md)
## 7.2. Configuration Procedures

[__SOURCE](7-arm-interference/2-setting/1-arm-set.md)
### 7.2.1. Enabling Arm Interference Prevention

Select 'System' → '4: Application Parameters' → '17: Cooperative Control' → '4: Inter-robot Interference Prevention' → '1: Interference Prevention Conditions'.

<br> 

![[Figure 7-7] Arm Interference Prevention Menu](../../_assets/7-8.png) 

<br>

To enable arm interference prevention, select the 'Interference Detection Partner Robot'. The 'expected maximum interference distance' is the distance from the arm interference area at which the system expects interference and can perform deceleration stop.

<br> 

![[Figure 7-8] Arm Interference Prevention Conditions Screen](../../_assets/7-9.png)

<br>

| Error Message | E0244 Robot (0)'s arm interference detection is not possible |
|:--|:--| 
| Possible Causes | - If the cooperative control of the partner robot set for interference detection is set to 'Disabled' on the partner robot. <br> - The partner robot is not participating in the cooperative control network. <br> - The partner robot has not configured arm interference prevention conditions. <br> - The partner robot's common coordinate system is not set. |
| Action | Check your robot's and the partner robot's cooperative control status, common coordinate settings, participation in the cooperative control network, and interference prevention conditions. |

[__SOURCE](7-arm-interference/2-setting/2-arm-region.md)
### 7.2.2. Setting Arm Interference Areas

The arm interference area model is a cylinder composed of hemispheres on both ends. For example, for the H-axis, you can model the radius from the H-axis joint position to the V-axis joint position as shown below.


<br>

![[Figure 7-10] Hemispherical and cylindrical arm interference area](../../_assets/7-10.png)

<br>

The cylindrical link model for the robot body arm applies to S, H, V, and B axes. The default radius values for each axis are determined as follows. If additional equipment is mounted on the robot, set the radius for the corresponding axis larger than the default value.

 - S-axis radius: Set to twice the distance from the S-axis rotation center to the H-axis joint
 - H-axis radius: 1.8 times the distance from the B-axis rotation center to the flange face
 - V-axis radius: Distance from the B-axis rotation center to the flange face

<br>

![[Figure 7-11] Axis-specific interference radius settings](../../_assets/7-11.png)

<br>

Currently, arm interference detection supports detecting all axes using the S, H, and V axis settings.

<br>

![[Figure 7-12] H-axis offset radius](../../_assets/7-12.png)

<br>

{% hint style="warning" %}
If you intend to set values smaller than the defaults, exercise extreme caution. For example, the H-axis of a serial-link robot such as the HS220 has an offset to the right from the S-axis center as shown in the figure. The H-axis interference detection area is set based on the segment from the S-axis rotation center along the H-axis link to the V-axis rotation center, so the H-axis radius must be set large enough to include the entire H-axis link from the S-axis rotation center.
{% endhint %}

[__SOURCE](7-arm-interference/2-setting/3-tool-region.md)
### 7.2.3. Setting Tool Interference Areas

<Br>

![[Figure 7-13] Flange coordinate system](../../_assets/7-13.png)

<Br>

To set the tool interference area for each tool number, use the robot flange coordinate system as a reference. When the robot is in the reference pose, the flange coordinate system has Z pointing outward normal to the flange face, X pointing downward, and Y pointing to the robot's left.

You can set up to 4 interference areas per tool number. For any tool number used in the robot program, you must configure the tool interference area. If not configured, tool interference detection will not occur.

### 1) Example for a single (servo-gun) tool

The tool interference area is set by defining start and end points and a radius from coordinates on the tool flange. You may set up to four interference areas per tool number.

Refer to the figure below for flange coordinate directions and an example configuration.
 
 <Br>

![[Figure 7-14] Flange coordinate system example](../../_assets/7-14.png)

<Br>

### 2) Example for a hanger-type tool

#### 2-1) When configuring only one tool interference area

For asymmetrical tools relative to the flange center, when defining a single tool interference area you can set the tool shape center and use the maximum distance from center to tool corners as the radius. In the example below, relative to the robot coordinate system X=-175, Y=-485, and the radius should be set slightly larger than the larger of R1 and R2 (e.g., 1300 rather than 1250). Because hemispheres are created at each end of the cylinder when setting a radius of 1300, set Z positions as P1=(-175,-485,500) and P2=(-175,-485,1000).

 
 <Br>

![[Figure 7-15] Drawing for 1 tool interference area setting](../../_assets/7-15.png)


<Br>
  

![[Figure 7-16] 1 tool interference area setting](../../_assets/7-16.png)


<Br>

However, when the radius is set this large, it may be unnecessarily larger than the actual tool shape. If precise tool region settings are required, model the tool by dividing it into multiple regions.


#### 2-2) When configuring 4 tool interference areas

<Br>
  

![[Figure 7-17] Drawing for 4 tool interference areas](../../_assets/7-17.png)


<Br>

For large tools such as hangers, dividing the area can prevent overestimation of the tool interference area. For example, for a tool of width 2110mm and height 1350mm, divide the vertical area into three equal parts and model three cylinders with approximately 350mm radius as areas 1-3. Finally, set the offset from the flange to the tool as area 4 to achieve the configuration below.

 
<Br>
  

![[Figure 7-18] 4 tool interference areas configuration](../../_assets/7-18.png)

<Br>



[__SOURCE](7-arm-interference/2-setting/4-monitor.md)
### 7.2.4. Arm Interference Status Monitoring

<Br>

![[Figure 7-21] Cooperative control monitoring](../../_assets/7-21.png)


<br>

You can check the arm interference state in 'Cooperative Control Monitoring'. The arm interference state displays the potential interference axis and the interference distance.

 - Potential Interference Axis: The axis of your robot that has the smallest distance to the partner robot
 - Interference Distance [mm]: Distance between potential interference axes
      - Display range: 10 times the expected maximum interference distance (if expected maximum interference distance is 0, display range is 1000 mm)
      - If interference distance exceeds the display range, it is shown as ----.

If the monitored arm interference state differs from the actual state, check the cooperative control common coordinate system and the arm interference detection configuration.

[__SOURCE](7-arm-interference/3-detect/README.md)
## 7.3. Interference Detection

[__SOURCE](7-arm-interference/3-detect/1-decel-stop.md)
### 7.3.1. Deceleration Stop

If the robot decelerates and stops after invading the user-configured arm interference area and tool interference area, due to deceleration distance and robot inertia, a collision may occur even if an error is detected. Therefore, the detection area is expanded taking robot speed into account to detect interference earlier.

The figure below illustrates the concept of generating an expected interference area (Level 2 detection area) when robots move toward each other. The dashed area indicates the expected interference area, and the solid line indicates the user-configured interference area.
 
![[Figure 7-22] Interference area invasion 1](../../_assets/7-22.png)


<br>

The expected interference area is automatically set by calculating the robot's travel speed and stopping time, but the user can set the maximum value as the 'expected maximum interference distance.'
The expected interference distance calculated by the controller, when the robot moves at high speed, is the configured interference area plus the expected maximum interference distance to detect interference. In the expected interference distance range, the robot performs deceleration stop, and if it enters the interference area, it performs an immediate stop without deceleration. If the robot moves at low speed and the controller-calculated expected distance is smaller than the 'expected maximum interference distance', it will not detect interference even if it is within the expected maximum interference distance.

 ![[Figure 7-23] Arm interference prevention conditions](../../_assets/7-23.png)


<br>

| Error Message | - W0147 Robot 0) expected arm interference and stopped  <br> - E0237 Robot 0) ARM interference area detected |
|:--|:--|
| Possible Causes | When a robot invades another robot's expected interference area during movement, the above warning and error messages may occur simultaneously and stop the robot. |
| Action | If the above warning occurs during normal program playback, re-check the work program. |


[__SOURCE](7-arm-interference/3-detect/2-quick-stop.md)
### 7.3.2. Immediate Stop

Even if deceleration stopping occurs in the predicted interference detection (Level 2 detection area), the robot may still invade the interference area due to deceleration distance during stopping. If the interference area is directly exceeded, an immediate stop is performed without deceleration.

 
![[Figure 7-24] Interference area invasion 2](../../_assets/7-24.png)


| Error Message | E0237 Robot 0) ARM interference area detected |
|:--|:--|
| Possible Causes | The arm and tool areas were invaded |
| Action | If the above warning occurs during normal program playback, re-check the work program. |


[__SOURCE](7-arm-interference/3-detect/3-play-err.md)
### 7.3.3. Errors Occurring During Playback

When two robots move from S1 to S2 on a rail as shown below, if the S2 positions of the two robots are separated by more than the sum of the tool interference area and the expected maximum interference distance, no W0147 or E0237 will occur. This represents a normal program.

<br> 

![[Figure 7-25] Example of a normal program](../../_assets/7-25.png)

<br>

If, as in the figure below, the S2 point is slightly outside the configured tool interference area but within the expected maximum interference distance, an error (W0147 or E0237) may occur. In this case, adjust the expected maximum interference distance or change the teach points.

<Br>
 
![[Figure 7-26] Incorrect program example 1](../../_assets/7-26.png)

<br>
 
If the S2 point is taught so that it completely invades the defined tool interference area, an error (W0147 or E0237) will occur when the robots move to S2.


<br>

![[Figure 7-27] Incorrect program example 2](../../_assets/7-27.png)

<br>

In such cases, reduce the 'tool interference area' or the 'expected maximum interference distance' to prevent the error.


{% hint style="warning" %}

Setting the tool interference area too small-smaller than the actual tool-may cause collisions between robots.

{% endhint %}

[__SOURCE](7-arm-interference/3-detect/4-dead-lock.md)
### 7.3.4. Handling in Deadlock State

A deadlock occurs when two robots invade each other's interference area and cannot move the robots further by jogging or program execution. In this case, release the interference detection for the affected robot relative to the partner robot, and then use the jog function to move out of the interference area carefully under user supervision.
 
<br> 

![[Figure 7-28] Release inter-robot arm interference detection](../../_assets/7-28.png)

<br>

After moving out of the interference area, check the partner robot number and resume operation.
 
<Br> 

![[Figure 7-29] Setting inter-robot arm interference detection](../../_assets/7-29.png)

[__SOURCE](7-arm-interference/3-detect/5-net-err.md)
### 7.3.5. Handling Network Issues During Cooperative Control

If the cooperative control network is not functioning properly, arm interference detection between robots may not operate correctly. When problems occur on the cooperative control network, the following error may occur.

<br>

| Error Message | E0244 Robot (0)'s arm interference detection is not possible |
|:--|:--|
| Possible Causes | The HiNet network to the partner robot for which interference detection conditions were set is disconnected |
| Action | - Check the network cable of the affected robot. <br> - Refer to Cooperative Control Status Monitoring and restore the cooperative control state to normal. |

[__SOURCE](8-service/README.md)
# 8. Service Functions

[__SOURCE](8-service/1-status-mon.md)
## 8.1. Cooperative Control Status Monitor

(1) Select 'Inter-robot Cooperative Control' from 'Window Settings' → 'Selection'.
 
 ![](../_assets/9-2.png)


(3) The cooperative control status is displayed as follows.

 ![](../_assets/9-3.png)



(4) Each item in the monitoring function has the following meanings.

 - Motor ON: Indicates the drive-ready state of each robot. (on/off)
- Operation Mode: Indicates whether each robot is set to manual mode or automatic mode. (Manual/Automatic)
- Manual Cooperation: Displays the manual cooperative state of each robot.
    - Independent: Individual jog state
    - Master: Cooperative jog state, MASTER specified
    - Slave: Cooperative jog state, SLAVE specified
- Automatic Cooperation: Displays the cooperative state during robot playback.
    - Stop: Robot is not running
    - Individual: Performing individual robot playback actions
    - Waiting: Waiting in the cowork command for the partner robot to reach the cooperation position
    - Cooperation: During cooperative playback
- Error State: Shows the recent error state of each robot. Cleared upon startup
- Potential Interference Axis: The axis of the robot closest to the partner robot
- Interference Distance [mm]: Distance between potential interference axes


{% hint style="warning" %}
If cooperative control is set to <Disabled> in the cooperative control parameters, monitoring information will not be displayed.

![](../_assets/9-4.png)

{% endhint %}

[__SOURCE](8-service/2-io-mon.md)
## 8.2. HiNet I/O Monitor

(1) Select 'General Input' from 'Window Settings' → 'Selection'.  
![](../_assets/9-5.png)


(2) Check the status of configured input signals for each robot.  
![](../_assets/9-6.png)

[__SOURCE](8-service/3-manual-sigout.md)
## 8.3. Manual Output Function

You can manually change your robot's cooperative control status.

- Display the 'General Output' window from 'Window Settings' → 'Selection'.
- Move to the output signal corresponding to your robot number that you want to change manually.
- Press the 'Manual Output' button and change it in the dialog that appears.


![](../_assets/9-7.png)

[__SOURCE](8-service/4-rcode.md)
## 8.4. R code



R codes used for cooperative control.

[Table 8-1] R351 Manual Cooperative State Setting

| R351 | Description |
|:--:|:--:|
|0|Indiv. (Individual)|
|1|Master|
|2|Slave|
|3|cmov Recording Mode|

<br>
[Table 8-2] R353 Robot Cooperative State Reset

| R353 | Description |
|:--:|:--:|
|0|Cancel Reset|
|1|Execute Reset|

[__SOURCE](9-error-code/README.md)
# 9. Error Codes

[__SOURCE](9-error-code/1-warning.md)
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

[__SOURCE](9-error-code/2-system-err.md)
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

[__SOURCE](9-error-code/3-operation-err.md)
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
