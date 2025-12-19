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