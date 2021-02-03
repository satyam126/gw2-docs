# Realtime Skill Duration

![alt text](https://i.ibb.co/tD6BzvW/yellowbar.png)

The goal of this post is to track the progress of a skill (0-100%). <br/>
I have found an UI function that gets called every time the yellow bar gets updated. This function can be found with the following string: ```"..\\..\\..\\Game\\Ui\\Widgets\\SkillProgress\\SkpSegment.cpp"```

![alt text](https://i.ibb.co/JmwhPNg/On-Skill-Segment.png)<br/>
A percentage gets computed at line 47. The passed time ```(0x48)``` get divided by the total cast time of the skill ```(0x54)```. The goal is to extract that percentage. Currently I'm achieving that by using a hook.
<br/>
I've tried to trace the ```v3``` (first argument of this function) back to the origin. But it seems like that this field is entangled in UI related stuff.
<br/>
<br/>
If you keep hitting xref on the original function you will end up in a big switch statement:
![alt text](https://i.ibb.co/vHkrCJV/uiSwitch.png)<br/>
The first argument of this function contains some sort of ```frameId```.
This ```frameId``` also matches on where I assume this ```frame``` might gets initialized/created?

This is the function where I think the ```frame``` gets initialized/created? (I hooked it to extract the ```frameId``` and it only got called once): (found with: "..\\..\\..\\Game\\Ui\\Widgets\\SkillProgress\\SkpWarmup.cpp")
![alt text](https://i.ibb.co/0VHDkqQ/Create-Skill-Warmup.png)<br/>

The arguments of this function are easy to trace back (```Character```, ```Order```, ```CharSkill```, ```SkillDef```, etc.). This function gets called from some kind of ```Order``` class. Your player character has an Order struct that contains an array of Orders. This array
contains the current active orders. Currently I've identified orders such as ```SkillOrder``` and ```MovementOrder```. Unfortunately the arguments of the function that gets called on every skill progress bar update is not that easy to trace back.