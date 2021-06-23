# Orders
This change will expose the orders. This will allow us to do the following:
- view interactions/channels with gadgets
- view dodges from other players
- view accurate skill start times

The notify table you called ```IAgentCharNotifyVftable__``` contains the function ```BeginOrder```.
The ```BeginOrder``` function adds "orders" to a list. This list can be found at ```rcx + 0x28```.

![alt text](https://i.ibb.co/0J7k0xD/Create-Order.png)
<br/>
This ```CreateOrder``` function that is being called in the function ```BeginOrder``` can create an order of several types(skill cast, movement, evade, etc).

![alt text](https://i.ibb.co/c6dH2jJ/Construct-Order.png)
<br/>
Variable ```v5``` is the second argument of this function. It is probably some kind of bitfield because its being used like this in ```BeginOrder```:
* ```(v5 >> 4) & 1```
* ```orderIndex = (v5 >> 5) & 1;```
This could indicate the type of the order?
<br/>

Variable ```v4``` is the third argument of this function. It is a pointer to a struct that contains the Id of an order.
<br/>
<br/>
<br/>
<br/>
![alt text](https://i.ibb.co/r4g2k3S/Skill-Order-Construct.png)
<br/>
<br/>
<br/>
<br/>
Looking at the contents of the SkillOrder object in memory will yield the following image:
![alt text](https://i.ibb.co/gzZnQqk/Skill-Order.png)
The most important things that an order should have are:
1. UNIQUE order id
2. Something that determines the skillId (skillDef or some derivative)
3. *Timestamp when the order was placed (optional, can be estimated with a loop)

&ast; The timestamp I found is unfortunately not stable, I wonder if we can find one.

