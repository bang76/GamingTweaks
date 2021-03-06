## Responsiveness Impact

The following things should be as low as possible:

* Audio latency
* Ping/Network latency (use the ping command to quickly check your average latency which might be different [depending on several factors])
* DPC Latency (use [LatencyMon](https://www.resplendence.com/latencymon) to check it)
* _Overall network latency_ (this can't be tested easily because it is depening on several factors)
* Keyboard input processing (depending on yourself + how fast the keyboard/mouse + OS processes the signals)


The following things should be as high as possible:

* The energy profile (should be set to Ultimate), see [here](https://docs.microsoft.com/en-us/windows-hardware/customize/desktop/customize-power-slider) why.
* Frequency (only in case you do Overclocking (!)) of several components CPU/GPU (requires testing to stabilize it).
* Power Management Mode (nVidia Control Panel [NVCP]) "application controlled" is enough.


## Choosing the "correct" Windows 10 Version

Why does it matter? [Different Windows versions](https://en.wikipedia.org/wiki/Windows_10_editions) coming with different pre-installed apps or software. Practical you could remove them but this costs a) your time and b) you might not be able to remove all apps (_easily_). The Backgrounds apps and started services matter in a sense that they might result in a [higher CPU/RAM usage](http://www.blackviper.com/service-configurations/) or lags because these apps and services typically trying to update themselves in the _right moment_ which might even ends-up with a [Bluescreen (BSOD)](https://answers.microsoft.com/en-us/windows/forum/all/windows-10-update-causing-blue-screen-errors-daily/45a08401-87c9-4c52-b160-f8548bc42c6f) or [crashes] (https://answers.microsoft.com/en-us/windows/forum/apps_windows_10-outlook_mail/windows-update-caused-loss-of-mail-app-windows/aec58c9c-9371-46b4-ab69-2b54353eff5c).

* Avoid Preview/Insider builds
* Avoid Pro/Home Editions
* Use Education/Enterprise or LTSC versions (if possible)

Edu./Ent. or LTSC versions have no pre-installed apps OR/AND you can take control over them without the need to rely on third-party apps or script. Group policy Editor (GPO - gpedit.msc) and the integrated Windows 10 own Settings can control every app/store/update behavior.


## Driver installation

The driver installation order does matter and might help to solve or prevent some problems.
* OS
* Chipset (reboot)
* USB (e.g. ASMedia Technology Inc.)
* Audio/GPU (the order doesn't matter)
* Monitor/keyboard/mouse etc.

Why is the specific order needed? Some driver(s) and their installers having troubles detecting your current hardware if e.g. the chipset isn't installed first, other programs simply conflicting with the IRQ order (older mobos).

It's not necessary to re-install the entire OS in case you made a mistake, I suggest you use [DDU](https://www.wagnardsoft.com/) in combination with [RAPR](https://github.com/lostindark/DriverStoreExplorer) in order to get rid of _possible_ leftovers and old/redundant drivers in Windows driver store folder. at this point I also suggest to create a "Driver" folder on another HDD/SSD/USB drive and place all drivers you got in there. It's maybe the first time a bit more effort to collect all of them but it helps to update the drivers + keeps on eye on the current installed ones and possible (in case you store the last two versions) you have a revision in case the newer drivers are problematic.


## Reasons to avoid WUS Drivers

In [some situations](https://www.windowscentral.com/amd-marks-50-years-gold-edition-radeon-vii-ryzen-7-bundles) the offered drivers from Windows Update Servers (WUS) are outdated compared to the ones which the OEM (AMD, nVidia, Intel etc.) offers which means that they can cause some performance or even crash related issue. My own _advice_ is to use [Wumgr](https://github.com/DavidXanatos/wumgr) which is an open source program to take control over Windows Updates (in case you don't want to mess with GPO's/Registry). Windows 10 Build 1903+ got an function to manually install drivers via the integrated GUI (in this case you might not need Wumgr).

Even some OEMs might have outdated drivers (listed on the driver pages e.g. Realtek), Station-Drivers or Win-Raid Forum often have more up-2-dated drivers.

I recommend:
- Create a folder on a usb drive or external drive where you store all you drivers (in case you re-install Windows and to keep track of your current installed drivers).
- Label the folders and files correctly which shows you directly which version you currently have installed.


#### Tools like Snappy Driver Installer & Co

Snappy Driver ([Origin](https://www.snappy-driver-installer.org/) - the version which is open-source and without ads) can help you in case your OEM doesn't provide a manual to identify your current hardware, however in my experience such tools should be avoided because they _maybe_ install or identify the wrong hardware which might only ends-up with more problems and they could contain ads or are infected with malware (since they are a huge target because driver based malware is harder to remove/spot and the installer might execute the installation process under administrative rights to gain access). My _advice_ is (even if it's more effort) to [manually identify the installed hardware](https://www.windowscentral.com/how-check-your-computer-full-specifications-windows-10) create ther driver folder and download/verify the driver from trusted websites sich as Station-Drivers & Win-RAID.


## Install AiO runtimes or repacks such as DirectX, NetFramework or Visual C++ Redistributable

There is a wide-spreading myth that says that it helps to install repacked versions to _gain gaming performance_. This is wrong and there was never any evidence given, but it's true that such repacks a) are smaller in download size (compared to the original packages) b) helping you to avoid wasting SSD/HDD space on your OS partition. For example you can use [abbodi1406 vcredist package](https://github.com/abbodi1406/vcredist) which only installs the latest Microsoft Visual C++ Redistributable Runtimes which comes without any payload - in other words you save a lot of space. While this in theory is a good thing it is not always practical because some Game Stores such as Steam or even some applications which you install forcing you to _re-install_ those packages because they won't probably detect that you already have those runtimes installed. This basically means you override such a repack with the official MS packages and at the end you won't gain anything out of it.

Problems:
* Repacks could contain malware
* Steam and other Stores, or even some application overriding or forcing you to install official runtimes even if never ones are already installed
* No performance benefits


## Operating System (general tweaking advice)
* Switch unneeded services (services.msc) from automatic to manual start. This lowers CPU/Ram usage and migrates possible attack scenarios e.g. it prevents NetBios attacks (if that service was disabled). Keep in mind that some services can't be disabled (depending on the Windows 10 Build) which then require you to disable it via registry.
* Disable unneeded tasks in Task Scheduler, pretty much as same as above the goal is to reduce CPU/Ram consumption and to possible migrate attack scenarios.
* Disable unneeded logs in Event Viewer - This is more or less optional, performance wise this doesn't gain anything but it helps your SSD life since Windows writes those events in the background to a file/disk.
* Do not install any AntiVirus product, if you like to use an AV then stick with [Windows Defender because it's good enough](https://www.tomsguide.com/us/windows-defender,review-2209.html) as proven in 'independent' AV tests.
* Use only a good NAT Firewall and [Sandboxie](https://www.sandboxie.com/) (paid product), sandbox untrusted or unknown stuff. Sandboxie has no performance drops unless you use it 'cracked' or load huge apps into it. Windows 10 Build 1903/20H1 will get it's own _free_ but limited sandbox function which would be a free alternative to Sandboxie.
* Change [Core Parking only in XP, 7 and 8](https://social.technet.microsoft.com/Forums/azure/en-US/76dac4e8-ce8f-4b83-b33d-bbef50ae5d9c/cpu-core-parking-in-windows-7-should-it-be-left-alone-or-should-users-disable-it?forum=w7itproperf) because since Windows 10 the OS itself controls it automatically already.
* Delete unneeded UWP apps and uninstall the stuff you won't need, this gains some SSD/HDD space, reduces memory/cpu usage (since such apps mostly running in the background or trying to update themselves).


### Windows 7 vs. Windows 10

Gaming on Windows 10 is not necessary better or worst, it's depending on several factors such as game development API, Engine itself, if the game was 'designed' and 'optimized' for Windows 10/7, the driver and driver profiles and many more things.

[![](http://img.youtube.com/vi/RkHFYKDOo74/0.jpg)](http://www.youtube.com/watch?v=RkHFYKDOo74 "Windows 7 Vs. Windows 10 Game Performance (right-click and open it in a new Browser tab)")

Application(s) impact
---------------

Some applications and their integrated drivers from external devices like [a mouse can cause serious FPS drops](https://old.reddit.com/r/Doom/comments/8a1m9s/psa_deactivate_the_new_razer_chroma_option_in/). Keep in mind that you should update the driver ASAP once their is a new one out, this might not only fixes performance problems, it often also fixes security holes, simply review the changelog manually before you apply the changes to see if it's worth it and do backups before you install a new upgrade.


### Fix Memory Issue before with Windows 10 Build 1607 (Anniversary Update)

* Download [EmptyStandbyList](https://wj32.org/wp/software/empty-standby-list/) and put it under e.g. C:\ (ensure you don't move this file)
* Right click > Properties and select 'Run as Admin' under compatibility.
* Open your Task Scheduler > Create Task (on the far right).
* General Tab (give it a name, doesn't matter which one!). Under security options > Change user or group > Advanced > Find Now > go down and choose SYSTEM (important to make it run silently in the background). Tick 'Run with highest privileges' and 'Hidden' at the bottom. You can find an example [here](https://stackoverflow.com/questions/6568736/how-do-i-set-a-windows-scheduled-task-to-run-in-the-background).
* Click Triggers Tab > New > On a schedule > One Time. Tick repeat task every 5 minutes (possibly excessive but it causes no issues). Also choose 'for the duration of: indefinitely'
* Actions tab > Start A program > Point to the EmptyStandbyList.exe file.
* The Standby memory is automatically cleared every 5 mins.


Task Scheduler and the impact on the OS
---------------

List of Windows tasks to disable (privacy & performance related):

* \Microsoft\Windows\Application Experience > AitAgent, ProgramDataUpdater
* \Microsoft\Windows\Autochk > Proxy
* \Microsoft\Windows\Customer Experience Improvement Program> Consolidator, KernelCeipTask, UsbCeip
* \Microsoft\Windows\DiskDiagnostic > Microsoft-Windows-DiskDiagnosticDataCollector
* \Microsoft\Windows\Maintenance > WinSAT
* \Microsoft\cSystemRestore > SR
* \Microsoft\Windows\WindowsBackup > ConfigNotification
* \Microsoft\Windows Defender > MP Scheduled Scan
* \Library\Microsoft\Windows\WindowsColorSystem\Calibration Loader (disable it if you use your own Display Color Profile)
* \Microsoft\\Microsoft\CDPUserSvc (see [here](https://account.microsoft.com/privacy/activity-history))



##### **The following workaround is specifically for Windows 1703 >= 1803**


Some games might have random stutter because Windows tries to free some resources (more or less good) which might causes game stutters. A more detailed explanation can be found to the issue over [here](https://forums.guru3d.com/threads/fix-game-stutter-on-win-10-1703-1803.420251/page-12#post-5590635). Possible workarounds in form from batch files or small utilities can be found [here](https://forums.guru3d.com/threads/fix-game-stutter-on-win-10-1703-1803.420251/).

### Power Management

Set your power setting to maximum performance (it's not needed to use an "ultimate" power-plan) if you graphic card driver has an 'maximum performance' settings enable it too, this will ensure that the GPU uses it's full potential.


### GameDVR + GameBarPresenceWriter

Whenever you stream games via OBS Studio, make sure you disable GameDVR, it is also a smart advice to in general stay away from it since most applications & games are simply not optimized for it - this doesn't have anything to do with that MS _fucked something up_ it's more that most older games (and even several new ones) are not adopted to get any benefit in such _low-latency_ mode.

Keep in mind that the registry tweak is not needed in case you're on RS5+ because `Settings > Gaming > Game bar` is the way to go (since some people reporting to have other registry values).

```bash
Windows Registry Editor Version 5.00

[HKEY_CURRENT_USER\Software\Microsoft\GameBar]
"UseNexusForGameBarEnabled"=dword:00000000
"AutoGameModeEnabled"=dword:00000000

[HKEY_CURRENT_USER\System\GameConfigStore]
"GameDVR_Enabled"=dword:00000000
"GameDVR_FSEBehavior"=dword:00000002
"GameDVR_FSEBehaviorMode"=dword:00000002
"GameDVR_HonorUserFSEBehaviorMode"=dword:00000000
"GameDVR_DXGIHonorFSEWindowsCompatible"=dword:00000000
"GameDVR_EFSEFeatureFlags"=dword:00000000
"Win32_AutoGameModeDefaultProfile"=hex:02,00,01,00,00,00,c4,20,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00
"Win32_GameModeRelatedProcesses"=hex:01,00,01,00,01,00,c0,00,c6,02,50,54,c7,02,\
  70,00,61,00,6e,00,65,00,6c,00,2e,00,65,00,78,00,65,00,00,00,8c,00,4e,8d,e1,\
  74,b8,ed,d2,02,18,4c,c7,02,1e,00,00,00,b8,ed,d2,02,1e,00,00,00,0f,00,00,00,\
  30,e7,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,00,\
  00,00,00,00,00,00,00,00,00,00

; Disable GameBarPresenceWriter.exe (needs same like PowerShell removal higher rights) - Do not use it, it's optional!
;[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsRuntime\ActivatableClassId\Windows.Gaming.GameBar.PresenceServer.Internal.PresenceWriter]
;"ActivationType"=dword:00000001
;"CLSID"="{cbfd414c-5037-3c98-a85e-a5e7ca509cfc}"
;"Server"="Windows.Gaming.GameBar.Internal.PresenceWriterServer"
; "TrustLevel"=dword:00000000
```

## Patch related performance impacts

### KB4482887

[KB4482887](https://support.microsoft.com/en-au/help/4482887/windows-10-update-kb4482887) does _for some users_ decrease the gaming performance, however it does [not have anything to do with Retpoline](https://old.reddit.com/r/microsoft/comments/ax18s7/kb4482887_caused_major_performance_issues_for_me/ehrtr4b/) changes because it's [not enabled by default](https://www.borncity.com/blog/2019/03/05/windows-10-retpoline-spectre-2-schutz-manuell-aktivieren/). Microsoft official says that you can ignore/uninstall or [hide](https://support.microsoft.com/de-de/help/4026726/windows-hide-windows-updates-or-driver-updates) the update. They promise to fix the performance issue with the next patchday.

```
// Microsoft statement
After installing KB4482887, users may notice graphics and mouse performance degradation with desktop gaming when playing certain games (eg: Destiny 2)"...
```

Fixed with Windows 10 Build 17763.379 and [KB4489899](https://support.microsoft.com/en-us/help/4489899/windows-10-update-kb4489899).


## KB4494441 Build 1809 17763.503

[Retpoline](https://techcommunity.microsoft.com/t5/Windows-Kernel-Internals/Mitigating-Spectre-variant-2-with-Retpoline-on-Windows/ba-p/295618) is activated by default with [KB4494441](https://support.microsoft.com/en-us/help/4494441/windows-10-update-kb4494441) if Spectre Variante 2 (CVE-2017-5715) was activated (manually) before the KB was installed.
