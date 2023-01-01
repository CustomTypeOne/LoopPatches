***
## LoopPatches main branch updated 15-Dec-2022

The LoopPatches code in this branch have been lightly tested, but you use them at your own risk.

* Tested with Loop Dev version: 15 Dec 2022, commit 290211f
* Tested using mg/dL
* Verified LoopPatches can be applied with commit 3770f56, 23 Dec 2022
* Verified LoopPatches can be applied with commit 84afcfb, 01 Jan 2023

### Loop-dev vs LoopPatches Branch Status

The LoopPatches found in the **main** branch of LoopPatches can be applied to the Loop-dev version built using the **BuildLoopFixedDev** script.

* Before an update is added to [**BuildLoopFixedDev**](https://loopkit.github.io/loopdocs/build/step13/#download-loop-dev) script
    * LoopPatches main branch is tested to make sure patches can be applied
    * As long as the patches apply, no change is required to LoopPatches main branch
* On 27-Nov-2022, the patches required modification
    * The older version of LoopPatches is saved in the branch named: dev-f245588
    * If LoopWorkspace commit is f245588 or older, that branch can be used
    * In the interim, LoopPatches branch dev was modified to work with newer commits until both the build script and LoopPatches were ready for update
* As of 15-Dec-2022, the main branch of LoopPatches and **BuildLoopFixedDev** script were updated at the same time


## **Table of Contents**

* [Custom Type One: LoopPatches Overview](#custom-type-one-looppatches)
* [Feature Details](#feature-details)
* [Feature Selection](#feature-selection)
    * [Use iOS Settings](#use-ios-settings)
    * [All Features](#all-features)
    * [Automatic Switching Strategy or Basal Lock](#automatic-switching-strategy-or-basal-lock)
    * [mmol/L Users](#mmolL-users)
* [Apply LoopPatches](#apply-looppatches)
    * [Summary of Steps](#summary-of-steps)
    * [Fresh Download of Loop](#fresh-download-of-loop)
    * [Download LoopPatches](#download-looppatches)
    * [Open New Terminal at LoopWorkspace](#open-new-terminal-at-loopworkspace)
    * [Copy and Paste Commands](#copy-and-paste-commands)
    * [Build with LoopPatches](#build-with-looppatches)
    * [Congratulations](#congratulations)
* [Confirm Patches Work](#confirm-patches-work)
    * [Example for Switcher Patch](#example-for-switcher-patch)
    * [Example for Basal Lock](#example-for-basal-lock)
* [(Optional) Examine Code Before Building](#optional-examine-code-before-building)

# Custom Type One: LoopPatches

LoopPatches offer several adjustments to Loop. Each is disabled by default the first time you build after adding the patches, but your selected values are maintained for subsequent builds for a given phone. Only enable the feature(s) you want to use and test. Leave the rest disabled.

Note: for **prior users of LoopPatches**: _The order of features has been modified and new features are available. There is no longer a drag and drop action required to add Settings to Xcode._

* Features near the bottom of the list are either not recommended or are new and require more care
* The order of patches displayed under Settings does not affect the values saved from previous builds
    * Those values are remembered (by name) for a given phone.

The configuration for each patch is found under the iOS Loop settings (after patch installation) in this order with these names:

1. Add Now Marker, Main Charts
    * Display Feature
    * A vertical line is presented on each of the 4 main charts on the main Loop screen
    * This can be enabled or disabled (default)
1. Automatic Strategy Switching
    * Switch Dosing Strategy from Temp Basal to Automatic Bolus at a glucose level you choose
1. Negative IOB Factor
    * Restrict the insulin Loop doses for negative IOB to prevent rebound lows
    * This feature is disabled by selecting a factor of 100% (default setting is 1.0, same as 100%)
    * Note - this modifies what Loop records as IOB whenever IOB is negative
1. Partial Bolus Application Factor
    * Adjust the percentage of recommended insulin that Loop delivers for each Automatic Bolus when that Dosing Strategy is selected
    * **NOT RECOMMENDED, added for convenience of people returning from FreeAPS**
1. Basal Lock
    * Prevent Loop from reducing or suspending insulin when you go over a set glucose value to assist with stubborn highs
    * Basal is "locked" to be no lower than the scheduled rate (overrides are ignored)
    * **Use with care; meant for high glucose >250 mg/dL (13.9 mmol/L)**
        * **When used improperly, this can cause lows**

Use caution with these features and adjust conservatively and slowly for safety.

**WARNING: These patches are open source, experimental and not approved for therapy by any governmental organization.**

* Do not use LoopPatches if you are not an experienced Looper who has previously built Loop and understands how to customize the code.
* It is your responsibility to review the code and understand the changes made.
* You take full responsibility for building and running Loop Dev with the patches and do so at your own risk.
* Please consult with your health care professional regarding your diabetes management.

## Feature Details

**DO NOT attempt to use these patches until you have read and understood the documentation for each patch. Open the Loop Patches Documentation link (below) in a new tab or window and read the documentation.**

* Hold down the control key and click (or right click) on the link for Loop Patches Documentation : https://www.craft.do/s/pakv8NO1oYpDgh
* Select open in a new window or new tab of your browser and read about each patch provided by Jon Fawcett
* New additions to the LoopPatches - provided by Marion Barker
    * Add Now Marker, Main Charts: No documentation required
* Then return to this page before continuing (the documentation page does not have the patch code)

## Feature Selection

### Use iOS Settings

After installation, each patch will be enabled or modified using the phone iOS settings.

Tap on the phone settings icon

* Scroll down until you find the Loop app
* Tap on Loop
* The graphic below shows phone (Loop) settings: Left before the Patch, Right after the Patch

<a href="/img/looppatches-loop-settings.svg"><img src="/img/looppatches-loop-settings.svg?raw=true" alt="Image showing the iOS settings screen before and after applying Settings.bundle" width="500"></a>

All settings can be enabled or disabled individually. Be certain that you enter appropriate values before enabling each. Please file an issue if you experience problems or have a question.

After each fresh build, check all the values and check behavior for any enabled patches.

### All Features:

* To make sure your modification of a setting is updated in Loop immediately, quit the Loop app (swipe up) and then restart
    * If you do not do this, then within one Loop cycle, the values should be updated anyway
    * Do not guess, make sure the feature you just changed is behaving the way you want

### Automatic Switching Strategy or Basal Lock:

* When modifying a threshold value: disable the feature, modify threshold and then enable
* Tap on the "Threshold" row to bring up a keyboard and enter or edit a value, return when done
* Make sure that value is reasonable **before** sliding the switch to Enabled

### mmol/L Users

No patch changes are required for mmol/L users. Several users confirmed threshold values are entered in mmol/L, but please check carefully on your device.

## Apply LoopPatches

### Summary of Steps

1. Obtain a fresh download of Loop
    * Build to a simulator; ensure it builds without error
1. Delete any prior copies of LoopPatches from Downloads folder
1. Download fresh zip of LoopPatches
    * Find in Downloads, unzip using directions
1. Open a NEW terminal in new LoopWorkspace
1. Follow directions to install patches
    * STOP IMMEDIATELY if you get an error
1. Build Loop with LoopPatches to your phone
1. Choose the feature(s) to enable and test each one

### Fresh Download of Loop

Warning: Only apply LoopPatches to a fresh download of Loop. Once patches are applied, you cannot apply them again without taking steps that are not included in these instructions. If you have other customizations you wish to apply, those should be added after applying LoopPatches.

For each link below - remember to control-click (or right click) to open link in a new tab or window so you can return to these instructions easily.

* Use the [Loop-dev](https://loopkit.github.io/loopdocs/build/step13/) instructions in LoopDocs to download Loop
* When building, choose to build to a simulator (not your phone) to ensure build succeeds before applying LoopPatches

### Download LoopPatches

Follow these directions carefully to remove any old copies of LoopPatches and then download a fresh copy.

1. Open Finder on your computer and examine the Downloads folder
    * If a folder called `LoopPatches-main` exists, delete it
        * Hold down the Control Key and click on the folder name and select `Move to Trash`
    * If a file called `LoopPatches-main.zip` exists, delete it using the same method
    * Examine Finder to make sure there are no folders or files that begin with LoopPatches in Downloads, there may be others with the number 2 or 3 appended to the name if you downloaded without deleting old copies or unzipped more than one time
1.  Open this [link](https://github.com/CustomTypeOne/LoopPatches) in a separate tab to download the code without loosing your place in these instructions.(You can scroll up and down on this webpage if you prefer.)
    * Click on the green button that says `Code`
    * Select Download ZIP
    * Return to these instructions

#### To unzip the folder:

Option 1:
* Double click on the LoopPatches-main.zip indicator at the bottom of your browser

Option 2:
* Return to Finder and examine the Downloads folder
    * Double click on `LoopPatches-main.zip`
    * You will notice this creates the `LoopPatches-main` folder
        * No further action is required

You can use the same finder window for the next step - you won't need this location again.

### Open New Terminal at LoopWorkspace

It is now time to open a terminal window associated with the LoopWorkspace folder of your new Loop-dev download. This will be called the **LoopWorkspace Terminal Window** to distinguish it from any other terminal windows you might have open.

For full directions, with graphics, refer to LoopDocs at this link: [Open a Terminal in LoopWorkspace Folder](https://loopkit.github.io/loopdocs/build/step13/#open-a-terminal-in-loopworkspace-folder).

The short bullet list is provided here (if you don't need the instructions linked above)

* Use Finder to navigate to Downloads / BuildLoop
* Find the version of Loop-dev you just downloaded
* Open the folder to view LoopWorkspace
* Hold down the CTRL key and click (or right-click) LoopWorkspace
* A menu appears - select New Terminal at Folder (near the bottom of the list)

**As soon as that window opens, type pwd in the terminal and hit return.  The command pwd means to print the working directory.**

The response must end in LoopWorkspace and the date-time should match the fresh download. For example:

`/Users/marion/Downloads/BuildLoop/Loop-dev-221215-0924_290211f/LoopWorkspace`

If the response is wrong, quit out of that terminal and try again.

### Copy and Paste Commands

Now that you have a new terminal window opened in the LoopWorkspace folder, you can copy and paste the following sets of commands into that terminal window. Each patch must be applied to the correct folder, so you will see change directory (`cd`) commands as well as `git apply` commands. If you see the word `error` at the beginning of a line, stop and review the instructions. **DO NOT CONTINUE after an error is observed.** (A whitespace error is a warning and can be ignored.)

Copy the lines below by hovering the mouse near the top right side of the text and clicking the copy icon. When you click the icon, a message that says “Copied” will appear on your screen.

```
cd Loop
git apply ~/Downloads/LoopPatches-main/LoopPatch.txt
cd ..
cd LoopKit
git apply ~/Downloads/LoopPatches-main/LoopkitPatch.txt
cd ..

```

After the text is copied, click in the **LoopWorkspace Terminal Window** and paste the text. (Ways to paste: CMD-V; or CNTL-click and select from menu or Edit-Paste at top of Mac screen.) Once the line is pasted, hit return.  On some computers the return is not necessary but does not hurt anything. On some computers the return is required to execute the commands.

After you paste and hit return. There should be no messages in response (unless there is an error). Make sure you do not see the word `error` at the beginning of a line with the phrase `patch does not apply`.

Copy and paste the next line into the same **LoopWorkspace Terminal Window**. This command (`xed`) will open (or bring to front if already open) Xcode so you can build the code with LoopPatches applied. The `.` just means to open Xcode in the current LoopWorkspace location.

```
xed .

```

* Optional, you can check the modified files inside Xcode using [(Optional) Examine Code Before Building](#optional-examine-code-before-building)

### Build with LoopPatches

1. Click on the Build Arrow to build to the simulator again
    * If a window pops up asking if you want to Replace "Loop"?, click on Replace
    * Confirm the build succeeded without errors
1. (Optional) If you want other customizations, add them now and test build to the simulator again
    * Confirm the build succeeded without errors
1. Plug in your phone, select your phone and build to your phone

### Congratulations!

So long as you did not get any errors, you have now applied the LoopPatches customization to your Loop app. Remember, these are configured under iOS -> Settings -> Loop screen. These features cannot be adjusted inside the Loop app settings screen.

Only enable the feature(s) you want to use and test. Leave the rest disabled.

Every time you build, please check the settings: refer to [Use iOS Settings](#use-ios-settings).

## Confirm Patches Work

For each patch you enable, please confirm it works the way you expect it to work before allowing it to run "unattended". You should check this each time you build. It is too easy to miss a step and have something not operating the way you expect.

If you do not know how to confirm a feature is working, **do not enable** that feature.

There are no guardrails to check Threshold values entered in the patch settings. Please check entries carefully and confirm expected behavior after making a change in patch settings.

### Example for Switcher Patch

1. Confirm that Dosing Strategy is set to Automatic Bolus and Closed Loop is enabled
1. Next time glucose is elevated above target, confirm that an automatic bolus is enacted
1. Type a value under iOS -> Settings -> Loop -> AUTOMATIC STRATEGY SWITCHING -> Switching BG Threshold that is significantly higher than your current glucose
1. Enable the AUTOMATIC STRATEGY SWITCHING feature
1. Next CGM reading should indicate that a high temp basal is enacted, instead of an automatic bolus

Now that you've confirmed the patch is working as desired:

* Disable the feature
* Modify the Switching BG Threshold to the desired value
* Enable the feature

Loop will now automatically switch between Dosing Strategy of Temp Basal (less aggressive) when glucose is below that threshold level to a Dosing Strategy of Automatic Bolus (more aggressive) when glucose is above that threshold level.

Pay attention next time glucose is Below the threshold to ensure that only Temp Basal increases are provided.

### Example for Basal Lock

**Be very careful with this one. If you set the Basal Lock Threshold too low, it will prevent Loop from restricting basal and can cause low glucose.**

**Look for an opportunity when glucose is high, plan on focusing on your phone for 15 to 30 minutes.**

1. Confirm that Closed Loop is enabled and Basal Lock is disabled
1. Next time glucose has been elevated for a while and Loop has given enough insulin that a Temp Basal of 0 U/hr is being provided (raising your correction range can make this happen sooner but be sure to restore it when done testing)
1. Type a value under iOS -> Settings -> Loop -> BASAL LOCK -> Basal Lock Threshold that is less than your current glucose
    * Enable the BASAL LOCK feature
    * Next CGM reading should indicate Loop restored scheduled basal
1. Immediately after that Loop cycle, raise the Basal Lock Threshold to be above your current glucose
    * Next CGM reading should indicate Loop restored lower basal

Now that you've confirmed the patch is working as desired:

* Disable the feature
* Modify the Basal Lock Threshold to the desired value
* Enable the feature (if desired)

Loop will no longer restrict basal when your glucose is higher than this threshold. Pay attention over the next few meals.

* **Start with 250 mg/dL (13.9 mmol/L) or higher**
* **Do not go below 200 mg/dL (11.1 mmol/L) without careful thought and observation**
* **If you notice an increase in lows, raise the threshold or disable the feature**

## (Optional) Examine Code Before Building

In the Xcode window, left pane, you will notice the letter M appears by modified files.

These files should be modified. If they are not, you did not apply the patches successfully. Note the line numbers are all after the patch has been applied. In your Xcode display, when viewing that file, you will see a vertical blue bar left of the code indicating a line has been modified.

1. Under the Loop folder icon (left side of Xcode pane)
    * Loop/Managers/DoseMath.swift
        * line 12, near 395, near 503
    * Loop/Managers/LoopDataManager.swift
        * near line 1599, near 1641
    * LoopUI/Charts
        * These 4 files contain code for the "now" marker
        * COBChart.swift, DoseChart.swift, IOBChart.swift and PredictedGlucoseChart.swift
1. Under the LoopKit folder icon (left side of Xcode pane)
    * LoopKit/InsulinKit/InsulinMath.swift
        * near line 43 and 93
1. If you are comfortable with git command line tools and happen to type git status in the Loop folder, you will notice that `Loop.xcodeproj/project.pbxproj` has been modified and a new Settings.bundle folder with files inside it has been added to the Loop folder.
