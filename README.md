# gw2-docs

The process consists of 2 parts:
- Missiles
- Effects

Missiles: missiles are kinda like projectiles

Effects: effects are like AoE's (these can sometimes be created with projectiles)

# Missiles

There is a dynamic array that keeps track of every missile that is currently present. 
This array contains missile(?) structs that might not contain every detail of the missile.
Missiles(?) get added to the array in the following function:
`0x0F1A1C0`

![alt text](https://image.prntscr.com/image/hMAwoQ6RRPSzRNbX1qqO1Q.png)

The structs and offsets that are used to iterate over the missiles(?):
```
#define MISSILE_MANAGER 0x20DC108

struct SkillInfo
{
	BYTE gap0[0x28];
	DWORD skillId;
};

struct SkillDef
{
	BYTE gap0[0xB0];
	SkillInfo* skillInfo; // this sometimes returns an invalid pointer (might wanna check if it is within bounds)
};

struct Missile
{
	BYTE gap0[0x60];
	float x;
	float y;
	float z;
	BYTE gap1[0x4];
	SkillDef* skillDef;
	BYTE gap2[0x58];
	float targetX; // these are multiplied by some value (might need to hook to access these values)
	float targetY; // these are multiplied by some value (might need to hook to access these values)
	float targetZ; // these are multiplied by some value (might need to hook to access these values)
};

struct MissileManager
{
	BYTE gap0[8];
	Missile** missiles;
	BYTE gap1[4];
	unsigned int maxMissiles;
};
```

To get access to the target position of a missile (or target character) and missile speed of a missile, 
the following function can be hooked: `0x10E17D0`
![alt text](https://i.ibb.co/nsbNpCV/img.png)

The last part contains an import branch. Function `fn_processMissileTarget` will only be called if the 
missile has a character as a target. The function `fn_processMissile` will only be called if the missile
does not have a character as a target (for example a skillshot).

I haven't reversed the character struct but I think that (targetAgent, 0x10) might point to a character struct.
Also the target position of a missile eventually gets stored into the missile struct (the one above). But
the stored coordinates that are in this struct are transformed by a set of floats. By hooking this(`0x10E17D0`) 
function you will get the real target coordinates.

TODO for missiles:
- find the source character of a missile (can be useful for PvP?)

# Effects

There is a dynamic array that keeps track of every effect that is currently present. This array contains effect(?) structs. Effects(?) get added to the array in the following function: `0x10A0900`

![alt text](https://image.prntscr.com/image/6kysouMLRFC8IkgSdcqvAQ.png)

Structs to iterate over the effects:
```
struct Effect
{
	char pad_0x0000[0x40]; //0x0000
	float targetX; //0x0040 
	char pad_0x0044[0xC]; //0x0044
	float targetY; //0x0050 
	char pad_0x0054[0xC]; //0x0054
	float targetZ; //0x0060 
};

struct EffectManager
{
	BYTE gap0[8];
	Effect** effects;
	BYTE gap1[4];
	unsigned int maxEffects;
};
```
TODO for effects:
- find the skillId (Important)

