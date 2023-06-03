***
## LoopPatches

**README last updated on 3-June-2023**

LoopPatches offer several adjustments to Loop. Each is disabled by default the first time you build after adding the patches, but your selected values are maintained for subsequent builds for a given phone. Only enable the feature(s) you want to use and test. Leave the rest disabled.

Documentation found at [LoopPatches](https://www.loopandlearn.org/custom-type-one-loop-patches/). **Read the documentation before applying and using the patches.**

You can use the LoopWorkspace patch file in this repository to apply LoopPatches to released and (as of now) development code.

However, it is much easier to use the Customization Select script instead. Copy and paste this command into any terminal window to use this script to select desired Customizations for your most recent download of Loop. Documentation is at [Run Customization Select Script](https://www.loopandlearn.org/build-select/#utilities-custom).

```
/bin/bash -c "$(curl -fsSL \
    https://raw.githubusercontent.com/loopnlearn/loopbuildscripts/main/CustomizationSelect.sh)"
```

The LoopPatches code is lightly tested and **you use this at your own risk**.

There are **no guardrails**, so be extremely careful when you enter thresholds in iOS settings.

**[Loop with Patches](https://www.loopandlearn.org/main-lnl-patches/) already includes the CustomTypeOne LoopPatches with some additional customizations**
