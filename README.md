# STALKER-Anomaly-modded-exes

Here is list of exe files for Anomaly 1.5.2 that contains all engine patches by community required for some advanced mods to work.

# Read the instructions PLEASE!!!
![image](https://github.com/themrdemonized/STALKER-Anomaly-modded-exes/assets/46323442/6c5b89c8-c749-4945-b842-ec0a7c4f748a)


* Install the latest Visual C++ Redistributables: https://www.techpowerup.com/download/visual-c-redistributable-runtime-package-all-in-one/
* Download STALKER-Anomaly-modded-exes.zip archive.
* Unpack all directories directly into your Anomaly game folder, overwrite files if requested.
* Delete shader cache in launcher before first launch of the game with new exes. You only have to do it once.

# List of patches

* DLTX by MerelyMezz with edits and bugfixes by demonized, differences compare to original:
  * Attempting to override sections no longer crash the game, but prints the message into the log. All sections that triggers that error will be printed
  * Duplicate section errors now prints the root file where the error happened for easier checking mod_... ltxes
  * Print of class and script errors in console
  * DLTX received possibility to create section if it doesn't exists and override section if it does with the same symbol `@`.
  Below is the example for `newsection` that wasn't defined. Firstly its created with one param `override = false`, then its overriden with `override = true`

  ```
  @[newsection]
  override = false

  @[newsection]
  override = true
  
  ```

  * DLTX received possibility to add items to parameter's list if the parameter has structure like 
  
  ```name = item1, item2, item3```
  
    * `>name = item4, item5` will add item4 and item5 to list, the result would be `name = item1, item2, item3, item4, item5`
    * `<name = item3` will remove item3 from the list, the result would be `name = item1, item2`
    * example for mod_system_...ltx: 
    
    ```
      ![info_portions]
      >files                                    = ah_info, info_hidden_threat

      ![dialogs]
      >files                                    = AH_dialogs, dialogs_hidden_threat
      
      ![profiles]
      >files                                    = npc_profile_ah, npc_profile_hidden_threat
      >specific_characters_files                = character_desc_ah, character_desc_hidden_threat
    ```

  * Here you can get the LTXDiff tool with set of scripts for converting ordinary mods to DLTX format (https://www.moddb.com/mods/stalker-anomaly/addons/dltxify-by-right-click-for-modders-tool).

* DXML by demonized
  * Allows to modify contents of loaded xml files before processing by engine by utilizing Lua scripts
  * For more information see DXML.md guide.

* Possibility to unlocalize Lua variables in scripts before loading, making them global to the script namespace
  * For unlocalizing a variable in the script, please refer to documentation in test file in `gamedata/configs/unlocalizers` folder

* Doppler effect of sounds based on code by Cribbledirge and edited by demonized.
* True First Person Death Camera, that will stay with player when he dies and will react accordingly to player's head transforms, with possibility to adjust its settings.
  * Known bugs:
    * If the player falls with face straight into the ground, the camera will clip underground due to model being clipped as well with

* Pseudogiant stomps now can kill and damage any object, stalker or mutant, instead of only actor, configurable via console commands

* New console commands for demo record stuff

* Added CGameObject::NetSpawn and NetDestroy callbacks to Lua

* Added `gameobjects_registry` table in `callbacks_gameobject.script` that contains all online game objects and updates accordingly. Additionally, a global iterator `game_objects_iter` added that will go through all online game objects

  ```lua
  for obj in game_objects_iter() do
    printf(obj:section())
  end
  ```

* In case of missing translation for a string, the engine will fallback to english text for this string.

* Additional functions and console commands described in `lua_help_ex.script`

* Additional callbacks described in `callbacks_gameobject.script`

* Moved solution to Visual Studio 2022, In case you have problems, make sure you installed the latest Visual C++ Redistributables. You can find them here: https://www.techpowerup.com/download/visual-c-redistributable-runtime-package-all-in-one/

* Additional edits and bugfixes by demonized
  * Restored "Fatal Error" MessageBox popup in case of encountering fatal engine errors like it was on Windows 7 or lower
  * In case of typical first person model/animation errors, the game will print the section that has defined model
  * MAX_TRIS const increased from 1024 to 16384
  * Enabled death animations for CWeaponAutomaticShotgun class
  * Fixed sorting news in News Tab in PDA
  * Added getting material of ray_pick() result with all of its properties
  * Potential fix for stuck monsters from OGSR Engine repo in `control_animation_base_accel.cpp`
  * Removed maximum engine limit of 5 artefacts on belt
  * Added printing of engine stack trace in the log via StackWalker library https://github.com/JochenKalmbach/StackWalker
   * To make it work you need to download `pdb` file for your DX/AVX version and put it into same place as `exe` file. PDB files are here: https://github.com/themrdemonized/xray-monolith/releases/latest

* Fixes and features by Lucy
  * Reshade shaders won't affect UI, full addon support version of Reshade is required (see TROUBLESHOOTING for details)
  * fix for hands exported from blender (you no longer have to reassign the motion references)
  * fix for silent error / script freeze when getting player accuracy in scripts
  * animation fixes (shotgun shell didn't sync with add cartridge and close anims)
  * game no longer crashes on missing item section when loading a save (should be possible to uninstall most mods mid-game now)
  * fix for mutants stuck running in place (many thanks to Arszi for finding it)
  * fix for two handed detector/device animations (swaying is now applied to both arms instead of only the left one)
  * it's now possible to play script particle effects in hud_mode with :play(true) / :play_at_pos(pos, true)
  * the game will now display a crash message when crashing due to empty translation string
  * Scripted Debug Render functions
  * Debug renderer works on DX10/11
    * Many thanks to OpenXRay and OGSR authors:
    * https://github.com/OpenXRay/xray-16/commit/752cfddc09989b1f6545f420a5c76a3baf3004d7
    * https://github.com/OpenXRay/xray-16/commit/a1e581285c21f2d5fd59ffe8afb089fb7b2da154
    * https://github.com/OpenXRay/xray-16/commit/c17a38abf6318f1a8b8c09e9e68c188fe7b821c1
    * https://github.com/OGSR/OGSR-Engine/commit/d359bde2f1e5548a053faf0c5361520a55b0552c
  * Exported a few more vector and matrix functions to lua
  * Optional third argument for world2ui to return position even if it's off screen instead of -9999
  * Unified bone lua functions and made them safer
  * It's now possible to get player first person hands bone data in lua

* Fixes and features by DPurple
  * Fix of using `%c[color]` tag with multibyte font causing unexpected line ending by DPurple
  * Ability to autosave the game before crash occurs, can be disabled with console command `crash_save 0` and enabled with `crash_save 1`. Maximum amount of saves can be specified with command `crash_save_count <number>`, where number is between 0 to 20 (default is 10)

* Smooth Particles with configurable update rate by vegeta1k95
  * To change update rate use console command `particle_update_mod` which takes values from 0.04 to 10.0 (default is 1.0). 1.0 corresponds to 30hz, 0.5 - 60hz and so on. The setting is also available in the options menu in "Modded Exes" group
  * Possibility to set particle update delta in milliseconds in .pe files for fine tuning with `update_step` field

* Shader Scopes by CrookR and enhanced by Edzan, comes ready to use in the archive, delete old version first

  * Dynamic zoom is disabled by default for alternative sights (can be enabled by adding scope_dynamic_zoom_alt = true to the weapon section). For example, if you take SVD Lynx or SVD PMC with March Tactical (or other sights with adjustable zoom) and switch to alternate sight, they wont have dynamic zoom anymore
  * Possibility to set alternative sight crosshair and zoom_factor with `scope_texture_alt = <path to texture>` and `scope_zoom_factor_alt = <number>` parameters in weapon ltx
  * The main sights with dynamic zoom and binoculars now normally remember their state.
  * Added console command sds_enable [on (default)/off] to enable/disable Shader Based 2D Scopes.
  * Added sds_speed_enable [on (default)/off] console command to disable/enable mouse speed (sensitivity) effect of scope_factor when aiming.
  * Added console command sds_zoom_enable [on (default)/off] with which you can disable /enable correction of max. zoom with scope_factor, if this option is enabled then max. zoom will be such as prescribed in settings regardless of scope_factor value, if this option is disabled then max. zoom will be sum of value prescribed in settings and the increase that gives scope_factor.

  Above mentioned options are applicable only for scopes which have prescribed values in file scoperadii.script

  * Added alternative zoom control (toggle with new_zoom_enable [on/off (default)]
    * Minimal zoom is equal to either mechanical zoom or the one prescribed in section min_scope_zoom_factor.
    * The step of zoom adjustment is more precise. Also, it's possible to adjust the step of zoom with the console command zoom_step_count [1.0, 10.0], this option is also applicable to the binoculars.
  * In the new version all implementations from fakelens.script have moved directly to the engine. fakelens.script remained as a layer between the engine and scopeRadii.script

* All settings can be edited from the game options in "Modded Exes" tab
![image](http://puu.sh/JC40Y/9315119150.jpg)

## TROUBLESHOOTING
* Q: The game crashes when using reshade and trying to switch resolution/change graphics settings/init `vid_restart` command
* A: This is due to Reshade versions shenanigans. The latest tested version that doesn't crash while doing stuff in question is 5.7.0, you can download it here: https://reshade.me/downloads/ReShade_Setup_5.7.0_Addon.exe. If you wish to use later versions, try not to change graphics settings with them.

## Below are the edits that are supplemental to the mods, the mods themselves **are not included**, download the mods by the links. If mods in the links provide their own exes, you can ignore them, all necessary edits are already included on this page. 

* BaS engine edits by Mortan (https://www.moddb.com/mods/stalker-anomaly/addons/boomsticks-and-sharpsticks)

* Screen Space Shaders by Ascii1457 (https://www.moddb.com/mods/stalker-anomaly/addons/screen-space-shaders)

* Heatvision by vegeta1k95 (https://www.moddb.com/mods/stalker-anomaly/addons/heatvision-v02-extension-for-beefs-nvg-dx11engine-mod/)

## How to make my own modded exe?

How to compile exes:
1. Fork xray-monolith repo from https://github.com/themrdemonized/xray-monolith
2. Clone the fork onto your pc
3. Select all-in-one-vs2022 branch
4. Compile the engine-vs2022.sln solution with VS2022
5. For batch builds of all configurations use `batch_build.bat` in xray-monolith repo
6. For successful compilation, **the latest build tools with MFC and ATL libraries is required**

## Changelog
**2024.01.30**
* Hrust: fix volumetric fog

**2024.01.27**
* Fixed: `[error]Expression    : left_eye_bone_id != u16(-1) && right_eye_bone_id != u16(-1), CBaseMonster::update_eyes_visibility`
* Reenabled robinhood hashing

**2024.01.26**
* Temporary disabled robinhood hashing, reason: `[error]Expression    : left_eye_bone_id != u16(-1) && right_eye_bone_id != u16(-1), CBaseMonster::update_eyes_visibility`
* Print Lua stack on `you are trying to use a destroyed object` error
* Print error message for CAI_Stalker::net_Export in the log when crashing
* MagielBruntink: Print missing `.ogg` comments only in debug mode

**2024.01.18**
* MagielBruntink: Increased lua_gcstep default to 400 and allow console editing via `lua_gcstep` command 

**2024.01.13**
* Fixed typo in GameMtlLib.cpp
* OneMorePseudoCoder: Memory leaks fixes

**2024.01.11**
* Added possibility to override gamemtl.xr materials and define new ones via `materials.ltx` and `material_pairs.ltx` files. Please read the guide in those files in `gamedata/materials` folder
* Removed `pSettings->line_exist(sect_name,"fire_point")==pSettings->line_exist(sect_name,"fire_bone")` game crash check
* Raised `GAMEMTL_SUBITEM_COUNT` for material sounds and particles constant from 4 to 10
* Fixed rare unlocalizer crash and crashes on Linux because of this bug

**2024.01.04**
* New `db.actor` exports
  * `db.actor:get_actor_crouch_coef()`
  * `db.actor:set_actor_crouch_coef(float)`
  * `db.actor:get_actor_climb_coef()`
  * `db.actor:set_actor_climb_coef(float)`
  * `db.actor:get_actor_walk_strafe_coef()`
  * `db.actor:set_actor_walk_strafe_coef(float)`
  * `db.actor:get_actor_run_strafe_coef()`
  * `db.actor:set_actor_run_strafe_coef(float)`
  * `db.actor:get_actor_sprint_strafe_coef()`
  * `db.actor:set_actor_sprint_strafe_coef(float)`
* Added `hit_fraction_actor` field for helmet upgrades
* Added filename field for section items
* Added ini script methods for DLTX
  * dltx_print(string sec = nil, string line = nil): prints information about sections. If sec is nil, then whole file will be printed. If section is provided and line is nil, then the whole section will be printed. If both provided, only the provided line will be printed
  * dltx_get_filename_of_line(string sec, string line): returns filename that was used for a line in the section
  * dltx_get_section(string sec): returns a table with section information with structure:
  ```
    {
      [<section_1>] = {
        name = <section_1>
        value = <value_1>
        filename = <filename_1>
      }
      ...
    }
  ```
  * dltx_is_override(string sec, string line): returns true if line in section was overriden by DLTX mod

**2023.12.30**
* Added `bullet_id` field to script hit struct
* Restored behaviour of `r_bool_ex` and `r_value` functions to match vanilla code
* Filtered useless lines in stack trace if `pdb` file is not present

**2023.12.24**
* SSS update
* Minimap shape fix moved into option. Add `ratio_mode = "1"` in `zone_map_*.xml` files in `level_frame` node to enable the new code

**2023.12.23**
* DLTX: simplified possibility to delete whole section, now its just enough to write `!![section]` to completely delete it
* Longreed: added possibility for minimap frame to have a custom rectangular shape 

**2023.12.17**
* Fixed getting wrong values in ini cache due to robin_hood hashing, reenabled the library

**2023.12.16u1**
* Temporary disabled robin_hood hashing to fix crashes

**2023.12.16**
* `xr_unordered_map` type is replaced with robin_hood hashing from https://github.com/martinus/robin-hood-hashing. Additionaly introducing `xr_unordered_set` and `xr_pair` types based on this library
* Added engine-based caching ini values in CIniFile class
* Added Lua function `ini_file:get_filename()` to return the filename of file
* Replaced `ini_file_ex` class with implementation that is derived from `ini_file`, fully backwards compatible with existing `ini_file_ex`
* `level.iterate_nearest` will sort objects by ascending distance before executing Lua callback
* Added `game.update_pda_news_from_uiwindow(CUIWindow*)` function to update news in PDA from news window on the HUD
* Added printing of engine stack trace in the log via StackWalker library https://github.com/JochenKalmbach/StackWalker
  * To make it work you need to download `pdb` file for your DX/AVX version and put it into same place as `exe` file. PDB files are here: https://github.com/themrdemonized/xray-monolith/releases/latest

**2023.12.09u1**
* Fixed crash on failed `tonumber` conversion when using `SYS_GetParam`

**2023.12.09**
* Disabled get_console warning for bool variables
* Lua unlocalizer supports `_g.script`
* Lua unlocalizer filename check is insensitive, ie `[_G]` is the same as `[_g]`
* Disabled Lua caches for ini files when using `SYS_GetParam` and reading variables such as `r_string_ex` in favor of engine functions and to reduce memory footprint and possible GC calls
* Added undocumented Lua extensions exports into `lua_help_ex.script`
* Added new callback `on_news_received` to manipulate game news when they are displayed
* Added `game.change_game_news_show_time` function to postpone fadeout of game news
* Added `throttle(func, time)` function to throttle calls to `func` by `time` in milliseconds


**2023.12.06**
* Added gun object and gun owner params to `actor_on_hud_animation_mark` and `
actor_on_hud_animation_play` callbacks
* Warnings when script fails to get console variables due to incorrect type

**2023.12.02**
* Added possibility to edit freelook angle limit with console command `freelook_cam_limit`
* Using /Ob3 flag for compiling, theoretically should increase performance a bit

**2023.11.28**
* Lucy: add a motion mark to the draw/holster animations of the flashlight to trigger when the light turns on or off

**2023.11.25**
* Added functions for manipulating map spot graphics
  * `level.map_get_object_spot_static(u16 id, LPCSTR spot_type)` will return CUIStatic object of the spot on the map
  * `level.map_get_object_minimap_spot_static(u16 id, LPCSTR spot_type)` will return CUIStatic object of the spot on the minimap
* If DXML query is invalid, the game will crash with an error message and callstack

**2023.11.22**
* GhenTuong: parametrized functions in dialogs (precondition, action, script_text tags)
  * '=' and '!' can be used and work same as condlist. `=` is true condition, `!` is false
  * () can be used to input parameters. Parameters are separated by ':'
  * Example: `<precondition>!file.func(dolg:1:false)</precondition>`
  ```lua
    function func(a,b,dialog_id,phrase_id,next_id,p)
      printf("%s %s %s %s %s %s", a, b, dialog_id, phrase_id, next_id, table.concat(p, " "))
    end
  ```
* Added option to write timestamps in console and log file. Type `log_timestamps 1` in console to turn on the feature
* DXML query function will always return table even with invalid queries

**2023.11.15**
* Fixed crash when trying to use alt aim on Mosin-like scopes

**2023.11.14**
* Fixed issue when having grenade launcher attached will trigger shader scopes

**2023.11.12**
* Fixed physics initialization when obj:force_set_position(pos, true) is used
* Fixed not working shader scopes when alternative sight is an optic
* Removed (DLTX, DXML, ...) string from version title in the main menu screen

**2023.10.27**
* Reverted change to mouse wheel, its not inverted now
* Toggle inverted mouse wheel with console command `mouse_wheel_invert_zoom 1` 

**2023.10.20**
* Removed monster stuck fix due to big fps loses it causes. You can turn it back via console command `monster_stuck_fix 1`

**2023.10.17**
* SSS 18 update
* Lucy: specifying a custom UI bone for Svarog/Veles in the hud sections of detectors via `detector_ui_bone` property
* `string_table_error_msg` console command to print missing translation strings 

**2023.10.05**
* Fixed occasional crash when right click on PDA map
* `db.actor:set_actor_direction` supports roll as third argument

**2023.09.30**
* Added possibility to disable weapon switch with mouse wheel, use console command `mouse_wheel_change_weapon 0`
* Fixed invisible console bug when there are invisible debug gizmos being used
* `db.actor:set_actor_direction` supports pitch as a second argument
* Minor fixes of right click PDA callback
* Added print of stack when incorrect bone id provided for bone functions
* Moved LuaJIT to VS2022 toolchain and applied optimization flags for build 

**2023.09.22**
* Added `on_map_right_click` callback, which allows to right click anywhere on the map and fire user functions at projected real world position. Refer to `callbacks_gameobject.script`
* Added possibility to zoom in and out relative to cursor on the map, instead of always center
* Fixed possible crash when using script functions for getting bone properties
* Added temporary fix for view NPC PDA's function not working correctly if 2D PDA is used
* Added `player_hud` functions documentation in `lua_help_ex.script`
* Added global functions
  * `nextTick(f, n)` will execute function f on the next n-th game tick. Your function should return true if you want to fire it once, just like with time events
  * `print_tip(s)` will print information in news feed as well as in console 

**2023.09.06**
* Moved build procedure to Github Actions in https://github.com/themrdemonized/xray-monolith
* Apart from exes themselves, https://github.com/themrdemonized/xray-monolith repo will contain PDB files if you want to debug the code yourself
* Added `angle` and `force_set_angle` functions for game objects by GhenTuong
* Added `get_modded_exes_version` function

**2023.09.02**
* Performance improvements when calling level.object_by_id function, thanks Lucy for the hint

**2023.08.29**
* Added `apply_torque` function to `get_physics_shell()` Lua object to apply rotational force to models
* Fixes by ![clayne](https://github.com/clayne)
  * https://github.com/themrdemonized/xray-monolith/pull/14

**2023.08.19**
* Removed diff files, please fork XRay-Monolith repo to work on engine and submit changes via pull requests: https://github.com/themrdemonized/xray-monolith
* Added boneId parameter to `on_before_hit_after_calcs` callback
* More descriptive error message on crashes if it was caused by Lua
* Fixes by ![clayne](https://github.com/clayne)
  * https://github.com/themrdemonized/xray-monolith/pull/1
  * https://github.com/themrdemonized/xray-monolith/pull/2
  * https://github.com/themrdemonized/xray-monolith/pull/3
  * https://github.com/themrdemonized/xray-monolith/pull/4
  * https://github.com/themrdemonized/xray-monolith/pull/5
  * https://github.com/themrdemonized/xray-monolith/pull/6
  * https://github.com/themrdemonized/xray-monolith/pull/7
  * https://github.com/themrdemonized/xray-monolith/pull/8
  * https://github.com/themrdemonized/xray-monolith/pull/9
  * https://github.com/themrdemonized/xray-monolith/pull/10
  * https://github.com/themrdemonized/xray-monolith/pull/11
  * https://github.com/themrdemonized/xray-monolith/pull/12
  * https://github.com/themrdemonized/xray-monolith/pull/13
  
**2023.08.09**
* Reduced size of exes
* Changes to build procedure to solve not starting game with certain CPU configurations
* Restored original behaviour of `bone_position` and `bone_direction` functions to solve issues with some mods. If incorrect bone_id is specified for them, the warning will be printed in the console

**2023.08.08**
* SSS update
* Attempt to resolve not starting game with certain CPU configurations. Huge thanks to ![clayne](https://github.com/clayne) for contributing time and efforts to solve the problem

**2023.08.07**
* Lucy: Fix of broken left hand animations

**2023.08.06**
* SSS update

**2023.08.05**
* Fixed possible malfunction of shader scopes by enforcing `r__fakescope 1` on first update
* New callback `on_before_hit_after_calcs` that will fire just before applying hit to an entity, refer to `callbacks_gameobject.script`
* Possibility to keep hud drawed and affected when using `level.set_cam_custom_position_direction` function, refer to `lua_help_ex.script`
* Features and fixes by Lucy:
  * Device/Detector animations can now use the lead_gun bone if their hud section has lh_lead_gun = true (script animations can also use this config toggle in their section)
  * Device/Detector amera animations will now play even if there's something in your right hand
  * Cleaned up player_hud animation code

**2023.07.28**
* Features by LVutner:
  * Added support for Shader Scopes on DX9
  * Added support for Heatvision on DX10
* New file `aaaa_script_fixes_mp.script` that will contain monkeypatches for fixing some vanilla scripts
  * Fixed incorrect behaviour of `actor_on_item_before_pickup` callback
* Fixed unable to switch to russian language when typing text
* Added Troubleshooting section in readme file

**2023.07.24**
* Exes now are built with Visual Studio 2022. In case you have problems, make sure you installed the latest Visual C++ Redistributables. You can find them here: https://www.techpowerup.com/download/visual-c-redistributable-runtime-package-all-in-one/
* Fixes and features by Lucy
  * Reshade shaders won't affect UI, full addon support version of Reshade is required
  * fix for hands exported from blender (you no longer have to reassign the motion references)
  * fix for silent error / script freeze when getting player accuracy in scripts
  * animation fixes (shotgun shell didn't sync with add cartridge and close anims)
  * game no longer crashes on missing item section when loading a save (should be possible to uninstall most mods mid-game now)
  * fix for mutants stuck running in place (many thanks to Arszi for finding it)
  * fix for two handed detector/device animations (swaying is now applied to both arms instead of only the left one)
  * it's now possible to play script particle effects in hud_mode with :play(true) / :play_at_pos(pos, true)
  * the game will now display a crash message when crashing due to empty translation string
  * Scripted Debug Render functions, drawing debug boxes, spheres and lines 
  * Debug renderer works on DX10/11
    * Many thanks to OpenXRay and OGSR authors:
    * https://github.com/OpenXRay/xray-16/commit/752cfddc09989b1f6545f420a5c76a3baf3004d7
    * https://github.com/OpenXRay/xray-16/commit/a1e581285c21f2d5fd59ffe8afb089fb7b2da154
    * https://github.com/OpenXRay/xray-16/commit/c17a38abf6318f1a8b8c09e9e68c188fe7b821c1
    * https://github.com/OGSR/OGSR-Engine/commit/d359bde2f1e5548a053faf0c5361520a55b0552c
  * Exported a few more vector and matrix functions to lua
  * Optional third argument for world2ui to return position even if it's off screen instead of -9999
  * Unified bone lua functions and made them safer
  * It's now possible to get player first person hands bone data in lua
* All new functions are added in `lua_help_ex.script`

**2023.07.21**
* Added `level.get_target_pos()` and `level.get_target_result()` functions, refer to lua_help_ex.script
* Added `actor_on_changed_slot` callback, refer to `callbacks_gameobject.script`
* Hotfix of possible mouse unfocus from game window by Lucy

**2023.07.09**
* Added `anomaly_on_before_activate` event for NPCs in callbacks_gameobject.script to make them less vurnerable to anomalies if pathfinding is enabled
* Added possibility to set custom rotation angle of the wallmark, please refer to lua_help_ex.script in wallmarks_manager class
* 3D UI no longer clip with the sky and visibility in the dark fix by Lucy

**2023.07.07**
* Added `bullet_on_update` callback, please refer to callbacks_gameobject.script file for available info about new callback
* Added `life_time` field to bullet table

**2023.07.04**
* `ai_die_in_anomalies` command now works in real time
* Revised the code that described behaviour of NPCs and monsters when they are near anomalies
  * Anomalies are always visible for AI on engine level, previously it was defined by console variable `ai_die_in_anomalies`
  * Monsters will always try to evade anomalies
  * NPCs behaviour works this way
    * if `ai_die_in_anomalies` is 1, they will try to evade anomalies and will receive damage if they cant
    * otherwise its defined per NPC (by default its vanilla behaviour - no pathfinding and no damage) that can be changed via scripts
* New game object functions for NPCs:
  * npc:get_enable_anomalies_pathfinding() - get the state of anomalies pathfinding
  * npc:set_enable_anomalies_pathfinding(bool) - enable or disable anomalies pathfinding
  * npc:get_enable_anomalies_damage() -  get the state of anomalies damage
  * npc:set_enable_anomalies_damage(bool) -  enable or disable anomalies damage

**2023.07.03**
* Added level.map_remove_all_object_spots(id) function

**2023.07.01**
* Mouse wheel callback `on_mouse_wheel` can consume input if flags.ret_value is false, please refer to callbacks_gameobject.script file for available info about new callback
* Added global variable MODDED_EXES_VERSION

**2023.06.30**
* Added mouse wheel callback `on_mouse_wheel`, please refer to callbacks_gameobject.script file for available info about new callback
* Added `db.actor:get_actor_lookout_coef()` and `db.actor:set_actor_lookout_coef(float)` functions for manipulating maximum lean angle
* Fix of gun disappearing when switching between 1st and 3rd person view

**2023.06.17**
* Added `bullet_on_init` callback, please refer to callbacks_gameobject.script file for available info about new callback
* Small cleanup of dxml_core.script

**2023.06.04**
  * SSS update

**2023.05.29**
  * In case of missing translation for a string, the engine will fallback to english text for this string. To disable the behaviour, use console command `use_english_text_for_missing_translations 0`

**2023.05.27**
  * `local res, obj_id = game.ui2world(pos)` for unprojecting from ui coordinates (ie. mouse cursor) to the world

**2023.05.22**
  * `alife():iterate_object(function(se_obj))` function to iterate all objects that are in the game
  * `level.set_cam_custom_position_direction(Fvector position, Fvector direction)` and `level.remove_cam_custom_position_direction()` to manipulate camera in world coordinates
  * CWeapon additional methods: world model on stalkers adjustments
    * function Set_mOffset(Fvector position, Fvector orientation)
    * function Set_mStrapOffset(Fvector position, Fvector orientation)
    * function Set_mFirePoint(Fvector position)
    * function Set_mFirePoint2(Fvector position)
    * function Set_mShellPoint(Fvector position) 

**2023.04.27**
* SSS update

**2023.04.15**
* Added `get_artefact_additional_inventory_weight()` and `set_artefact_additional_inventory_weight(float)` for artefacts

**2023.04.09**:
* Put extra shader files in 000_shader_placeholder.db0, CLEAN SHADER CACHE IS REQUIRED

**2023.04.08**:

* SSS update
* Smooth Particles with configurable update rate by vegeta1k95
  * To change update rate use console command `particle_update_mod` which takes values from 0.04 to 10.0 (default is 1.0). 1.0 corresponds to 30hz, 0.5 - 60hz and so on. The setting is also available in the options menu in "Modded Exes" group
  * Possibility to set particle update delta in milliseconds in .pe files for fine tuning with `update_step` field

**2023.03.31**:

* SSS update
* Removed maximum engine limit of 5 artefacts on belt

**2023.03.25**:

* Potential fix for stuck monsters from OGSR Engine repo in `control_animation_base_accel.cpp`
* Added `bullet_on_impact` and `bullet_on_remove` callbacks, please refer to callbacks_gameobject.script file for available info about new callbacks

**2023.03.19**:

* Added true first person death camera (enabled by default), that will stay with player when he dies and will react accordingly to player's head transforms. Additional console commands
  * `first_person_death` // Enable First Person Death Camera
  * `first_person_death_direction_offset` // FPD Camera Direction Offset (in DEGREES)
  * `first_person_death_position_offset` // FPD Camera Position Offset (x, y, z)
  * `first_person_death_position_smoothing` // FPD Camera Position Change Smoothing
  * `first_person_death_direction_smoothing` // FPD Camera Direction Change Smoothing
  * `first_person_death_near_plane_offset` // FPD Camera Near Plane Offset

[![Watch the video](https://img.youtube.com/vi/Jm-DRNqnak0/default.jpg)](https://youtu.be/Jm-DRNqnak0)

* Fixed heatvision effects not applied to the player hands
* Added options menu for modded exes settings
  * From options menu you can adjust all added modded exes parameters, such as for Shader Scopes, Sound Doppler, FPD Camera and so on

![image](http://puu.sh/JC40Y/9315119150.jpg)

* Added `level.get_music_volume()` and `level.set_music_volume()` Lua functions to adjust music volume in runtime without messing with console commands

**2023.03.15**:

* Stability updates to heatvision sources
* DXML 3.0 update:
  * DXML now uses own storage for callbacks to ensure they are fired accordingly to registering order
  * Added `insertFromXMLFile` function to read contents of xml file to insert into xml_obj
  * Added optional parameter useRootNode to `insertFromXMLString` and `insertFromXMLFile` functions that will hint DXML to insert contents from a root node of parsed XML instead of the whole file (default: false) 

**2023.03.11**:

* Added heatvision support by vegeta1k95 (https://www.moddb.com/mods/stalker-anomaly/addons/heatvision-v02-extension-for-beefs-nvg-dx11engine-mod/)
* Fixed too big FOV when using shader scopes with `new_zoom_enable` command enabled

**2023.03.09**:

* Added possibility to unlocalize Lua variables in scripts before loading, making them global to the script namespace
  * For unlocalizing a variable in the script, please refer to documentation in test file in `gamedata/configs/unlocalizers` folder
* Fixed the bug where `scope_factor` settings were applied to disabled shader scopes or scopes without defined radius for shader effect
* Fixed non-working adjustable scopes upgrade for weapons

**2023.03.05**:

* Fixed the bug where the weapon with attached adjustable scope and grenade launcher will allow to zoom in with GL. To explicitly enable zooming with active grenade launcher, for whatever reason, add `scope_dynamic_zoom_gl = true` in weapon section in its .ltx file
* Possibility to add shader scopes to alternative sights
  * `scope_dynamic_zoom_alt = true` will enable adjustable scope for alt. sight
  * `scope_texture_alt = <path to texture>` will allow to specify what crosshair to use for alt. sight
* Correct zoom_factor calculation for adjustable scopes with shader scopes enabled, you wont get any extra zoom from shader on top of engine FOV
* `scope_factor` console command that changes zoom by shader scopes now works in real time
* Lowered chromatic abberation and scope blur effect, increasing the quality of image  

**2023.02.20**:

* New SSS update
* New demo-record.diff that contains these changes

  * New console commands:
    * `demo_record_blocked_input 1` will start demo_record but you won't be available to move it or stop it, its intended for manipulation via scripts executing console commands below. The console and Esc key are available
    * `demo_record_stop` will stop all launched `demo_record` commands, including with blocked input ones 
    * `demo_set_cam_direction <head, pitch, roll>` will set the direction the camera is facing and its roll. The parameters are in RADIANS, beware. Use this with `demo_set_cam_position <x, y, z>` to manipulate camera via scripts

**2023.02.18**:

* New SSS update

**2023.02.16**:

* Added `gameobjects_registry` table in `callbacks_gameobject.script` that contains all online game objects and updates accordingly. Additionally, a global iterator `game_objects_iter` added that will go through all online game objects

  ```lua
  for obj in game_objects_iter() do
    printf(obj:section())
  end
  ```

* Pseudogiant stomps now can kill and damage any object, stalker or mutant, instead of only actor. New callbacks provided for pseudogiants attacks in callbacks_gameobject.script

  * To disable new functionality, type in console `pseudogiant_can_damage_objects_on_stomp 0`

**2023.01.28**:

* DLTX received possibility to create section if it doesn't exists and override section if it does with the same symbol `@`.
Below is the example for `newsection` that wasn't defined. Firstly its created with one param `override = false`, then its overriden with `override = true`

```
@[newsection]
override = false

@[newsection]
override = true

```
* Added `bone_direction()` function for game objects
* Updated `lua_help_ex.script` with new functions available

**2023.01.23**:

* MAX_TRIS const increased from 1024 to 16384

**2023.01.13**:

* Fix corrupted print of duplicate section

**2023.01.06**:

* In case of typical first person model/animation errors, the game will print the section that has defined model

**2023.01.03**:

* Added CGameObject::NetSpawn and NetDestroy callbacks to Lua (file callbacks_gameobject.script), to register callback use

  ```lua
  RegisterScriptCallback("game_object_on_net_spawn", function(obj))
  RegisterScriptCallback("game_object_on_net_destroy", function(obj))
  ```

* DXML will no longer process translation strings of non eng/rus languages, they aren't supported yet
* New lua_help_ex.script file where new engine exports will be described
* Exported additional CWeapon functions considering weapon's RPM, handling and recoil
* Exported functions to get and set actors walk accel and walkback coeff

  ```lua
  db.actor:get_actor_walk_accel()
  db.actor:set_actor_walk_accel(float)
  db.actor:get_actor_walk_back_coef()
  db.actor:set_actor_walk_back_coef(float)
  ```
  * DLTX received possibility to add items to parameter's list if the parameter has structure like 
  
  ```name = item1, item2, item3```
  
    * `>name = item4, item5` will add item4 and item5 to list, the result would be `name = item1, item2, item3, item4, item5`
    * `<name = item3` will remove item3 from the list, the result would be `name = item1, item2`
    * example for mod_system_...ltx: 
    
    ```
      ![info_portions]
      >files                                    = ah_info, info_hidden_threat

      ![dialogs]
      >files                                    = AH_dialogs, dialogs_hidden_threat
      
      ![profiles]
      >files                                    = npc_profile_ah, npc_profile_hidden_threat
      >specific_characters_files                = character_desc_ah, character_desc_hidden_threat
    ```

* Exported distance_to_xz_sqr() function of Fvector
* Redesigned duplicate section error, it will additionally print what file adds the section in the first place in addition to the file that has the duplicate
