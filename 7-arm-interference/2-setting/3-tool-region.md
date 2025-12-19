## 7.2.3. Setting Tool Interference Areas

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

For large tools such as hangers, dividing the area can prevent overestimation of the tool interference area. For example, for a tool of width 2110mm and height 1350mm, divide the vertical area into three equal parts and model three cylinders with approximately 350mm radius as areas 1–3. Finally, set the offset from the flange to the tool as area 4 to achieve the configuration below.

 
<Br>
  

![[Figure 7-18] 4 tool interference areas configuration](../../_assets/7-18.png)

<Br>


