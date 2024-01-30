# Overview
Greetings Stranger! I'm not surprised to see your kind here.<br>
<br>
Are you worried about someones app or script to multibox Diablo 2? Do you have PTSD from being rick rolled in scripts?<br>
This is a guide on all the methods I know of for Diablo 2 Resurrected Multi boxing that don't require a script or custom application.<br>
<br>

There are a couple good scripts and apps I've seen out there (Sunblood's D2rML and ISBoxer springs to mind and oh, [this silly one](https://github.com/shupershuff/Diablo2RLoader) that I made).<br>
For the free ones I obviously recommend it's open source, don't be running some dodgy .exe where it can't be publically vetted on what it's doing.
For the paid ones, that's at your own risk but there are some seemingly reputable ones out there.<br>
I would recommend staying clear of any game altering mods, or anything that adds any element of automation within the game etc (at the end of the day, the game is for playing right?).

# Game Launching Methods
## Launch via Parameters (with a desktop Shortcut)
This method will launch the game directly from your desktop, without the need to open the battlenet client.
1. Browse to your Diablo 2 Resurrected game install folder (you only need one install folder).
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

NOTE: KR.Actual.Battle.net has been down since 7th Oct 2023. Blizzard are useless and haven't resolved this service outage.

## Launch via Battlenet Client
Ew yucky. Ignore the plethora of YouTube guides telling you to open multiple battlenet instances to do this. Gross.<br>
Not only will you be tripping over various battlenet windows (which is a nightmare when changing regions) but you'll also need to copy the game install folder several times.

## Launch via Authentication Token (Advanced)
This is technically the same way that Battle.net uses to launch and does work with MFA (Multi-Factor Authentication) enabled accounts.
This token is basically saying this is my account, I'm the owner and I've authenticated. As such no username, password or MFA is needed.
In the registry key "HKCU:\SOFTWARE\Blizzard Entertainment\Battle.net\Launch Options\OSI" is a binary value called "WEB_TOKEN".
This registry value gets updated when you launch the game (from battle.net), reach character selection screen or close the game.
Essentially, to launch via this method, the WEB_TOKEN must be set prior with the appropriate account Authentication Token prior to launching d2r.exe
Note that the Token provided by the battle.net client is only a temporary token and will expire. We can however set a token that will not expire unless you disable/enable MFA on your account.

To obtain your token, decrypt, convert to binary and set the registry key, perform the following steps:
1. Open your preferred Browser in private mode
2. Browse to https://us.battle.net/login/en/?externalChallenge=login&app=OSI
3. Login with your battlenet details. This will show an error page (this is expected). The error page link contains an identifier for your account in the form of US-d12ab21123abcdefabcdefabcdef1231-123123123.
  a. eg if your URL is http://localhost:0/?ST=US-d12ab21123abcdefabcdefabcdef1231-123123123&flowTrackingId=123a1234-1234-1234-a1b2-123ab45c6de7, copy "US-d12ab21123abcdefabcdefabcdef1231-123123123" from this link.
5. DO NOT SHARE SCREENSHOTS OF THIS PAGE OR THE LINK TO THIS PAGE ANYWHERE ONLINE.
6. Use the following PowerShell commands, exchanging Token for your token and Region to the appropriate region:
    ```
    # Launch as admin
     if (!([Security.Principal.WindowsPrincipal][Security.Principal.WindowsIdentity]::GetCurrent()).IsInRole([Security.Principal.WindowsBuiltInRole] "Administrator")) { Start-Process powershell.exe "-NoProfile -ExecutionPolicy Bypass -File `"$PSCommandPath`"" -Verb RunAs; exit } #commands require elevated rights. Launch as admin.
    
    # Change these settings to suit you
     $Region = "NA" # Choose between NA, EU and KR.
     $Token = "US-d12ab21123abcdefabcdefabcdef1231-123123123" # Obtain this token from the site above. KEEP THIS SECRET. Sharing this is like giving away the location and keys to your car.
     $GamePath = "C:\Program Files (x86)\Diablo II Resurrected" # Where your game is installed.
    
    # Define Entropy
     $Entropy = @(0xc8, 0x76, 0xf4, 0xae, 0x4c, 0x95, 0x2e, 0xfe, 0xf2, 0xfa, 0x0f, 0x54, 0x19, 0xc0, 0x9c, 0x43)
    # Convert the token and entropy to byte arrays
     $TokenBytes = [System.Text.Encoding]::UTF8.GetBytes($Token)
     $EntropyBytes = [byte[]] $Entropy
    # Encrypt the token
     [void][System.Reflection.Assembly]::LoadWithPartialName("System.Security")
     $ProtectedData = [System.Security.Cryptography.ProtectedData]::Protect($TokenBytes, $EntropyBytes, [System.Security.Cryptography.DataProtectionScope]::CurrentUser)
    # Set registry Values
     $Path = "HKCU:\SOFTWARE\Blizzard Entertainment\Battle.net\Launch Options\OSI"
     Set-ItemProperty -Path $Path -Name "REGION" -Value $Region
     Set-ItemProperty -Path $Path -Name "WEB_TOKEN" -Value $ProtectedData -Type Binary
    # Start the game
     Start-Process "$Gamepath\D2R.exe" -ArgumentList -uid OSI
    ```
Note: Due to how the game updates registry values, the drawback to using this method is that you can't open all accounts up at once, or close a game instance while another is loading. You must wait to get to the character selection screen before launching a subsequent account.

Credit to dschu012 for [discovering this](https://github.com/Farmith/D2RMIM/pull/11/files#diff-5408bbaf05738fe52729de093b38981abecffeb304b1cd388713cbe6a0461d21) and thanks to Sunblood for pointing me towards this discovery.

# Handle killing Methods
This requires 3rd party software (albeit Microsoft recommended) to kill the process handle that runs within d2r.exe when launched.<br>
Killing this handle allows for multiple instances.
## Process Explorer (ProcExp.exe)
Long story short, launch game, open procexp as administrator, search for d2r.exe in the top right filter. Click on the handle tab and scroll down (it's a sizeable list) until you see an entry for 'DiabloII Check For Other Instances'. Right click on it and choose close. You are then clear to launch a subsequent game instance.<br>
Note that most youtube guides cover off how to use this old method, so I won't rehash instructions here.<br>
**Download\:** https://learn.microsoft.com/en-us/sysinternals/downloads/process-explorer
## Handle64.exe
This is a handy command line based tool that can also kill process handles like Process Explorer.
Note: Requires a script (unless you like typing commands manually):<br>
**Download\:** https://learn.microsoft.com/en-us/sysinternals/downloads/handle

```
  # Launch as admin
  if (!([Security.Principal.WindowsPrincipal][Security.Principal.WindowsIdentity]::GetCurrent()).IsInRole([Security.Principal.WindowsBuiltInRole] "Administrator")) { Start-Process powershell.exe "-NoProfile -ExecutionPolicy Bypass -File `"$PSCommandPath`"" -Verb RunAs; exit } #commands require elevated rights. Launch as admin.

  # Inspect running processes for d2r.exe and examine all handles and write to a d2r_handles.txt
  & "$PSScriptRoot\handle\handle64.exe" -accepteula -a -p D2R.exe > $PSScriptRoot\d2r_handles.txt
	$proc_id_populated = ""
	$handle_id_populated = ""
	foreach($Line in Get-Content $PSScriptRoot\d2r_handles.txt) {
		$proc_id = $Line | Select-String -Pattern '^D2R.exe pid\: (?<g1>.+) ' | %{$_.Matches.Groups[1].value}
		if ($proc_id){
			$proc_id_populated = $proc_id
		}
		$script:handle_id = $Line | Select-String -Pattern '^(?<g2>.+): Event.*DiabloII Check For Other Instances' | %{$_.Matches.Groups[1].value}
		if ($handle_id){
			$handle_id_populated = $handle_id
		}
		if ($handle_id){
			Write-Host "Closing" $proc_id_populated $handle_id_populated
			& "$PSScriptRoot\handle\handle64.exe" -p $proc_id_populated -c $handle_id_populated -y
		}
	}
```

This essentially checks a d2r.exe for the handle and closes it if it exists.
I'm lazy and didn't write this, I just copied from [here](https://forums.d2jsp.org/topic.php?t=90563264&f=87&p=595448522)

# Methods without requiring handle to be killed.
All of these options are gross from a usability, quality of life and even financial (hardware) perspective but do functionally work without the need to use software to kill process handle.
## Virtual Machine
You can run D2r from a VM, however there are several technical steps required. Not all free VM technologies support this.
If you want to explore this avenue, this guy has great instructions for Hyper V VM setup and steps for GPU partitioning:<br>
https://www.youtube.com/watch?v=XLLcc29EZ_8
## Windows Account Switching
Essentially this is just creating multiple user accounts on your workstation, login to each, launch d2r from them and switch windows accounts to access the next D2r account.
## Multiple Physical PC's
Simple. Have multiple Physical computers used to launch the game with different accounts.
That's it.

# Notes
## Performance Tips
If you don't want your Diablo games to run like a slideshow, here are some tips. You'll of course need to adjust based on your hardware and setup.
1. IMPORTANT. Set an Frame Rate (FPS) cap in the graphics options. Recommend 60 but adjust depending on your GPU power and instances you're running. This will prevent each instance from trying to fully utilise your GPU compute.
2. Reduce graphics settings in game to performance over quality.
3. Run games in Windowed mode. Especially if you have more than one monitor. Not only will it save you performance, it's waaaay easier than alt tabbing.
4. In addition to changing your settings to launch the game in windowed mode, you should also make your secondary account windows smaller (ie lower resolution) to save on GPU utilisation. You can adjust resolution from the in game menu or simply by shrinking the window. If need you can of course do the opposite and maximise one of the smaller windows if you are playing another character for a bit.
5. If you are wanting different graphics settings for different accounts (eg different FPS cap, different audio settings, different resolution, nicer graphics settings etc etc), then I would highly recommend making use of the QOL features of this script. The automatic settings switcher can be used so that each account loads with it's own settings at launch. There is also the manual setting switcher feature if you want to define what settings file to load for a given account. See the relevant sections above for more info.
6. Obviously if you run other graphic demanding things like wallpaper engine in the background, this will hurt your overall FPS. Some wallpapers will have neglible impact but some are  noticably impactful on performance.
7. Make use of hardware monitoring software to see how much you are utilising RAM, CPU, GPU - Processor and GPU - VRAM. If you are under or overutilised you can adjust your settings accordingly for the best experience.

**My setup**<br>
Note that on my specs (5950x, RTX2080s (which has 8GB VRAM), 32GB RAM), I run my instances on the lowest graphics options possible. <br>
DLSS is set to ultra performance. Framerate (FPS) caps for secondary accounts are around 50fps. For my primary account I set the FPS cap to 60fps.<br>
<br>
With 3 instances (2 windows at approx 1280x780 resolution, 1 window (primary account) at 2556x1373 resolution, The CPU is barely used, Memory is about 85% utilised, VRAM is 80% utilised and GPU is about 85-90% (6800MB).<br>
With 4 instances (an additional window at approx 1280x780), CPU is still fine (15%), Memory is maxed out, VRAM is 92%+ (7600MB+) and GPU is 95-100%. Different parts of the game can run pretty poorly and as such sometimes I reduce the secondary accounts FPS Cap to around 44 instead.<br>
<br>
I've noted that with my hardware running 4 instances is generally not fun graphically due to performance stutters, FPS drops and increased chance of crashing. I'd argue that running 4 or more accounts is confusing and isn't fun logistically either but I digress.

Lastly a quick note that there are mods which force legacy graphics which some folk enjoy the benefits from. However I can't endorse mods as using any mod is at your own risk.<br>

## Other notes
All game instances share the same settings file (Settings.json) which can be found in C:\Users\USERNAME\Saved Games\Diablo 2 Resurrected.<br>
This means if you edit the graphics/audio settings from the in game menu, it will apply these settings to the next time you launch the game, regardless of the account.<br>
Character settings are stored seperately.
