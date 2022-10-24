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
    * This feature is disabled by selecting a factor of 100% (default setting)
    * Note - this modifies what Loop records as IOB whenever IOB is negative
1. Basal Lock
    * Prevent Loop from reducing or suspending insulin when you go over a set glucose value to assist with stubborn highs
    * **Use with care; meant for high glucose >250 mg/dL, 14 mmol/L**
        * **When used improperly, this can cause lows**

Use caution with these features and adjust conservatively and slowly for safety.

**WARNING: These patches are open source, experimental and not approved for therapy by any governmental organization.**

* Do not use LoopPatches if you are not an experienced Looper who has previously built Loop and understands how to customize the code.
* It is your responsibility to review the code and understand the changes made.
* You take full responsibility for building and running Loop Dev with the patches and do so at your own risk.
* Please consult with your health care professional regarding your diabetes management.

## Feature Details

**DO NOT attempt to use these patches until you have read and understood the documentation for each patch. Open the Loop Patches Documentation link (below) in a new tab or window and read the documentation.**

* Hold down the control key and click (or right click) on the link for [Loop Patches Documentation](https://www.craft.do/s/pakv8NO1oYpDgh)
* Select open in a new window or new tab of your browser and read about each patch
* Then return to this page before continuing (because the documentation page does not have the patch code)

## Feature Selection After Installation

After installation, each patch will be enabled or modified using the phone iOS settings.

Tap on the phone settings icon

* Scroll down until you find the Loop app
* Tap on Loop
* The graphic below shows phone (Loop) settings: Left before the Patch, Right after the Patch

<a href="/img/looppatches-loop-settings.svg"><img src="/img/looppatches-loop-settings.svg?raw=true" alt="Image showing the iOS settings screen before and after applying Settings.bundle" width="500"></a>

Note: If you observe the settings screen as shown on the right side of the graphic above, this means you dragged the Settings Bundle into the correct location as described in the installation instructions. You must also perform the `git apply` action described below, where you copy and paste text into the appropriate terminal location, with no errors reported for the patches to actually be "connected" to these iOS settings.

All settings can be enabled or disabled individually. Be certain that you enter appropriate values before enabling each. Please file an issue if there are problems with mmol/L units.

For the Automatic Switching Strategy or Basal Lock features:

* Tap (or double-tap) on the "value" row to bring up a keyboard and enter a value
    * There is no "done" button on the keyboard for these entries
    * Click on the <Settings button at upper left to dismiss the keyboard
    * Tap on Loop again to view the value
* Make sure that value is reasonable **before** sliding the switch to Enabled
* When modifying a value, be sure to disable the switch, modify and then enable

## Apply the Patches

### Fresh Download of Loop-dev

Warning: Only apply LoopPatches to fresh a download of Loop-dev. If you have other customizations you wish to apply, those should be added after applying LoopPatches.

For each link below - remember to control-click (or right click) so you can return to these instructions easily.

* Use the [Loop-dev](https://loopkit.github.io/loopdocs/build/step13/) instructions in LoopDocs to download Loop-dev
* When building, choose to build to a simulator (not your phone) to insure build succeeds before applying LoopPatches
* Keep Xcode open - you will use it again after applying LoopPatches

### Download LoopPatches

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

### Open New Terminal at LoopWorkspace

It is now time to open a terminal window associated with the LoopWorkspace folder of your new Loop-dev download.

For full directions, with graphics refer to LoopDocs at this link: [Open a Terminal in LoopWorkspace Folder](https://loopkit.github.io/loopdocs/build/step13/#open-a-terminal-in-loopworkspace-folder).

* Open Finder
* Navigate to Downloads / BuildLoop
* Find the version of Loop-dev you just downloaded
* Open the folder to view LoopWorkspace
* Hold down the CTRL key and click (or right-click) LoopWorkspace
* A menu appears - select New Terminal at Folder (near the bottom of the list)

### Copy and Paste Commands

Now that you have a new terminal window opened in the LoopWorkspace folder, you can copy and paste the following sets of commands into that terminal window. If you see the word `error` at the beginning of a line, stop and review the instructions. **DO NOT CONTINUE after an error is observed.** (A whitespace error is a warning and can be ignored.)

Copy the lines below by hovering the mouse near the top right side of the text and clicking the copy icon. When you click the icon, a message that says “Copied” will appear on your screen.

```
cd Loop
git apply ~/Downloads/LoopPatches-main/LoopPatch.txt
cd ..
cd LoopKit
git apply ~/Downloads/LoopPatches-main/LoopKitPatch.txt
cd ..
cp -pr ~/Downloads/LoopPatches-main/Settings.bundle Loop

```

After the text is copied, click in the terminal window and paste the text. (Ways to paste: CMD-V; or CNTL-click and select from menu or Edit-Paste at top of Mac screen.) Once the line is pasted, the lines will execute.

Notice you will see the text (in the block above) repeated in the terminal display. There should be no other messages. Make sure you do not see the word `error` at the beginning of a line with the phrase `patch does not apply`.

If you see this message:
    `cp: /Users/<your name>/Downloads/LoopPatches-main/Settings.bundle: No such file or directory`

* That means you did not double click the `Settings.bundle.zip` file.  Do it now and then copy and paste just this one line.

```
cp -pr ~/Downloads/LoopPatches-main/Settings.bundle Loop

```

### Configure Xcode with Settings Bundle

Return to the LoopWorkspace folder in Finder that you used to open the terminal window.

* Double click on LoopWorkspace to open the LoopWorkspace folder
* Double click on Loop to open the Loop folder
* Locate the Settings.bundle file - you will use that next

Return to Xcode, which was used to build the fresh Loop-dev download to a simulator.

* Click on the folder icon in the left pane of Xcode
* Click on the icon to the left of the Loop folder to open it (you should see Scripts, Common, etc)

You need to arrange your screen to see both the Finder folder and Xcode for this next step.

* From Finder, drag the Settings.bundle into Xcode (using these directions)
    * Click on Settings.bundle and hold the mouse button down
    * Drag into the Xcode left pane (as shown in the graphic below)
    * Move the mouse (while holding down the button) until the blue line (see graphic below) is immediately under Loop and above Scripts
    * Let go of the mouse button
* A new window will appear in Xcode as shown in the graphic below
    * Add a check mark (if not there) by Copy Items if needed
    * Add a check mark, in Add to Targets, to left of Loop

<a href="/img/looppatches-settings-bundle.svg"><img src="/img/looppatches-settings-bundle.svg?raw=true" alt="Image showing the Xcode window as user drags Settings.bundle into place" width="750"></a>

* If you use mmol - follow the directions below for MMOL users before building with LoopPatches
* Optional, check the modified files inside Xcode (instructions below)

### Ready to build with LoopPatches:

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
        * line 12, near 395, near 503
    * Loop/Managers/LoopDataManager.swift
        * near line 1599, near 1641
1. Under the LoopKit folder icon (left side of Xcode pane)
    * LoopKit/InsulinKit/InsulinMath.swift
        * near line 43 and 93
1. If you are comfortable with git command line tools and happen to type git status in the Loop folder, you will notice that `Loop.xcodeproj/project.pbxproj` has been modified. All the changes in that file have to do with incorporating the Settings.bundle.
