***
## LoopPatches

LoopPatches offer several adjustments to Loop. Each is disabled by default the first time you build after adding the patches, but your selected values are maintained for subsequent builds for a given phone. Only enable the feature(s) you want to use and test. Leave the rest disabled.

**README last updated on 21-May-2023**

You are in the correct place if you want to apply LoopPatches to the released Loop 3.2.2 version.

This page has instructions for applying LoopPatches.

Refer to the [LoopPatches](https://www.loopandlearn.org/custom-type-one-loop-patches/) documentation page on the Loop and Learn website for usage instructions. **Read the documentation before applying and using the patches.**

The LoopPatches code was lightly tested, but you use this at your own risk.

There are no guardrails, so be extremely careful when you enter thresholds in iOS settings.

### LoopPatches Branches

The LoopPatches found in the **main** branch of LoopPatches can be applied to the released Loop code from the **main** branch of LoopKit/LoopWorkspace.

The LoopPatches found in the **dev** branch of LoopPatches can be applied to the **dev** branch of LoopKit/LoopWorkspace. The dev branch is often identical to the main branch. When there is a change required, it may take a few days for the dev branch to be updated. For each copy/paste block of text below - you will need to replace the word `main` with the word `dev` to use the dev branch for LoopPatches.

## **Table of Contents**

* [Apply LoopPatches](#apply-looppatches)
    * [Summary of Steps](#summary-of-steps)
    * [Fresh Download of Loop](#fresh-download-of-loop)
        * [Open New Terminal at LoopWorkspace](#open-new-terminal-at-loopworkspace)
        * [LoopWorkspace Quick Access](#loopworkspace-quick-access)
    * [Copy and Paste Commands](#copy-and-paste-commands)
    * [Build with LoopPatches](#build-with-looppatches)
    * [Congratulations](#congratulations)
    * [OOPS - Clean Up Patches](#oops---clean-up-patches)
* [Confirm Patches Work](#confirm-patches-work)
    * [Example for Switcher Patch](#example-for-switcher-patch)
    * [Example for Basal Lock](#example-for-basal-lock)
* [(Optional) Examine Code Before Building](#optional-examine-code-before-building)

## Apply LoopPatches

### Summary of Steps

1. Obtain a fresh download of Loop
    * Build to a simulator; ensure it builds without error
1. Open a NEW terminal in new LoopWorkspace
1. Follow directions to install patches
    * STOP IMMEDIATELY if you get an error
1. Build Loop with LoopPatches to your phone
1. Choose the feature(s) to enable and test each one

### Fresh Download of Loop

For each link below - remember to control-click (or right click) to open link in a new tab or window so you can return to these instructions easily.

* Use the [Build Select Script](https://loopkit.github.io/loopdocs/build/step14/#download-loop) instructions in LoopDocs to download Loop
* When building, choose to build to a simulator (not your phone) to ensure build succeeds before applying LoopPatches
* If you chose [Loop with Patches](https://www.loopandlearn.org/main-lnl-patches/) when your ran the Build Select Script, you already have LoopPatches along with a few other customizations, so stop now and read about how to use the patches

If you closed your terminal after the download - you need to follow the [Open New Terminal at LoopWorkspace](#open-new-terminal-at-loopworkspace) steps before applying patches. 

Otherwise, skip ahead to the [LoopWorkspace Quick Access](#loopworkspace-quick-access) instructions.

#### Open New Terminal at LoopWorkspace

If you are returning to add LoopPatches and have closed your terminal from the download, you should follow these steps to open a terminal window associated with the LoopWorkspace folder of your new Loop 3 download. This will be called the **LoopWorkspace Terminal Window** to distinguish it from any other terminal windows you might have open.

For full directions, with graphics, refer to LoopDocs at this link: [Open a Terminal in LoopWorkspace Folder](https://loopkit.github.io/loopdocs/build/code_customization/#open-a-terminal-in-loopworkspace-folder).

The short bullet list is provided here (if you don't need the instructions linked above)

* Use Finder to navigate to Downloads / BuildLoop
* Find the version of Loop 3 you just downloaded
* Open the folder to view LoopWorkspace
* Hold down the CTRL key and click (or right-click) LoopWorkspace
* A menu appears - select New Terminal at Folder (near the bottom of the list)

**As soon as that window opens, type pwd in the terminal and hit return.  The command pwd means to print the working directory.**

The response must end in LoopWorkspace and the date-time should match the fresh download. For example:

`/Users/marion/Downloads/BuildLoop/Loop-230114-1645/LoopWorkspace`

If the response is wrong, quit out of that terminal and try again.

Now you can skip ahead to [Copy and Paste Commands](#copy-and-paste-commands).

#### LoopWorkspace Quick Access

If the terminal from your download is still open, you can scroll up to where the download started. You'll see a section similar to this:


| Terminal Display: |
|---|
|
 -- Downloading Loop to your Downloads folder --;<br><br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;/Users/marion/Downloads/BuildLoop/Loop-230521-1655 |

Highlight the path and put a `cd` in front of it and a `/LoopWorkspace` at the end and paste it into the terminal. It will look like this, but will have your path name.

```
cd /Users/marion/Downloads/BuildLoop/Loop-230521-1655/LoopWorkspace
```

Do **not** use the cd line above - make your own. Enter that into your terminal.

### Copy and Paste Commands

Now that you have a new terminal window opened in the LoopWorkspace folder, you can copy and paste the following sets of commands into that terminal window. If you see the word `error` at the beginning of a line, stop and review the instructions. **DO NOT CONTINUE after an error is observed.**

Copy the lines below by hovering the mouse near the top right side of the text and clicking the copy icon. When you click the icon, a message that says “Copied” will appear on your screen.

```
curl https://raw.githubusercontent.com/CustomTypeOne/LoopPatches/main/LoopPatch.txt | git apply --directory="Loop"
curl https://raw.githubusercontent.com/CustomTypeOne/LoopPatches/main/LoopkitPatch.txt | git apply --directory="LoopKit"

```

After the text is copied, click in the **LoopWorkspace Terminal Window** and paste the text. (Ways to paste: CMD-V; or CNTL-click and select from menu or Edit-Paste at top of Mac screen.) Once the line is pasted, hit return.  On some computers the return is not necessary but does not hurt anything. On some computers the return is required to execute the commands.

After you paste and hit return. The patches will be automatically applied and your screen should be similar to the graphic below.

<a href="/img/looppatches-with-curl.png"><img src="/img/looppatches-with-curl.png?raw=true" alt="nominal terminal display when applying LoopPatches" width="600"></a>

There should be no error messages in response (unless there is an error). Make sure you do not see `error: patch failed` at the beginning of a line with various details afterwords. Be sure to only paste one time to a fresh download. A second paste will show errors. See [OOPS - Clean Up Patches](#oops---clean-up-patches)

#### Build from LoopWorkspace Terminal Window

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

### OOPS - Clean Up Patches

If you hit paste twice (or perhaps you tried to apply the wrong branch of LoopPatches).

Copy the lines below by hovering the mouse near the top right side of the text and clicking the copy icon. When you click the icon, a message that says “Copied” will appear on your screen. When you paste these lines into your **LoopWorkspace Terminal Window**, you are removing LoopPatches from your clone for Loop and LoopKit.

```
curl https://raw.githubusercontent.com/CustomTypeOne/LoopPatches/main/LoopPatch.txt | git apply --directory="Loop" --reverse
curl https://raw.githubusercontent.com/CustomTypeOne/LoopPatches/main/LoopkitPatch.txt | git apply --directory="LoopKit" --reverse

```

If that does not work - if you get errors, then you can try the next approach. This will remove all customizations (any you made as well as the LoopPatches changes) from your clone for both Loop and LoopKit and you will have to apply them again.

```
cd Loop;git stash;rm -rf Settings.bundle;cd ..
cd LoopKit;git stash;cd ..

```

You should now be able to return to [Copy and Paste Commands](#copy-and-paste-commands) to try again.

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
