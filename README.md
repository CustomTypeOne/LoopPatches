# LoopPatches

# PAF-Switcher-NegativeIOB Patch

This patch modifies Loop for 3 new features:
- Alternate Partial Bolus Application Factor (PAF) allows you to adjust the 40% default used when determining what percentage of the calculated AB dose that Loop delivers.
- Automatic Strategy Switcher allows you to configure a threshold where Loop automatically switches between TB (<= threshold) and AB (> threshold). You must set Loop to AB mode and enable this setting for it to function. If you are in TB only, it will not auto switch you to AB.
- Negative IOB Factor is a percentage you can use to adjust the effect of negative IOB. During stubborn lows, Loop will frequently try to dose too much of the negative IOB as a recovery. This restricts Loop to only use this percentage of the negative IOB in a dose.

To apply the patch, you MUST apply both files. 
The "Loop-" file should be saved to LoopWorkspace/Loop/ and "LoopKit-" should be saved to LoopWorkspace/LoopKit/
Open a terminal to the above folders and run: git apply patchname.txt
The only acceptable erros to be shown are "whitespace" errors

To keep from needing to modify these patches frequently, the settings have been moved to iOS Settings App->Loop. This is the same location where you find Bluetooth, privacy, and similar settings.
All 3 settings can be enabled or disabled individually
