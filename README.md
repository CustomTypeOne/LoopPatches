***
## LoopPatches cannot be applied to Dev code that is older than 14 July 2022.

Tested with Loop Dev version: 26 Sep 2022, commit ca8a374

# Custom Type One: LoopPatches

Loop Patches offer several adjustments to Loop. Each is found under the iOS Loop settings (after patch installation) in this order with these names:

1. Partial Bolus Application Factor
    * Adjust the percentage of recommended insulin that Loop delivers for each Automatic Bolus when that Dosing Strategy is selected
    * **NOT RECOMMENDED, added for convenience of people returning from FreeAPS**
1. Automatic Strategy Switching
    * Switch Dosing Strategy from Temp Basal to Automatic Bolus at a glucose level you choose
1. Negative IOB Factor
    * Restrict the insulin Loop doses for negative IOB to prevent rebound lows
    * Unlike the other patches, this one is enabled by default using a 50% setting for negative IOB
    * To Disable this factor, modify the picker wheel to 100%
1. Basal Lock
    * Prevent Loop from reducing or suspending insulin when you go over a set glucose value to assist with stubborn highs
    * **Use with care; meant for high glucose >250 mg/dL, 14 mmol/L**
        * **When used improperly, this can cause lows**

Use caution with these features and adjust conservatively and slowly for safety.

**WARNING: These patches are provided open source, are highly experimental and not approved for therapy by any governmental organization.**

* Do not use LoopPatches if you are not an experienced Looper who has previously built Loop and understands how to customize the code.
* It is your responsibility to review the code and understand the changes made.
* You take full responsibility for building and running Loop Dev with the patches and do so at your own risk.
* Please consult with your health care professional regarding your diabetes management.

## Feature Details

**DO NOT attempt to use these patches until you have read and understood the documentation for each patch. Open the Loop Patches link in a new tab or window and read the documentation.**

