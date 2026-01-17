## 2.4.3. Travel-Axis System

When configuring the travel-axis system for cooperative control, install travel axes with the same specifications as parallel as possible.

![[Figure 2-6] Travel-axis system configuration for cooperative control](../../_assets/2-6.png)

{% hint style="warning" %}
- Systems with travel axes should set the travel-axis specification to 'arbitrary' and perform travel-axis calibration before use.
- Install the travel axes of cooperative robots as parallel as possible.
- Large synchronization errors during travel-axis movement may be caused by inaccurate travel-axis calibration.
- For details about the travel-axis calibration function, refer to the '${cont_model} controller operation manual'.
- Travel-axis calibration should be performed for both MASTER and SLAVE.

{% endhint %}