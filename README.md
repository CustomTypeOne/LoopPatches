***
## LoopPatches

**README last updated on 02-August-2023**

**WARNING - the patches in this repository are no longer maintained here**

Please read [New Home for LoopPatches](#new-home-for-looppatches)

Original Open Source warning:

These patches are provided open source.

It is your responsibility to review the code. These patches are highly experimental for testing, research, and education and are not approved for therapy. It is your responsibility to review the code and understand the changes using this makes. You should also run tests in an xcode simulator to review the effect they have on Loop behavior and settings.

LoopPatches offer several adjustments to Loop. Each is disabled by default the first time you build after adding the patches, but your selected values are maintained for subsequent builds for a given phone. Only enable the feature(s) you want to use and test. Leave the rest disabled.

## New Home for LoopPatches

Documentation for the CustomTypeOne LoopPatches is found at [LoopPatches](https://www.loopandlearn.org/custom-type-one-loop-patches/). 

**Read the documentation before applying and using the patches.**

The patches stored in this repository are no longer being updated.

* They do not work with development code
* They will not work with the next release of Loop

The Loop and Learn team has taken over development for these patches as part of the CustomizationSelect script used to modify Loop.

* Documentation is at [Customization Select](https://www.loopandlearn.org/custom-code)

The Customization Select Script automatically handles selecting the correct version as updates are required by changes to dev or released code.

Copy and paste the command below into any terminal window to use this script to select desired Customizations for your most recent download of Loop.

```
/bin/bash -c "$(curl -fsSL \
    https://raw.githubusercontent.com/loopandlearn/lnl-scripts/main/CustomizationSelect.sh)"
```

The LoopPatches code is lightly tested and **you use this at your own risk**.

There are **no guardrails**, so be extremely careful when you enter thresholds in iOS settings.

**[Loop with Patches](https://www.loopandlearn.org/main-lnl-patches/) already includes the CustomTypeOne LoopPatches with some additional customizations**