* Hold down the control key and click (or right click) on the [Loop Patches](https://www.craft.do/s/pakv8NO1oYpDgh)
* Select open in a new window or new tab of your browser

Each patch is enabled or modified using the phone iOS settings.

Tap on the phone settings icon

* Scroll down until you find the Loop app
* Tap on Loop
* The graphic below shows phone (Loop) settings: Left before the Patch, Right after the Patch

<a href="/img/looppatches-loop-settings.svg"><img src="/img/looppatches-loop-settings.svg?raw=true" alt="Image showing the iOS settings screen before and after applying Settings.bundle" width="500"></a>

Note: If you observe the settings screen as shown on the right side of the graphic above, this means you dragged the Settings Bundle into the correct location as described in the installation instructions. You must also perform the `git apply` action described below, where you copy and paste text into the appropriate terminal location, with no errors reported for the patches to actually be "connected" to these iOS settings.

All settings can be enabled or disabled individually. Be certain that you enter appropriate values before enabling each. I am unable to test MMOL but will report here if anyone reports it works or does not work with mmol.

## To Apply

Warning: Only apply LoopPatches to fresh a download of Loop-dev. If you have other customizations you wish to apply, those should be added after applying LoopPatches.

For each link below - remember to control-click (or right click) so you can return to these instructions easily.

* Use the [Loop-dev](https://loopkit.github.io/loopdocs/build/step13/) instructions in LoopDocs to download Loop-dev
* When building, choose to build to a simulator (not your phone) to insure build succeeds before applying LoopPatches
* Keep Xcode open - you will use it again after applying LoopPatches

Then follow these directions carefully.

1. Open Finder on your computer and examine the Downloads folder
    * If a folder called `LoopPatches-main` exists, delete it
        * Hold down the Control Key and click on the folder name and select `Move to Trash`
    * If a file called `LoopPatches-main.zip` exists, delete it using the same method
    * Examine Finder to make sure there are no LoopPatches-main folders or zip files in Downloads
1. Use the green button at the top of this page that says `Code`
    * Click on `Code`
    * Select Download ZIP
1. Return to Finder and examine the Downloads folder
    * Double click on `LoopPatches-main.zip`
    * This creates the `LoopPatches-main` folder, double click on it to open the folder
    * Inside the folder is a file called `Settings.bundle.zip`, double click on that file
    * You will need to return to this `LoopPatches-main` folder later - so remember how to get here

It is now time to open a terminal window in your new Loop-dev download.

Please follow these instructions from LoopDocs: [Open a Terminal in LoopWorkspace Folder](https://loopkit.github.io/loopdocs/build/step13/#open-a-terminal-in-loopworkspace-folder).

Now that you have a terminal window opened in the LoopWorkspace folder, you can copy and paste the following sets of commands into that terminal window. If you see the word `error` at the beginning of a line, stop and review the instructions. **DO NOT CONTINUE after an error is observed.** (A whitespace error is a warning and can be ignored.)

Copy the lines below that starts with `cd Loop` by hovering the mouse near the top right side of the text and clicking the copy icon. When you click the icon, a message that says “Copied” will appear on your screen.

```
cd Loop
git apply ~/Downloads/LoopPatches-main/LoopPatch.txt
cd ..
cd LoopKit
git apply ~/Downloads/LoopPatches-main/LoopKitPatch.txt
cd ..

```

After the text is copied, click in the terminal window and paste the text. (Ways to paste: CMD-V; or CNTL-click and select from menu or Edit-Paste at top of Mac screen.) Once the line is pasted, the beginning lines will execute but the last one waits for you to finish the process by hitting return one more time.

Notice you will see messages talking about trailing `whitespace errors`, but those lines begin with the word `warning`. Those can all be ignored. Make sure you do not see the word `error` at the beginning of a line with the phrase `patch does not apply`.

Return to the `LoopPatches-main` folder in Finder and locate the Settings.bundle folder.

Return to the Xcode that was used to build Loop-dev to a simulator.

* Click on the folder icon in the left pane of Xcode
* Click on the icon to the left of the Loop folder to open it (you should see Scripts, Common, etc)

You need to be able to see both Finder and Xcode for this next step.

* From Finder `LoopPatches-main` folder, drag the Settings.bundle into Xcode (using these directions)
    * Click on Settings.bundle and hold the mouse button down
    * Drag into the Xcode left pane (as shown in the graphic below)
    * Move the mouse (while holding the button) until the blue line (see graphic below) is immediately under Loop and above Scripts
    * Let go of the mouse button
* A new window will appear in Xcode as shown in the graphic below
    * Add a check mark (if not there) by Copy Items if needed
    * Add a check mark, in Add to Targets, to left of Loop
    * The other add to targets boxes (from older graphic) can be left unchecked

<a href="/img/settingsbundle.png"><img src="/img/settingsbundle.png?raw=true" alt="Image showing the Xcode window as user drags Settings.bundle into place" width="1209"></a>

* If you use mmol - follow the directions for MMOL users
* Optional, check the modified files inside Xcode (instructions below)

Ready to build with the patches:

1. Click on Square Block to the left of the Build arrow in Xcode if it exists
    * The Square Block just means Xcode is connected to the Simulator and the simulator is running
    * Clicking on the square block, stops the simulator
1. Click on the Build Arrow to build to the simulator again
1. Confirm the build succeeded without errors
1. (Optional) If you want other customizations, add them now and test build to the simulator again
1. Click on Square Block to stop the simulator
1. Plug in your phone, select your phone and build to your phone

### MMOL Users

You need to make a modification to select "numbers and punctuation" for the 2 items shown below before you build.

<a href="/img/mmolChange.png"><img src="/img/mmolChange.png?raw=true" alt="Image showing the Xcode window as user modifies for using mmol/L units" width="1209"></a>

## To Confirm the Patches were Applied

In the Xcode window, left pane, you will notice the letter M appears by modified files.

These files should be modified. If they are not, you did not apply the patches successfully. There will be indications in Xcode that the files have been modified at the lines indicated. Note the line numbers are all after the patch has been applied.

1. Under the Loop folder icon (left side of Xcode pane)
    * Loop/Managers/DoseMath.swift
        * line 9, near 392, near 499
    * Loop/Managers/LoopDataManager.swift
        * near line 1596, near 1639
1. Under the LoopKit folder icon (left side of Xcode pane)
    * LoopKit/InsulinKit/InsulinMath.swift
        * near line 40 and 85
1. If you are comfortable with git command line tools and happen to type git status in the Loop folder, you will notice that `Loop.xcodeproj/project.pbxproj` has been modified. All the changes have to do with incorporating the Settings.bundle.
