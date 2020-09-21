# Squad functions
This update will add an api for the squad panel. It also allows one to automatically create a squad.
![](https://i.ibb.co/mBmH4vW/squad.png)

```
Name: fn_updateSquadInfo
Address: 0xa16c00
Can be located with string "selectedIcon"
```
Most of the important squad functions are being called in this function.

![](https://i.ibb.co/cxYxSbr/fn-update-Squad-Info.png)

You can ignore most of the body of the switch cases. You just have to pay attention to the function calls of the following context classes:
1. fn_getSquadCtx (0x489ed0)
2. fn_getSquadCtx2 (0x44c050)

So in total you have the following functions:
1. createSquad(this, v12), you can just set v12 to null, i tried to trace the v12 parameter but it goes through a lot of hoops
2. setSquadMode(this, mode), mode can be either 10 or 50
3. lockSubgroups(this, flag), flag can be true or false
4. allowInvites(this, flag), flag can be true or false
5. privateSquad(this, flag), flag can be true or false
6. setJoinRules(this, mode), mode can be 0-2 (all inclusive)
7. leaveSquad(this)
