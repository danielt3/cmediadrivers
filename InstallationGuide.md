# Installation Guide #

Download and unzip the archive containing the binaries to a folder of your choice. The files can be downloaded from [this page](http://code.google.com/p/cmediadrivers/downloads/list).
  * The bin-x86.zip archive has the compiled binaries for regular x86 32 bit systems, and bin-x64.zip file contains the binaries for EM64T/AMD64 64 bit systems.
  * Only the non-WaveRT (bin-x86.zip / bin-x64.zip) versions are compatible with Windows XP/2k.
Make sure that your soundcard is detected by the system (item in the Device Manager). Browse to the folder which contains the unpacked driver files. Start the setup executable and click "Install Driver":

![http://sites.google.com/site/dogber1/Home/installer.png](http://sites.google.com/site/dogber1/Home/installer.png)

You probably have to click away one of these annoying "unsigned drivers" dialogs:

![http://sites.google.com/site/dogber1/Home/image-7.png](http://sites.google.com/site/dogber1/Home/image-7.png)
![http://sites.google.com/site/dogber1/Home/xp-image-8.png](http://sites.google.com/site/dogber1/Home/xp-image-8.png)

If a reboot is required, you will be asked. After the installation is finished, it's a good time to get rid of the remnants of the official C-Media drivers, e.g. the memory eating mixer.exe in your Windows folder.

## Vista Configuration (not necessary on Windows 2000 / XP) ##
Once the driver has been installed, open up the "Sound" applet in the control panel and select your default output:

![http://sites.google.com/site/dogber1/Home/image-8.png](http://sites.google.com/site/dogber1/Home/image-8.png)

The SPDIF Interface **must** be the default device if you want AC3/DD passthrough.

Then open up the properties page of the SPDIF Interface and choose which audio formats should be passed through the digital connectors to your receiver:

![http://sites.google.com/site/dogber1/Home/image-9.png](http://sites.google.com/site/dogber1/Home/image-9.png)

And you're done.

## Troubleshooting ##
If you run into problems, you might want to check out the manual installation guide for [Windows XP](http://cmediadrivers.googlepages.com/xpinstallation) / [Windows Vista](http://cmediadrivers.googlepages.com/vistainstallation).