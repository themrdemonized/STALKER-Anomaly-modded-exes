# STALKER-Anomaly-modded-exes
Here is list of exe files for Anomaly 1.5.1 that contains all engine patches by community required for some advanced mods to work.
Here is the list of patches
* DLTX by MerelyMezz with my edits and bugfixes (https://www.moddb.com/mods/stalker-anomaly/addons/dltx-differential-ltx-loading), differences compare to original:
  * Attempting to override sections no longer crash the game, but prints the message into the log. All sections that triggers that error will be printed
  * Duplicate section errors now prints the root file where the error happened for easier checking mod_... ltxes
  * Fix of getting non-existing restrictor objects, observed by DAO mod (https://www.moddb.com/mods/stalker-anomaly/addons/dynamic-anomalies-overhaul-dao-read-description-please)
  * Print of class and script errors in console
  
* Shader Scopes by CrookR and enhanced by Edzan, comes ready to use in the archive, delete old version first
  * Dynamic zoom is disabled by default for alternative sights (can be enabled by adding scope_dynamic_zoom_alt = true to the weapon section). For example, if you take SVD Lynx or SVD PMC with March Tactical (or other sights with adjustable zoom) and switch to alternate sight, they wont have dynamic zoom anymore
  * The main sights with dynamic zoom and binoculars now normally remember their state.
  * Added console command sds_enable [on (default)/off] to enable/disable Shader Based 2D Scopes.
  * Added sds_speed_enable [on (default)/off] console command to disable/enable mouse speed (sensitivity) effect of scope_factor when aiming.
  * Added console command sds_zoom_enable [on (default)/off] with which you can disable /enable correction of max. zoom with scope_factor, if this option is enabled then max. zoom will be such as prescribed in settings regardless of scope_factor value, if this option is disabled then max. zoom will be sum of value prescribed in settings and the increase that gives scope_factor.
Above mentioned options are applicable only for scopes which have prescribed values in file scoperadii.script
 * Added alternative zoom control (toggle with new_zoom_enable [on/off (default)]
    * Minimal zoom is equal to either mechanical zoom or the one prescribed in section min_scope_zoom_factor.
    * The step of zoom adjustment is more precise. Also, it's possible to adjust the step of zoom with the console command zoom_step_count [1.0, 10.0], this option is also applicable to the binoculars.
 * In the new version all implementations from fakelens.script have moved directly to the engine. fakelens.script remained as a layer between the engine and scopeRadii.script
 
* ARX - Artefact & Anomalies Restoration eXperiment by Jurkonov (https://www.moddb.com/mods/stalker-anomaly/addons/arx-artefact-anomalies-restoration-experiment)
* Duty Expansion by GhenTuong and Tronex (https://www.moddb.com/mods/stalker-anomaly/addons/duty-expansion)
* Screen Space Shaders by Ascii1457 (https://www.moddb.com/mods/stalker-anomaly/addons/screen-space-shaders)

# Read the description PLEASE!!!
By default exes for ARX mod is in separate folder, if you dont want them, download STALKER-Anomaly-modded-exes.zip archive.
Unpack all directories directly into your Anomaly game folder, overwrite files if requested.
Delete shader cache in launcher before first launch of the game with new exes. You only have to do it once.

Patches folder contains diffs used to create new exes, they are used to compile your own exes if you need that

## How to make my own modded exe?
1. git clone https://bitbucket.org/anomalymod/xray-monolith.git
2. Open cloned repo in git console
3. apply the patches you want from patches folder of this modded exe repo, git apply <path_to_patch>
4. To compile the engine open the solution in VS2015, select all projects and configurations in Batch build and start a build.
