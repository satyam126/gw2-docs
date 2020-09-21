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
1. fn_getSquadCtx
2. fn_getSquadCtx2
