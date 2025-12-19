## 5.3. Playback in Automatic Mode

(1) Switch all cooperative robots to automatic mode.

(2) Verify that all cooperative robots have Drive Ready ON.

(3) Start the program from the beginning.

(4) Start each cooperative robot. (The start order of MASTER and SLAVE may be arbitrary.)



{% hint style="warning" %}

 - Do not arbitrarily move the cursor and execute from cowork m (or cowork s) unless you are at the cooperative playback reference position. Cooperative motion calculates the relative position of Master and Slave from the cowork m (cowork s) position, so it must be executed from the cooperative reference position.
 - Set the cooperative waiting time appropriately. If one of MASTER or SLAVE reaches the cooperative reference position first and the partner robot does not arrive within the 'cooperative waiting time', an error occurs. To wait indefinitely, set the cooperative waiting time to 0.


{% endhint %}
