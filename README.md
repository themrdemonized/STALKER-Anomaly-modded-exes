# STALKER-Anomaly-modded-exes
Here is list of exe files for Anomaly 1.5.1 that contains all engine patches by community required for some advanced mods to work.
Here is the list of patches
* DLTX by MerelyMezz with my edits and bugfixes (https://www.moddb.com/mods/stalker-anomaly/addons/dltx-differential-ltx-loading), differences compare to original:
  * Attempting to override sections no longer crash the game, but prints the message into the log. All sections that triggers that error will be printed
  * Duplicate section errors now prints the root file where the error happened for easier checking mod_... ltxes
  * Fix of getting non-existing restrictor objects, observed by DAO mod (https://www.moddb.com/mods/stalker-anomaly/addons/dynamic-anomalies-overhaul-dao-read-description-please)
  * Print of class and script errors in console
  
* Shader Scopes by CrookR (https://www.moddb.com/mods/stalker-anomaly/addons/shader-based-2d-scopes-151dx11engine-mod)
* ARX - Artefact & Anomalies Restoration eXperiment by Jurkonov (https://www.moddb.com/mods/stalker-anomaly/addons/arx-artefact-anomalies-restoration-experiment)
* Duty Expansion by GhenTuong and Tronex (https://www.moddb.com/mods/stalker-anomaly/addons/duty-expansion)
* Boomsticks And Sharpsticks by Mortan, Mich and co. (https://www.moddb.com/mods/stalker-anomaly/addons/boomsticks-and-sharpsticks)
* Screen Space Shaders by Ascii1457 (https://www.moddb.com/mods/stalker-anomaly/addons/screen-space-shaders)

# Read the description PLEASE!!!
By default exes for ARX mod is in separate folder, if you dont want them, download STALKER-Anomaly-modded-exes.zip archive.
Unpack both bin and db directories directly into your Anomaly game folder, overwrite files if requested.
Delete shader cache in launcher before first launch of the game with new exes. You only have to do it once.

Patches folder contains diffs used to create new exes, they are used to compile your own exes if you need that

## How to make my own modded exe?
1. git clone https://bitbucket.org/anomalymod/xray-monolith.git
2. Open cloned repo in git console
3. apply the patches you want from patches folder of this modded exe repo, git apply <path_to_patch>
4. To compile the engine open the solution in VS2015, select all projects and configurations in Batch build and start a build.
