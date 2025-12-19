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