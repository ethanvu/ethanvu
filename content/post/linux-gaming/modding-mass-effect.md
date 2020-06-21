---
title: "Installing ALOT, ALOV, MEUITM, and other mods for Mass Effect on Linux"
author: "Ethan Vu"
date: 2020-06-21T14:25:03-04:00
tags: ["Mass Effect", "Mass Effect series", "video game", "linux"]
categories: ["linux gaming"]
image: mass-effect/crew.jpg
---

# Introduction

Valve's [Proton](https://github.com/ValveSoftware/Proton/) allows Steam users to run games that don't have a native Linux implementation on their Linux machines.  It's amazing.  Mass Effect is has [a Gold rating on ProtonDB](https://www.protondb.com/app/17460) which means it runs well when using Proton, with minor adjustments.  If you have the game on Origin or you have a physical copy, you can also play on Linux, but you'll have to use [Lutris](https://lutris.net/) or something similar instead.

Unfortunately, there's not much out there on how to install mods such as [A Lot Of Textures (ALOT)](https://www.nexusmods.com/masseffect/mods/83?tab=description&BH=5) and [A Lot of Videos (ALOV)](https://www.nexusmods.com/masseffect/mods/144) for Mass Effect on Linux.  It took a lot of work to figure it out, but I was able to do it.  Here are some notes I've compiled in my quest in case you want to give it a go.

# First...

This guide is assuming you're using Steam.  Origin and physical copy users might find these notes useful though.

These are the system specs of the machine I played Mass Effect on:

* CPU: AMD Ryzen 5 3600
* GPU: AMD Radeon 5700 XT
* GPU Driver: 4.6 Mesa 20.0.7
* RAM: 16 GB
* OS: Manjaro 20.0.3
* Kernel: Linux 5.4.3.44-1

This guide should apply to most Linux distros, I suspect.  For example, GrayDog on YouTube is running Fedora 32 with ALOT and ALOV installed according to [this video](https://www.youtube.com/watch?v=o-NAJ77qI_U).

In this guide, I will assume the following:

* You have experience in Linux, e.g. permissions, using the terminal
* You know experience with Steam on Linux, e.g. you know how to backup games and how to run games with SteamPlay/Proton
* You have experience modding Mass Effect, e.g., you know that some mods are not compatible with each other and that texture mods are installed last

Finally, this guide is not exhaustive as it's entirely based off of my experience.  There might be multiple ways to install these mods or some steps that aren't actually required.  If you have any interesting information about installing mods for Mass Effect on Linux, let me know!

# Install and run your game once

First, install a fresh copy of Mass Effect.  Then run the game to make sure it works and so that Steam creates compatibility files that it needs for Proton to work its magic.

I highly recommend that you backup your game if you have the storage space because it's possible you'll mess up and need to reinstall.  If you have any saves in `/home/user/.local/share/Steam/steamapps/compatdata/17460/pfx/drive_c/users/steamuser/My\ Documents/BioWare/Mass\ Effect/Save/`, make sure to back those up too.

# Installing DLC + The Audio Issue

Next, you should install at least the Bring Down the Sky DLC first because some mods, like ME1 Recalibrated, require it.  If you want Pinnacle Station, you should install that now too.  Read [this Steam guide by Flabdad](https://steamcommunity.com/sharedfiles/filedetails/?id=1601463399).  It explains how to download and install the DLC.  It also specifies a way to fix the audio issue, but there have been reported problems with that method according to [this GitHub issue comment](https://github.com/ValveSoftware/Proton/issues/177#issuecomment-417933175).

The method to fix the audio issue that I recommend is by [LennoxLuther on ProtonDB](https://www.protondb.com/app/17460#vQ4bY78F06).

# Before Installing Any Mods

First thing to do is to download `binkw23.dll` and `bink32.dll` from [here](https://github.com/Erik-JS/masseffect-binkw32/tree/master/ME1/Release).  Put those files in `/home/user/.local/share/Steam/steamapps/common/Mass\ Effect/Binaries/`.  While testing, I've actually installed texture mods without these two dlls and I didn't run into much trouble.  I would still install them anyway.

# [ME1 Recalibrated](https://www.nexusmods.com/masseffect/mods/114)

Downloaded the exe version of this mod because installing the exe is the same as installing Bring Down the Sky and Pinnacle Station exes.  Below is an example.

```
export STEAM_COMPAT_DATA_PATH="/home/user/.local/share/Steam/steamapps/compatdata/17460/";  python3 /home/user/.local/share/Steam/steamapps/common/Proton\ 5.0/proton waitforexitandrun /home/user/Games/mass-effect/mods/ME1-recalibrated/ME1\ Recalibrated\ \(overwrites\ using\ exe\ installer\)-114-2-2-3-1590649034.exe
```

# [Improved Mako](https://www.nexusmods.com/masseffect/mods/115)

Installing this mod is very similar to how you would do it on Windows.

Keep a copy of the old `BIOGame.ini` somewhere in case you want to change back.

Extract `BIOGame.ini` from the archive you downloaded and put it in `/home/user/.local/share/Steam/steamapps/compatdata/17460/pfx/drive_c/users/steamuser/My\ Documents/BioWare/Mass\ Effect/Config/` to replace the existing version.

Alternatively, you can edit the original `BIOGame.ini`.  Look for `RBPhysicsGravityScaling` under the `[Engine.WorldInfo]` section and change it to 1.27 or your desired gravity levels.

# [Mass Effect Mouse Fix](https://www.nexusmods.com/masseffect/mods/82)

Installing this mod is also very similar to how you would do it on Windows.

Keep a copy of the old `dinput8.dll` somewhere in case you want to change back.

Extract `dinput8.dll` from the archive you downloaded and put it in `/home/user/.local/share/Steam/steamapps/common/Mass\ Effect/Binaries/`.

# [ENB or Reshade with SweetFX for Mass Effect 1](https://www.nexusmods.com/masseffect/mods/54)

Installing this mod is also very similar to how you would do it on Windows.

Extract the rar archive into `/home/user/.local/share/Steam/steamapps/common/Mass\ Effect/Binaries/`.

To uninstall, just delete those same files that you extracted.

# [A Lot of Videos (ALOV) for ME1](https://www.nexusmods.com/masseffect/mods/144)

Extract all desired files from the archives you downloaded.  From the main ALOV archive, you'll get two directories, BaseGame and BDTS.

In BaseGames, there is a `Movies` directory.  Replace the contents of `/home/user/.local/share/Steam/steamapps/common/Mass\ Effect/BioGame/CookedPC/Movies/` with this directory's contents.

In BDTS, there is also a `Movies` directory.  Replace the contents of `/home/user/.local/share/Steam/steamapps/common/Mass\ Effect/DLC/DLC_UNC/Movies/` with this directory's contents.

To install the optional FTL loading screen, take the lone `UCW_Loading_Flyby.bik` and replace `/home/user/.local/share/Steam/steamapps/common/Mass\ Effect/BioGame/CookedPC/Movies/UCW_Loading_Flyby.bik` with that file.

# Before downloading texture mods...

Disclaimer: I had a lot of problems installing texture mods.  I was not able to install MEUITM and ALOT with 100% stability, i.e. my game crashed a couple times when I clicked "Investigate" in conversation.  Also, I ran into issues where shadows didn't function properly when I installed MEUITM first then ALOT after, e.g. default male Shepard's face became completely black.

Download the Linux zips from [here](https://github.com/MassEffectModder/MassEffectModder/releases) and extract.  If the Linux zips aren't in the current release, try another.

First, run `./MassEffectModder.AppImage`.  Set the game path, e.g. `/home/user/.local/share/Steam/steamapps/common/Mass\ Effect/Binaries/MassEffect.exe`, and the user path, e.g. `/home/user/.local/share/Steam/steamapps/compatdata/17460/pfx/drive_c/users/steamuser/My\ Documents/BioWare/Mass\ Effect`.  What this will do is create a configuration file named `/home/user/.config/MassEffectModder/MassEffectModder.ini`.  The reason I use the GUI instead of the CLI version is that `MassEffectModderNoGui` gets stuck at [this line](https://github.com/MassEffectModder/MassEffectModder/blob/master/MassEffectModder/MassEffectModder/CmdLine/CmdLineParams.cpp#L775) due to an error.  I've never written any program in C++, but I know that a single C++ program might run differently on different OSes as well as different machines.  That's likely why it doesn't work, which is evident from the owner of the MassEffectModder repository removing the Linux programs in the latest release at the time of writing.

If you're using Steam and the version of Proton you're using is 5.0 or newer, you can skip to the next section.

If you're using an older version of Proton, you'll should enable the `PROTON_FORCE_LARGE_ADDRESS_AWARE` launch option because it's not enabled by default unlike Proton 5.0 and newer.  You can skip to the next section.

Otherwise, you should use `./MassEffectModderNoGui` to apply the large address awareness fix to ME1.  Below is an example.

```
/home/user/Games/mass-effect/mods/MassEffectModderNoGui --apply-me1-laa
```

I say "should" because the crashes I experienced usually occur due to LAA not working properly, [according to C3Anderson the creator of MEUITM](https://forums.nexusmods.com/index.php?/topic/1247570-meuitm/page-140#entry40934925).  However, I did try Mass Effect with LAA disabled and I felt that my game crashed more than when I had LAA enabled.  In short, I believe there is nothing to lose by enabling LAA.

# [MEUITM](https://www.nexusmods.com/masseffect/mods/1) and [A Lot Of Textures (ALOT) for ME1](https://www.nexusmods.com/masseffect/mods/83)

This section will be to install both MEUITM and ALOT.

Once you have the zip archives, extract the contents.

For MEUITM, in the mods directory, there will be many mem files.  Some mems will overwrite each other.  Check `installer.ini`, which was also extracted, to see which files correspond to which texture packs.  Choose one of each type and move or delete the others.  For example, I deleted `Eyes_Vibrant.mem` and kept `Eyes_Vanillastyle.mem`.

There will also be some zip archives in the `MEUITM` directory.  I've never tried installing them, but I suspect installing them only requires extracting the files to the proper locations similar to the SweetFX mod.

Consolidate the MEUITM and ALOT mem files into one directory.  Typically, the MEUITM is installed before ALOT.  With all mem files in one directory, the ALOT mems will be installed first since those files come first lexigraphically.  If you want to ALOT textures to override MEUITM textures, I would add some z's to the beginning of the ALOT mem files.  To check if the ALOT files were properly installed after MEUITM, compare your game to [these photos](https://www.nexusmods.com/masseffect/mods/1?tab=images).

Use `./MassEffectModderNoGui` to install the textures.  Below is an example.

```
/home/user/Games/mass-effect/mods/MassEffectModderNoGui --install-mods --gameid 1 --input /home/user/Games/mass-effect/mods/MEUITM/mods/ --alot-mode --limit-2k
```

If you want to try the 4K textures, remove the `--limit-2k` flag.

If you run into issues here, you'll need to reinstall your game (I hope you have a backup!) and all other mods.

# After installing texture mods...

This section is optional.  The reason this section is optional is because although the textures looked better when I did, I felt that the game crashed more than when I skipped this step.  Skipping this step should reduce and possibly eliminate crashes.  I say "possibly eliminate" because I played the last 10 hours of a playthrough with the original BIOEngine.ini and experienced no crashes.

Use `./MassEffectModderNoGui` to update the `BIOEngine.ini`.  Below is an example.

```
/home/user/Games/mass-effect/mods/MassEffectModderNoGui --apply-lods-gfx --gameid 1 --meuitm-mode --limit-2k
```

I would not recommend removing the `--limit-2k` flag.  My game crashed on startup when I did.

If you want to undo this, you can move `/home/user/.local/share/Steam/steamapps/compatdata/17460/pfx/drive_c/users/steamuser/My\ Documents/BioWare/Mass\ Effect/Config/BIOEngine.ini` out of the `Config` directory and run Mass Effect.  This should generate the original ini.

# Final Remarks

Feel free to ask questions if something doesn't work.  I tried a lot of things to get these mods to work so I might have forgotten to add a step or something.

Okay, that's all.  Good luck and have fun!
