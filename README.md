# Ask3lad Test Drive 3.0 – Overrides & Shenanigans

Custom weapons, overrides, units and missions for **Ask3lad Test Drive 3.0** (War Thunder CDK).

Start with [`notes/HOWTO.md`](notes/HOWTO.md) for the step-by-step guide.

## Folders

| Folder | What's inside |
|---|---|
| `weapons/` | Weapon definitions (cannons, bombs, rockets). Copied flat into `gameData/weapons/ask3lad/`. |
| `overrides/` | Small `include` + `@override` files that tweak an existing game weapon (speed, recoil, fuse...). Also go into `gameData/weapons/ask3lad/`. |
| `flightmodels/` | Player aircraft flightmodel, plus its weapon preset in `weaponPresets/`. |
| `units/` | Vehicle files (`us_m2a4`, ...) that pick which weapon the unit carries, plus physics snippets. |
| `missions/` | Mission `.blk` files. |
| `notes/` | Guides and procedures. |

## Naming

`<type>_<name>_<variant>.blk`, lowercase: `cannon_`, `bomb_`, `rocket_`, `override_`.
Two exceptions keep their original names because other files and the notes refer to them:
`Laser9000.blk` / `Laser9000_container.blk`, `Ask3ladBigWeaponSir.blk`, `Ask3ladBigCannonSir.blk`, `IForgotMyAirGun.blk`, `IForgotMyAirWeapon.blk`, `ask3lad_air_player.blk`, `ask3lad_air_custom.blk`.

## Where each file goes in the game

All paths are relative to your `WarThunder` folder.

| Repo folder | Game folder |
|---|---|
| `weapons/` | `content\pkg_local\gameData\weapons\ask3lad\` |
| `overrides/` | `content\pkg_local\gameData\weapons\ask3lad\` |
| `units/` | `content\pkg_local\gameData\units\` (`us_m2a4` goes in `units\tankmodels\userVehicles\`) |
| `missions/` | `UserMissions\Ask3lad\` |
| `flightmodels/` | `content\pkg_local\gameData\flightModels\` |
| `flightmodels/weaponPresets/` | `content\pkg_local\gameData\flightModels\weaponPresets\` |

## weapons/

| File | What it is | Old name |
|---|---|---|
| `cannon_supah_apfsds_mk1.blk` | APFSDS cannon with a HE filler | `IForgotMyNameSupahApfsds.blk` |
| `cannon_supah_apfsds_mk2.blk` | Supah APFSDS, Mk2 | `IForgotMyNameSupahApfsdsMK2.blk` |
| `cannon_hybrid_apfsds_hesh.blk` | 120 mm APFSDS + HESH | `hybrid_apfsds_hesh.blk` |
| `cannon_is2_fv4005_v1.blk` | Hybrid: IS-2 APHE ballistics + FV4005 HESH explosion | `is2fv4005.blk` |
| `cannon_is2_fv4005_v2.blk` | Guided AP/HESH hybrid cannon (newer than v1) | `is2fv4005-2.blk` |
| `cannon_lakbus.blk` | Lakbus cannon | `lakbus_cannon.blk` |
| `cannon_2s38_apfsds.blk` | 2S38 APFSDS (used for the plane gun, unfinished) | `2s38_apfsds.blk` |
| `cannon_mg.blk` | Custom machine gun/cannon (not documented yet) | `mg.blk` |
| `bomb_guided_mk2.blk` | Guided bomb Mk2 | `guided_bomb_mk2.blk` |
| `bomb_nuke_yeetus_deletus.blk` | Nuclear bomb (`us_nuclear_bomb_mk6` mesh) | `Yeetus_Deletus.blk` |
| `rocket_better_bomb.blk` | Hydra/Swingfire rocket using the `uk_12000lb_hc_mkI_n33_bomb` mesh | `Better_bomb.blk` |
| `rocket_su_rds37_hydra.blk` | Hydra-based rocket | `su_rds37_hydra.blk` |
| `Laser9000.blk` | Laser-guided rocket with the `su_fab_9000` mesh (explosiveMass 4297 kg), replaces the lmur | (unchanged) |
| `Laser9000_container.blk` | Container that points to `Laser9000.blk` | (unchanged) |

## overrides/

| File | What it is | Old name |
|---|---|---|
| `Ask3ladBigWeaponSir.blk` | 460 mm Type 94 naval cannon: speed 804, no recoil, shell masses | (unchanged) |
| `Ask3ladBigCannonSir.blk` | 152 mm LP83 cannon: 15 shots/s, no recoil, 1 kg shells | (unchanged) |
| `IForgotMyAirGun.blk` | 460 mm naval cannon adapted for the plane | (unchanged) |
| `IForgotMyAirWeapon.blk` | Plane weapon wrapper (Laser9000) | (unchanged) |
| `override_460mm_naval_cannon.blk` | 460 mm cannon tweaks (speed, recoil, fuse) | `460mm_naval_cannon_override.blk` |
| `override_rocket_su_rds37_hydra_speed200.blk` | `rocket_su_rds37_hydra` at speed 200 | `su_rds37_hydra_override.blk` |
| `override_cannon_is2_fv4005_v2_speed200.blk` | `cannon_is2_fv4005_v2` at speed 200 | `is2fv4005-2_speed_override.blk` |

## units/

| File | What it is | Old name |
|---|---|---|
| `us_m2a4/us_m2a4.blk` | M1A2 SEP3 Abrams carrying the Yamato 460 mm cannon setup | `us_m2a4.blk` |
| `us_m2a4/us_m2a4_m60_120s_aphe_hesh.blk` | M60 120S with the custom APHE/HESH weapon | `aphe_and_hesh_override.blk` |
| `us_m2a4/us_m2a4_physics_550t_snippet.blk` | Mass/engine overrides (550 t), ground only | `vehicle_physics_550t_snippet.blk` |
| `it_l3_cc/it_l3_cc_nuke_setup.blk` | L3 CC carrying the nuke weapon setup | (unchanged) |

## flightmodels/

| File | What it is |
|---|---|
| `ask3lad_air_player.blk` | Player aircraft flightmodel (set up on `douglas_ad_4`). Its weapon slots point at the custom weapons. |
| `weaponPresets/ask3lad_air_custom.blk` | Weapon preset `ask3lad_custom`, referenced from the flightmodel. |

## missions/

- `ask3lad_testdrive.blk`: ground test drive. Player tank is `userVehicles/us_m2a4` with the `us_m1a2_sep3_abrams_default` preset and `460mm_jp_type91_navy_apc` shells (9999).
- `ask3lad_testdrive_air_3x.blk`: "Ask3lad Test Drive 3.0 - Air" (thrust x3, respawning targets, nuke event after 210 s).
