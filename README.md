# Overview
Are you worried about someones app or script to multibox Diablo 2? Do you have PTSD from being rick rolled in scripts?<br>
This is a guide on all the method I know of for Diablo 2 Resurrected Multi boxing that don't require a script or custom application.<br>
<br>
If you do want to use a script, I heard that [this one](https://github.com/shupershuff/Diablo2RLoader) is pretty damn good and the guy that made it is accepting mortgage payments as a way to say a small thanks.<br>
Outside of this there are a couple other good scripts I've seen out there. Obviously ensure it's open source, don't be downloading some dodgy .exe.

# Game Launching Methods
## Launch via Shortcut
This method will launch the game directly from your desktop, without the need to open the battlenet client.
1. Browse to your Diablo 2 Resurrected game install folder.
2. Right click on d2r.exe and create shortcut. Copy shortcut to desktop.
3. Edit the shortcut and append the target field with:<br>
  -username YourBnetEmail -password YourBnetPassword -address \<region><br>
\<Region> could be us.actual.battle.net, EU.actual.battle.net and KR.actual.battle.net.
4. Rename shortcut to your linking.
5. Launch game from shortcut.
6. Kill handle as per [Handle Killing Methods](#handle-killing-methods)

You can either copy a shortcut for each account and region or simply keep one shortcut per account and edit address details the shortcut when you want to switch regions.<br>
Drawback with this method is that Blizzard forgot to make this work with MFA, which is kind of moot anyway as Blizzard prevent you from using standard MFA apps (which allow additional accounts).<br>
If you have issues logging in, try logging in manually into battlenet as sometimes there are captcha codes (especially if you typo your email or password).<br>

## Launch via Battlenet
Ew yucky. Ignore the plethora of YouTube guides telling you to do this. Gross.<br>
Not only will you be tripping over various battlenet windows (which is a nightmare when changing regions) but you'll also need to copy the game install folder several times.

# Handle killing Methods
## ProcExp.exe
Instructions TBC. Most youtube guides cover off how to use this.<br>
**Download**
https://learn.microsoft.com/en-us/sysinternals/downloads/process-explorer
## Handle64.exe
Instructions TBC<br>
Note: Requires a script (unless you like typing commands manually)<br>
**Download**
https://learn.microsoft.com/en-us/sysinternals/downloads/handle

# Methods without requiring handle to be killed.
All of these options are gross from a usability, Quality of Life and even financial (hardware) perspective but do functionally work without the need to use software to kill process handle.
## Virtual Machine
TBC
## Windows Account Switching
TBC
## Multiple Physical PC's
TBC

# Notes
## Performance Tips
TBC but long story short, set FPS cap, run in windowed mode, reduce gfx settings to low
## FAQ
TBC
## Other notes
All game instances share the same settings file (Settings.json) which can be found in C:\Users\USERNAME\Saved Games\Diablo 2 Resurrected.<br>
This means if you edit the graphics/audio settings from the in game menu, it will apply these settings to the next time you launch the game, regardless of the account.<br>
Character settings are stored seperately.
