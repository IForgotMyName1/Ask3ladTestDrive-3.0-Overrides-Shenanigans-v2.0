# How to use these files – step by step

Everything below is based on the files in this repo. Paths are relative to your `WarThunder` folder.

| Repo folder | Game folder |
|---|---|
| `weapons/` | `content\pkg_local\gameData\weapons\ask3lad\` |
| `overrides/` | `content\pkg_local\gameData\weapons\ask3lad\` |
| `units/` | `content\pkg_local\gameData\units\` (`us_m2a4` goes in `units\tankmodels\userVehicles\`) |
| `missions/` | `UserMissions\Ask3lad\` |
| `flightmodels/` | `content\pkg_local\gameData\flightModels\` |
| `flightmodels/weaponPresets/` | `content\pkg_local\gameData\flightModels\weaponPresets\` |

Weapons and overrides live flat in `gameData\weapons\ask3lad\` (no subfolders). The subfolders in this repo are only for organisation.

> Keep a backup of your current game files before copying new ones over them.

---

## 1. Install a weapon

1. Copy the file from `weapons/` into `gameData/weapons/ask3lad/`.
2. If it is used by an override or unit file, copy those too (see the include line inside them).
3. Keep the file names exactly as the other files refer to them.

## 2. Tweak an existing game weapon (override)

An override file includes the original game weapon and then changes only some values:

```
include "#/develop/gameBase/gameData/Weapons/navalModels_weapons/460mm_45_type_94_naval_user_cannon.blk"

"@override:bullet" { "@override:speed":r=804 }
"@override:bullet" { recoilMultiplier:r=0.0 }
"@override:recoilOffset":r=0.0
"@override:recoilTimes":p2=0.01, 0.01
```

Steps:
1. Copy a file from `overrides/` into `gameData/weapons/ask3lad/`.
2. Change the numbers you want. Use `"@override:<field>"` for values that already exist in the base weapon.
3. For a specific shell, nest it: `"@override:460mm_jp_type91_navy_apc" { "@override:bullet" { "@override:mass":r=300.0 } }`.
4. Reference the override file from a unit (section 3) or from a plane preset.

See `Ask3ladBigWeaponSir.blk` for a full example.

## 3. Put a weapon on a vehicle (units)

A unit file includes a base vehicle, then swaps the weapon preset and the gun:

```
include "#/develop/gameBase/gameData/units/tankModels/us_m60_120s.blk"

"@override:weapon_presets" { "@override:preset[1]" { "@override:name":t = "us_m60_120s_default"}}
"@override:weapon_presets" { "@override:preset[1]" { "@override:blk":t = "gameData/weapons/ask3lad/cannon_is2_fv4005_v2.blk"}}

"@override:commonWeapons" { "@override:Weapon[1]" { "@override:trigger":t = "gunner0"}}
"@override:commonWeapons" { "@override:Weapon[1]" { "@override:blk":t = "gameData/weapons/ask3lad/Ask3ladBigWeaponSir.blk"}}
```

Steps:
1. Pick the file in `units/` (example: `units/us_m2a4/us_m2a4.blk`).
2. Install it as the unit the mission loads. The ground mission uses `userVehicles/us_m2a4`, so the file has to be installed under that name.
3. The preset `name` must match the preset name the mission asks for (the mission uses `us_m1a2_sep3_abrams_default`).
4. Optional: add the physics snippet (`us_m2a4_physics_550t_snippet.blk`) lines to change mass and engine. Ground vehicles only.

## 4. Swap the lmur (helicopter missile) for a custom bomb or missile

Edit `gameData/weapons/ask3lad/Laser9000.blk`:

1. Set `mesh:t=""` to your bomb mesh name (find it in the War Thunder datamine).
2. Set `explosiveMass:r=` to the explosive mass in kilograms (the fab9000 example is `explosiveMass:r= 4297.0`).
3. Set `warheadMass:r=` to the mass of the whole bomb in kilograms (about 25 is recommended, so `warheadMass:r= 25.0`).

Then in `flightmodels/ask3lad_air_player.blk` (installed in `gameData\flightModels\`):

4. Replace all 3 occurrences of `gameData/Weapons/containers/lmur.blk` with
   `gameData/weapons/ask3lad/Laser9000_container.blk` (the custom missile).

## 5. Missions

1. Copy the mission `.blk` from `missions/` into `WarThunder\UserMissions\Ask3lad\`.
2. `ask3lad_testdrive.blk` needs the `userVehicles/us_m2a4` unit from section 3 and the preset `us_m1a2_sep3_abrams_default`.
3. `ask3lad_testdrive_air_3x.blk` is the air version (thrust x3, respawning targets, nuke event after 210 s).

## Quick checklist when something doesn't work

- Is every file you reference actually in `gameData/weapons/ask3lad/` with the exact same name?
- Does the preset `name` in the unit match what the mission asks for?
- Check include paths for typos (e.g. a doubled `weapons/weapons/`).
