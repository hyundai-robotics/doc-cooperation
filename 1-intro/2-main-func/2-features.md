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