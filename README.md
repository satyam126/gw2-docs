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

# Effects
