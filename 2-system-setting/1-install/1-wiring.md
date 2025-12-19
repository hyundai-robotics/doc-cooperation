## 2.1.1. Emergency Stop Wiring

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
