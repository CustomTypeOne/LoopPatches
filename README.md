***
## Patch will not apply to dev code as of July 14th. I'm currently testing the fix. If you want to test this also, open Looppatch.txt and find/replace "settings.dosingStrategy" with "settings.automaticDosingStrategy".
***

# LoopPatches

These patches are provided open source and it is your responsibility to review the code. These patches are highly experimental and not approved for therapy. It is your responsibility to review the code and understand the changes using this will make.

***
## Patches have only been tested using Loop Dev.
***

## To Apply

1. Only apply to fresh a download of Loop. If you attempted to apply and it errored (only whitespace errors are acceptable), delete the download and start over.
2. Use the green button to download the files and unzip the downloaded file
3. Inside the unzipped folder, you will also need to unzip the settings.bundle file
4. Copy LoopPatch.txt into /LoopWorkspace/Loop/, open terminal to this folder, and run: git apply LoopPatch.txt
5. Copy LoopkitPatch.txt into /LoopWorkspace/Loopkit/, open terminal to this folder, and run: git apply LoopkitPatch.txt
6. Open xcode and drag the settings.bundle file just inside the Loop project folder and select the first 5 boxes when asked for targets

![settingsbundle](https://user-images.githubusercontent.com/38429455/158242367-de24fa1b-9f4e-4082-9d9b-db6ad109a563.png)

# PAF-Switcher-NegativeIOB Patch

This patch modifies Loop for 3 new features. [Read more information here](https://www.notion.so/customtypeone/Loop-Patches-32a53bd5b48f4c2ea498ac6ab9efab06).
- Alternate Partial Bolus Application Factor (PAF) allows you to adjust the 40% default used when determining what percentage of the calculated AB dose that Loop delivers.
- Automatic Strategy Switcher allows you to configure a threshold where Loop automatically switches between TB (<= threshold) and AB (> threshold). You must set Loop to AB mode and enable this setting for it to function. If you are in TB only, it will not auto switch you to AB and it also will not switch the setting within Loop.
- Negative IOB Factor is a percentage you can use to adjust the effect of negative IOB. During stubborn lows, Loop will frequently try to dose too much of the negative IOB as a recovery. This restricts Loop to only use this percentage of the negative IOB in a dose. Credit goes to Kenneth Stack for this. I just integrated his brilliant solution.

To apply the patch, you MUST apply both files. 
1. From the main repository code page, download a zip of the code using the green code button and unzip the files. The "Loop-" file should be copied to LoopWorkspace/Loop/ and "LoopKit-" should be copied to LoopWorkspace/LoopKit/
2. Open a terminal to the above folders and run this command for each filename, replacing patchname.txt with the actual patch filename: git apply patchname.txt
3. The only acceptable erros to be shown after running the commands are "whitespace" errors

To keep from needing to modify these patches frequently, the settings have been moved to iOS Settings App->Loop. This is the same location where you find Bluetooth, privacy, and similar settings.
All 3 settings can be enabled or disabled individually. Be certain that you enter appropriate values before enabling each. I am unable to test MMOL for the switcher patch, but will report back here if someone confirms it works in MMOL.

# To Test the switcher functionality

1. Leave your phone plugged in with xcode running after building
2. Set Loop to Automatic Bolus for the dosing strategy
3. Set your BG threshold in iOS Settings/Loop
4. Enable the switcher toggle in iOS Settings/Loop
5. Open /Loop/Managers/LoopDataManager.swift in xcode and set breakpoints on lines 1614 and 1616
6. At the next Loop cycle, it will pause running at one of these breakpoints. Line 1614 is if BG is over your threshold, Line 1616 is if BG is under your threshold.


![IMG_0191](https://user-images.githubusercontent.com/38429455/161996907-9e81707a-cea7-421f-91d4-dc4c2e571a7e.jpeg)
