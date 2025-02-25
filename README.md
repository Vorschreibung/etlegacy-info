# ET:Legacy Info
Some bits of info around ET:Legacy.

- [**List of CVARs**](https://etlegacy.readthedocs.io/en/latest/cvars.html)
  (**NOTE** - These have to be updated manually and aren't likely to be up to
  date. - There's really no substitute to grepping the ET:L source atm.)

## General
### Commands to mutate CVARs (`set`/`seta`/`setl`/...)
```
set   - Set a CVAR temporarily.
seta  - Set a CVAR and "archive" it (make it permanent).
setl  - Set a CVAR temporarily and "locks" the setting.
sets  - Set a CVAR temporarily. Serverinfo flag is set (sent in response to front end requests).
setu  - Set a CVAR temporarily. Userinfo flag is set (sent to server on connect or change).
reset - Reset a specific cvar.
unset - Unset a userdefined cvar.

```

## Dev/Debug
### Skip warmup for dev cycles
```
g_doWarmup "0"
```

### Enable instant respawning for dev cycles
```
# default: 0
g_forcerespawn -1
```

### Draw last lines of Console during gameplay
```
con_drawnotify 1
con_numNotifies 10
```

### Auto-select a team/class/weapon during startup
```bash
unset_auc="cg_autoCmd ''"

CLASS_AXIS_COVERT_OPS_STEN="team r 4 10 3"
CLASS_AXIS_COVERT_OPS_K43="team r 4 31 3"
CLASS_AXIS_COVERT_OPS_FG42="team r 4 32 3"
CLASS_AXIS_SOLDIER_PANZERFAUST="team r 0 5 3"
CLASS_AXIS_SOLDIER_MOBILE_MG42="team r 0 30 3"
CLASS_AXIS_SOLDIER_MORTAR="team r 0 35 3"
CLASS_AXIS_SOLDIER_FLAMETHROWER="team r 0 6 3"
CLASS_AXIS_FIELD_OPS="team r 3 3 38"
CLASS_AXIS_ENGINEER_MP40="team r 2 3 38"
CLASS_AXIS_ENGINEER_K43="team r 2 23 3"
CLASS_AXIS_MEDIC="team r 1 3 38"
CLASS_ALLIED_COVERT_OPS_FG42="team b_4_33_8"
CLASS_ALLIED_COVERT_OPS_GARAND="team b 4 25 8"
CLASS_ALLIED_COVERT_OPS_STEN="team b 4 10 8"
CLASS_ALLIED_SOLDIER_PANZERFAUST="team b 0 5 8"
CLASS_ALLIED_SOLDIER_MOBILE_MG42="team b 0 30 8"
CLASS_ALLIED_SOLDIER_MORTAR="team b 0 35 8"
CLASS_ALLIED_SOLDIER_FLAMETHROWER="team b 0 6 8"
CLASS_ALLIED_FIELD_OPS="team b 3 8 37"
CLASS_ALLIED_ENGINEER_THOMPSON="team b 2 8 37"
CLASS_ALLIED_ENGINEER_GARAND="team b 2 24 8"
CLASS_ALLIED_MEDIC="team b 1 8 37"

# e.g. pass ...

+set cg_autoCmd "${CLASS_AXIS_SOLDIER_PANZERFAUST};${unset_auc}"
```

e.g.:
```bash
#!/usr/bin/env bash
args=(
    +sv_fps 40
    +sv_pure 0

    +set cg_autoCmd "team r 0 5 3;cg_autoCmd ''"

    +devmap battery
)
./build/etl.x86_64 "${args[@]}"
```

## Server CVARs
### Restrict Skills/Upgrades
see <https://github.com/etlegacy/etlegacy/blob/dc468ca65237fa9de1d4932b4a7c191186ee136e/src/game/bg_misc.c#L56>
```
# defaults
# NOTE - disable by setting -1, e.g.: 'skill_medic -1'
skill_battlesense 20 50 90 140
skill_engineer 20 50 90 140
skill_medic 20 50 90 140
skill_fieldops 20 50 90 140
skill_lightweapons 20 50 90 140
skill_soldier 20 50 90 140
skill_covertops 20 50 90 140
```
### Restrict Heavy Weapons
```
# default
g_heavyWeaponRestriction 100
```
