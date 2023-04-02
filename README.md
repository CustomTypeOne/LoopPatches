***
## LoopPatches

**README last updated on 02-April-2023**

This **sliding-scale** branch of LoopPatches is very experimental. Do NOT use unless you are experienced.

This README file is bare-bones.

The patch is extracted from IsThisPaul/Loop branch dev-with-patches-sliding-scale-paf.

* If you have not used LoopPatches before - do not use
* If you are not using dev and keeping up with zulipchat - do not use
* If you have not followed this topic [Sliding Scale Partial Application Factor](https://loop.zulipchat.com/#narrow/stream/144182-development/topic/Sliding.20Scale.20Partial.20Application.20Factor) - do not use

You use these patches at your own risk and are responsible for ensuring they work as you expect. Adjust settings carefully - there are no guardrails or error checking features.

* If you have previously applied the regular dev or main branch of LoopPatches, you must clean them up first using [OOPS - Clean Up Patches](#oops---clean-up-patches).
* Note - this will wipe out any other customizations you have applied to Loop or LoopKit submodules

The new Sliding Scale feature is added to the bottom of the list under iOS Settings, Loop.

The default values are shown in this graphic:

-<a href="/img/sliding-scale-default.jpg"><img src="/img/sliding-scale-default.jpg?raw=true" alt="nominal terminal display when sliding scale is first added to patches" width="600"></a>

You must enter values suitable for your CGM glucose units (mg/dL or mmol/L). There are no guardrails so be careful.

* If you use mmol/L, do not use a comma as a decimal separator
    * Enter 5.5 not 5,5 (which whould be interpreted as 5.0 mmol/L)

Definition of the settings:

* At a blood glucose reading at or below `Bottom of Scale BG`, Loop will dose `Starting Application Factor` of the recommended bolus
* At a blood glucose reading above `Bottom of Scale BG` and up to `Top of Scale BG`, Loop will linearly increase the application to 100% but limited by `Max Application Factor`
* If `Max Application Factor` exceeds 100%, then
    * At a blood glucose reading above `Top of Scale BG`, Loop will continue to linearly increase the application factor up to that maximum value
* When `Max Application Factor` is less than 100%, the linear ramp matches that of hitting 100% at `Top of Scale BG`, but is limited to `Max Application Factor`

But what happens if I get more than my recommended dose?

* Any additional dose above 100% will be accounted for on the next loop and removed from the recommended dose, effectively making that large dose a "super bolus"

### Copy and Paste Commands

NOTE: These are meant to be applied in the LoopWorkspace folder and are using the new format developed for GitHub patching. (Same commands work in build_loop.yml or for Mac-Xcode build.)

Copy the lines below by hovering the mouse near the top right side of the text and clicking the copy icon. When you click the icon, a message that says “Copied” will appear on your screen.

```
curl https://raw.githubusercontent.com/CustomTypeOne/LoopPatches/sliding-scale/LoopPatch.txt | git apply -v --directory=Loop
curl https://raw.githubusercontent.com/CustomTypeOne/LoopPatches/sliding-scale/LoopkitPatch.txt | git apply -v --directory=LoopKit

```


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

If you hit paste twice (or perhaps you tried to apply the main branch of LoopPatches to a development branch of Loop).

Copy the lines below by hovering the mouse near the top right side of the text and clicking the copy icon. When you click the icon, a message that says “Copied” will appear on your screen. When you paste these lines into your **LoopWorkspace Terminal Window**, you are removing the patches and restoring your download to the original state (for Loop and LoopKit).

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
