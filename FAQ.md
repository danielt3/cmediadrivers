

## What are the disadvantages of using the driver? ##
If you're a gamer, you won't be a able to enable [EAX](http://en.wikipedia.org/wiki/Environmental_audio_extensions) effects - however, regular multi-channel 3D sound is still possible. If you plan to use the analog ports, you should look for another card - the analog parts (ADC, DAC) of the C-Media chip are pretty bad. If you have a card with a 8768+/8770 chip, you'll lose the Dolby Digital Live feature.

## What are the advantages of the using the driver? ##
This driver is completely bloat-free (e.g. no annoying tray icon), small (100kB), fast (due to the lack of sound processing) and stable. Features not seen in all the official drivers such as true 16 bit output and correct **ac3/dts passthrough** over the digital ports (coaxial, TOSLink) are fully implemented. Furthermore, it supports [bitperfect](Bitperfect.md) playback and two additional sample rates (88.2 kHz, 96 kHz).  The driver runs on all the major Windows flavors (including the Media Center Edition/MCE and 64 bit systems) and the source code is fully available. Thus it's especially well suited for HTPCs.

## Is the driver compatible with AC97/HDA chips such as C-Media 9738/9739/9880L? ##
No. All USB devices from C-Media are incompatible, too.

## What is S/PDIF? ##
S/PDIF is basically a standard which defines an interface for transmitting audio signals digitally without loss. This interface basically supports two kinds of formats:
  * _Stereo, 16 bit_: this format is used for the vast majority of audio CDs and subsequently MP3s/FLACs/etc.
  * _Dolby Digital (AC3)/dts_: this format is basically compressed/encoded multi-channel audio. Such signals are decoded by a receiver/amplifier. This kind of audio data can usually be found in pre-encoded form on many DVDs and subsequently DVD rips, some TV broadcasts and even CDs (dts CD). You need to activate the so called **passthrough mode** in software players to enable the transmission of such pre-encoded data over S/PDIF (see below). Multi-channel sound from games and other applications is usually NOT encoded in this format because a proper software encoder requires too much computational effort - the only option to output the sound is to use the analog ports.

A limitation of the S/PDIF is that it can carry no more than two uncompressed PCM audio channels - multi-channel has to be compressed beforehand. Due to bandwidth constraints, newer formats found on Bluray and HD-DVD media such as Dolby TrueHD or DTS-HD can't also be transmitted over SPDIF.

The S/PDIF signal can be transmitted optically through TOSLink (LED sender -> plastic optical fiber -> receiver) and/or electrically through RCA/coaxial cable. Optical transmission has the advantage that it's galvanically isolated and that it isn't susceptible to crosstalk (noise induction from other lines) and ground loops, so it's preferable over a coaxial cable in most cases.

## What's the recommended setting for the speaker configuration? ##
The capability to pass through a multi-channel AC3/dts signal is unaffected by this setting. For having a S/PDIF signal during music playback, the "2.0 Stereo" setting is recommended assuming that the soundcard is digitally connected to the receiver/amplifier (TOSLink/coax cable).

The driver model of Windows has unfortunately quite a few design flaws. A major one is that a driver has no way to determine whether an application wants to play a 5.1 PCM sound (e.g. some game) or just plain stereo sound (e.g. WinAMP). If the speaker configuration is set to 5.1, all sources are considered to be 5.1 and the digital ports are turned off.

## Why do I get only stereo sound when playing DVDs? ##
In all likelihood, there are some configuration issues causing this. Here are some hints:
  * Verify that the driver has been installed correctly (see below).
  * Check the settings of your favorite player, and make sure that the audio configuration is set to "passthrough" (see below).
  * Make sure that there is an ac3/dts track on the DVD you're trying to play and that it has been selected.
  * Check the connection between the soundcard and your receiver. Both devices must be linked digitally via S/PDIF by either a coax or a TOSLink cable.

## What is Dolby Digital Live? ##
Dolby Digital Live is a marketing term coined for the capability to encode multi-channel audio data to AC3/dts on the fly. This is a pretty bad idea because there's quite a nasty quality loss in the process ([transcoding](http://en.wikipedia.org/wiki/Transcoding) and low bit rates), it requires computational effort (resulting in a significant frame rate drop) and it's still bug ridden.

There are a handful of cmedia chips which support DDL with the help of the official drivers, but unlike NVidia's Soundstorm, it's entirely software based - there is no hardware acceleration. Consequently there's no implementation for Dolby Digital Live in this driver.

## How do I install the driver in 64 bit edition of Vista? ##
Currently, the only way to run the driver after installing these updates is by [pressing F8 during boot-up and disabling the enforced driver signing](http://www.codeproject.com/KB/vista/vista_x64.aspx#Driver_Signing) or by [installing the linked tool](http://www.ngohq.com/home.php?page=dseo). You have to [enable test signing](http://sites.google.com/site/dogber1/Home/dseo1.png) with the tool. Each time you've installed the driver, it needs to be [test-signed](http://sites.google.com/site/dogber1/Home/dseo3.png) _**after**_ the installation.


## I tried to load the driver, but my system crashed. How can I recover? ##
There are two possible causes:
  1. Older versions (6.xx) of the offical C-Media drivers have a nasty bug which crashes the system when they are unloaded. If you update a driver, the operating system tries to unload the old one and load the new one, and therefore this bug might have triggered the crash. A workaround is to delete the file "`cmpci.sys`" from the `C:\Windows\System32\Drivers` directory and reboot. You'll find a yellow exclamation mark next to the sound card's node in the device manager indicating that the driver couldn't be loaded. If you try to update the driver now, it should work.
  1. The open source driver has caused the crash. If the system won't boot up anymore, press F8 during the boot process and select "safe mode". Then delete the file "cmipci.sys" in your `C:\Windows\System32\Drivers` folder. Reboot and your system should come up just fine. Windows puts a so called "minidump" file in the `C:\Windows\Minidump` directory every time it crashes - you'd be a great help to the development process if you could send these files to me.


## How do I enable ac3/dts passthrough in my player software? ##
The so called "passthrough mode" enables preencoded ac3/dts/wma pro streams to be transmitted to your receiver. Such streams can often be found on DVDs, in AVIs/MKVs or other digital media.
### WinDVD ###
Start WinDVD, right-click somewhere in the video window and select 'Setup...'. Then go to the [audio tab](http://sites.google.com/site/dogber1/Home/windvd.png) and select "Digital S/PDIF Out to External Processor".
### PowerDVD ###
Start PowerDVD, right-click somewhere in the video window and select 'Configuration...'. Then go to the [audio tab](http://sites.google.com/site/dogber1/Home/powerdvd.png) and select the "Use SPDIF" entry from the 'Speaker Environment' box.
### Media Player Classic ###
Open Media Player Classic and open the 'Options' window ('View' -> 'Options' or just press the O key). Select the 'Internal Filters' node from the tree on the left and double click the 'AC3' entry in the 'Transform Filters' list. Choose "SPDIF" in the [window](http://sites.google.com/site/dogber1/Home/mplayerc.png) and click "OK".
### AC3Filter ###
Click Start, Programs, AC3Filter and then "AC3Filter Config". Check the ["Use SPDIF"](http://sites.google.com/site/dogber1/Home/ac3filter.png) box.
### ffdshow ###
Install the latest version of ffdshow. Click Start, Programs, ffdshow, "Audio decoder configuration". Click "codecs" in the left panel and [select "S/PDIF"](http://sites.google.com/site/dogber1/Home/ffdshow.png) from the drop down menus both for AC3 and dts.
### vlc ###
vlc contains a bug that results in stuttering audio playback when ac3/dts passthrough is enabled. In the most current version of vlc, there is a way to circumvent this bug: set the [output module](http://sites.google.com/site/dogber1/Home/vlc.png) to "WaveOut", save the settings and restart vlc.

## How do I enable ac3/dts passthrough in Windows Vista x64? ##
If you are using the WaveRT version of the driver, it should work out of the box with the standard x86 codecs. If you're using the non-WaveRT version, you need to upgrade to the x64 versions of both the player software and the codecs. When using x86 codecs / software, there are problems with passthrough which are caused by a bug in Vista's x86 compatibility layer. [Here](http://sourceforge.net/project/showfiles.php?group_id=173941&package_id=199416&release_id=569930) are x64 builds of ffdshow, and x64 binaries for Media Player Classic are available [here](http://tibrium.neuf.fr/).

_Update: This issue has been fixed with Vista SP1 (build 6001)._

## How do I check if the driver has been installed correctly? ##
Open the device manager (Start -> Run -> `devmgmt.msc`) and open the 'Sound, video and game controllers' leaf. If the driver has been loaded successfully, [there should be a node](http://sites.google.com/site/dogber1/Home/devmgmt.png) with exactly the name "CMI8738/8768 Wave Audio Device". Also, the 'CMI8738/8768 Control Panel' should load and display version information in the 'About'-tab.

## Do I need the Windows Driver Development Kit (WinDDK) for running this driver? ##
No. Precompiled binaries are available in all flavors on the [download page](http://code.google.com/p/cmediadrivers/downloads/list).
However, if you plan to modify the source code and/or to recompile the binaries from the source, you need the WinDDK - it contains all the vital headers, libraries and a compiler for generating proper `sys` files.

## What are the command line options for `cmicontrol.exe`? ##
Start `cmicontrol.exe` with the parameter "`-h`" to get a full list of the parameters.

## Why doesn't my receiver play sounds when I connect it digitally to the soundcard? ##
There are four possible causes:
  1. The driver hasn't been installed correctly (check above).
  1. The speaker configuration of Windows has been set to something other than Stereo / "Desktop Speakers" - this automatically disables the digital output ports because multi-channel unencoded PCM signals aren't supported by SPDIF and the driver lacks real-time encoding capabilities for reasons stated above. If you set the speaker configuration to "Stereo", the capability to forward encoded multi-channel streams (e.g. dts or dolby/AC3 from a DVD) remains unaffected.
  1. Your receiver can't play streams with a sample rate greater than 48kHz. Disallow the higher sample rates by unticking the corresponding boxes in the third tab of the control panel applet.
  1. The SPDIF output port has been disabled in the control panel applet - enable it.

## Why can't I record sounds from the microphone/line-in/aux input? ##
Most likely, the "Enable S/PDIF-in recording" box in the second tab of the control panel applet is checked - untick it, click "Apply" and restart the recording application.

## Why does a message box with the title "CreateFile()" and the text "The system cannot find the file specified." pop up when I try to start the control panel applet / cmicontrol.exe? ##
Make sure that the driver has been installed correctly. If you are using Vista, this might be caused by a bug of the operating system. There's a workaround however: close every application which might use the soundcard (browser, winamp etc.), open up the device manager and select the "CMI8738/8768 Wave Audio Device" leaf. Right-click this leaf and select "Uninstall". A window will pop up asking for confirmation - in that window, tick the box "Delete the driver software for this device" and click "OK". Then, click the "Action" menu and select "Scan for hardware changes". If a suitable driver is now found in Vista's driver repository, it will be installed. Repeat the process until Vista can't find a driver anymore, then install the open source driver. The control panel applet should now work.

## How can I get multi-channel sound when playing stereo music? ##
The driver has been specifically designed not to process any sound that passes through it. It therefore doesn't upmix stereo sources to multiple channels by itself. For doing this, you can choose from a variety of plugins for favourite music player which give you control over the upmixing process, e.g. [Foobar](http://www.hydrogenaudio.org/forums/index.php?showtopic=29985), [Winamp](http://forums.winamp.com/showthread.php?s=&threadid=66049), generic [DirectSound](http://matrix-mixer.sourceforge.net/).

## After upgrading from the WaveRT version to the non-WaveRT version, sound playback doesn't work anymore. How can I resolve this? ##
This is actually caused by a bug in Vista: the registry entry associated to the driver isn't reset properly during a driver update. This annoyance can be circumvented by doing the procedure which is described in the question above.

## Why doesn't the "Master Mute" control work? ##
The hardware doesn't have such a control. Unfortunately, there is some software which requires the presence of such a switch, so a fake switch has been implemented. In the "official" driver from C-Media, the control is emulated in software.

## Why does playback/recording fail when using WASAPI? ##
WASAPI requires Windows Vista and the WaveRT version. Also, only 65536 bytes respectively samples can be addressed by the hardware so the size of the buffer needs to be lower or equal than this value.