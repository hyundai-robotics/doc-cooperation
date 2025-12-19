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
