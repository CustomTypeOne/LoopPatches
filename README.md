# LoopPatches

These patches are provided open source and it is your responsibility to review the code. These patches are highly experimental and not approved for therapy. It is your responsibility to review the code and understand the changes using this will make.

# PAF-Switcher-NegativeIOB Patch

This patch modifies Loop for 3 new features. [Read more information here](https://www.notion.so/customtypeone/Loop-Patches-32a53bd5b48f4c2ea498ac6ab9efab06).
- Alternate Partial Bolus Application Factor (PAF) allows you to adjust the 40% default used when determining what percentage of the calculated AB dose that Loop delivers.
- Automatic Strategy Switcher allows you to configure a threshold where Loop automatically switches between TB (<= threshold) and AB (> threshold). You must set Loop to AB mode and enable this setting for it to function. If you are in TB only, it will not auto switch you to AB.
- Negative IOB Factor is a percentage you can use to adjust the effect of negative IOB. During stubborn lows, Loop will frequently try to dose too much of the negative IOB as a recovery. This restricts Loop to only use this percentage of the negative IOB in a dose. Credit goes to Kenneth Stack for this. I just integrated his brilliant solution.

To apply the patch, you MUST apply both files. 
1. From the main repository code page, download a zip of the code using the green code button and unzip the files. The "Loop-" file should be copied to LoopWorkspace/Loop/ and "LoopKit-" should be copied to LoopWorkspace/LoopKit/
2. Open a terminal to the above folders and run this command for each filename, replacing patchname.txt with the actual patch filename: git apply patchname.txt
3. The only acceptable erros to be shown after running the commands are "whitespace" errors

To keep from needing to modify these patches frequently, the settings have been moved to iOS Settings App->Loop. This is the same location where you find Bluetooth, privacy, and similar settings.
All 3 settings can be enabled or disabled individually. Be certain that you enter appropriate values before enabling each. I am unable to test MMOL for the switcher patch, but will report back here if someone confirms it works in MMOL.
