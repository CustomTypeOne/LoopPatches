***
## LoopPatches cannot be applied to Dev code that is older than 14 July 2022.

Tested with Loop Dev version: 26 Sep 2022, commit ca8a374

# Custom Type One: LoopPatches

The Patches offer several adjustments to Loop. Each is found under the iOS Loop settings (after patch installation) in this order with these names:

1. Partial Bolus Application Factor
    * Adjust the percentage of recommended insulin that Loop delivers for each Automatic Bolus when that Dosing Strategy is selected **(NOT RECOMMENDED, added for convenience of people returning from FreeAPS)**
1. Automatic Strategy Switching
    * Switch Dosing Strategy from Temp Basal to Automatic Bolus at a glucose level you choose
1. Negative IOB Factor
    * Restrict the insulin Loop doses for negative IOB to prevent rebound lows
1. Basal Lock
    * Prevent Loop from reducing or suspending insulin when you go over a set glucose value to assist with stubborn highs **(use with care and only for high glucose >250 mg/dL, 14 mmol/L)**

Use caution with these features and adjust conservatively and slowly for safety.

**WARNING: These patches are provided open source, are highly experimental and not approved for therapy by any governmental organization.**

* Do not use the LoopPatches if you are not an experienced Looper who has previously built Loop and understand how to customize the code.
* It is your responsibility to review the code and understand the changes made.
* You take full responsibility for building and running Loop Dev with the patches and do so at your own risk.
* Please consult with your health care professional regarding your diabetes management.

## Feature Details

**DO NOT attempt to use these patches until you have read and understood the documentation for each patch. Click on the [Loop Patches](https://www.craft.do/s/pakv8NO1oYpDgh) link for the documentation.**

Hint: Open the link in a new browser window to make it easier to return to these instructions. If you hold down the control key and click (or right click) on a link, you can select open in a new window or new tab of your browser.

Each patch is enabled or modified using the phone iOS settings.

Tap on the phone settings icon

* Scroll down until you find the Loop app
* Tap on Loop
* The graphic below shows phone (Loop) settings: Left before the Patch, Right after the Patch

<a href="/img/loop-settings.svg"><img src="/img/loop-settings.svg?raw=true" alt="Image showing the iOS settings screen before and after applying Settings.bundle" width="500"></a>

Note: If you observe the settings screen as shown on the right side of the graphic above, this means you dragged the Settings Bundle into the correct location as described in the installation instructions. You must also perform the two `git apply` actions described below with no errors reported for the patches to actually be "connected".

All settings can be enabled or disabled individually. Be certain that you enter appropriate values before enabling each. I am unable to test MMOL but will report here if anyone reports it works or does not work with mmol.

## To Apply

Warning: Only apply LoopPatches to fresh a download of Loop-dev. Use the [Loop-dev](https://loopkit.github.io/loopdocs/build/step13/) instructions in LoopDocs. Build Loop-dev (to a simulator) after downloading and keep Xcode open once the build is successful.

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

You can now copy and paste these commands into that terminal window. If you see the word `error`, stop and review the instructions. **DO NOT CONTINUE after an error is observed.**

Copy the lines below that starts with `cd Loop` by hovering the mouse near the bottom right side of the text and clicking the copy icon (should say Copy to Clipboard when you hover over it). When you click the icon, a message that says “Copied to Clipboard” will appear on your screen.

```title="Apply the patch to the Loop module"
cd Loop
git apply --reject --whitespace=fix ~/Downloads/LoopPatches-main/LoopPatch.txt
cd ..
```

Repeat for the next patch.

```title="Apply the patch to the LoopKit module"
cd LoopKit
git apply --reject --whitespace=fix ~/Downloads/LoopPatches-main/LoopKitPatch.txt
cd ..
```

Return to the `LoopPatches-main` folder in Finder and locate the Settings.bundle folder.

Return to the Xcode that was used to build Loop-dev to a simulator.

* Click on the folder icon in the left pane of Xcode
* Click on the Loop folder to open it (you should see Scripts, Common, etc)
* Go to Finder and drag (select with mouse and move while mouse is held down) the Settings.bundle folder into the Xcode left pane moving the mouse until the blue line (see graphic below) is immediately under Loop and above Scripts.
    * Let go of the mouse
* A new window will appear in Xcode as shown in the graphic below
    * You need to click in the box to the left of Loop to add to targets
    * The other add to targets boxes can be left unchecked

![settingsbundle](https://user-images.githubusercontent.com/38429455/158242367-de24fa1b-9f4e-4082-9d9b-db6ad109a563.png)

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

<img width="1209" alt="mmolChange" src="https://user-images.githubusercontent.com/38429455/192881728-272f1672-7889-4a63-9a4c-2d0e4736b0a7.png">

## To Confirm the Patches were Applied

In the Xcode window, left pane, you will notice the letter M appears by modified files.

These files should be modified. If they are not, you did not apply the patches successfully.

1. Under the Loop folder icon (left side of Xcode pane)
    * Loop/Managers/DoseMath.swift
    * Loop/Managers/LoopDataManager.swift
1. Under the LoopKit folder icon (left side of Xcode pane)
    * LoopKit/InsulinKit/InsulinMath.swift