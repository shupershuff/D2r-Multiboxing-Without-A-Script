<br>

**THIS PAGE IS A WORKING DRAFT AND ISN'T FINISHED**    
<br>
<br>
# Overview
Greetings Stranger! I'm not surprised to see your kind here.<br>
<br>
Are you worried about someones app or script to multibox Diablo 2? Do you have PTSD from being rick rolled in scripts?<br>
This is a guide on all the methods I know of for Diablo 2 Resurrected Multi boxing that don't require a script or custom application.<br>
<br>
If you do want to use a script, I heard that [this one](https://github.com/shupershuff/Diablo2RLoader) is pretty damn good and the guy that made it is accepting mortgage payments as a way to say a small thanks. Payoff some internet strangers house today and feel great about it tomorrow! Everybody wins! I just need to add a payment option and I'm sure the mortgage will be payed off immediately hmm...<br>

Anywho, outside of my script there are a couple other good scripts and apps I've seen out there. For the free ones I obviously recommend it's open source, don't be running some dodgy .exe where it can't be publically vetted on what it's doing.
For the paid ones, that's at your own risk but there are some seemingly reputable ones out there. 
I would recommend staying clear of any game altering mods etc.

# Game Launching Methods
## Launch via Shortcut
This method will launch the game directly from your desktop, without the need to open the battlenet client.
1. Browse to your Diablo 2 Resurrected game install folder.
2. Right click on d2r.exe and create shortcut. Copy shortcut to desktop.
3. Edit the shortcut and append the target field with:<br>
  -username YourBnetEmail -password YourBnetPassword -address \<REGION><br>
\* \<REGION> could be us.actual.battle.net, EU.actual.battle.net or KR.actual.battle.net for Americas, Europe or Asia respectively.
4. Rename shortcut to your linking.
5. Copy shortcut and edit username and password for second account. Repeat for additional accounts.
6. Launch 1st instance of game from shortcut.
7. Kill handle as per [Handle Killing Methods](#handle-killing-methods)
8. Launch 2nd instance of game from shortcut.
9. Kill Handle again
10. Repeat steps 8 and 9 for subequent accounts.

You can either copy a shortcut for each account and region or simply keep one shortcut per account and edit address details the shortcut when you want to switch regions.<br>
Drawback with this method is that Blizzard forgot to make this work with MFA, which is kind of moot anyway as Blizzard prevent you from using standard MFA apps (which allow additional accounts).<br>
If you have issues logging in, try logging in manually into battlenet as sometimes there are captcha codes (especially if you typo your email or password).<br>

## Launch via Battlenet
Ew yucky. Ignore the plethora of YouTube guides telling you to do this. Gross.<br>
Not only will you be tripping over various battlenet windows (which is a nightmare when changing regions) but you'll also need to copy the game install folder several times.

## Authentication Alternatives
TBC reference temporary WEB_TOKEN and more permanent WEB_TOKEN methods of authenticating.

# Handle killing Methods
This requires 3rd party software (albeit Microsoft recommended) to kill the process handle that runs within d2r.exe when launched.<br>
Killing this handle allows for multiple instances.
## ProcExp.exe
Instructions TBC but long story short, launch game, open procexp, search for d2r.exe in the top right filter. Click on the handle tab and scroll down (it's a sizeable list) until you see an entry for 'DiabloII Check For Other Instances'. Right click on it and choose close. You are then clear to launch a subsequent game instance.<br>
Note that Most youtube guides cover off how to use this.<br>
**Download\:** https://learn.microsoft.com/en-us/sysinternals/downloads/process-explorer
## Handle64.exe
Instructions TBC<br>
Note: Requires a script (unless you like typing commands manually)<br>
**Download\:** https://learn.microsoft.com/en-us/sysinternals/downloads/handle

# Methods without requiring handle to be killed.
All of these options are gross from a usability, Quality of Life and even financial (hardware) perspective but do functionally work without the need to use software to kill process handle.
## Virtual Machine
TBC but this guy has great instructions:<br>
https://www.youtube.com/watch?v=XLLcc29EZ_8
## Windows Account Switching
TBC - Essentially just create multiple user accounts on your workstation, login to each, launch d2r from them and switch windows accounts to access the next D2r account.
## Multiple Physical PC's
TBC surely no instructins needed here anyway.

# Notes
## Performance Tips
TBC but long story short, set Framerate (AKA FPS) cap to 60, run in windowed mode, reduce gfx settings to low.<br>

There are mods which force legacy graphics which some folk enjoy but I can't endorse these, use at your own risk.
## FAQ
TBC
## Other notes
All game instances share the same settings file (Settings.json) which can be found in C:\Users\USERNAME\Saved Games\Diablo 2 Resurrected.<br>
This means if you edit the graphics/audio settings from the in game menu, it will apply these settings to the next time you launch the game, regardless of the account.<br>
Character settings are stored seperately.
