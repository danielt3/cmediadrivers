This project aims at developing Windows drivers for [C-Media 8738 / 8768](http://www.cmedia.com.tw/?q=en/pci_audio) based soundcards, focusing on providing a compact, bloat- and bug-free alternative to the official drivers in order to squeeze the most out of the hardware. The driver is stable and it is [successfully used](UserComments.md) in a large variety of environments.

An inexpensive PCI soundcard with a C-Media chip is required for running this driver. The driver is compatible to Windows 2000, XP, Vista and 7. Due to [arbitrary](http://www.cs.auckland.ac.nz/~pgut001/pubs/vista_cost.html) [driver signing restrictions](http://www.microsoft.com/whdc/winlogo/drvsign/drvsign.mspx) imposed by Microsoft, the 64 bit versions of Windows Vista and 7 are currently unsupported although there's a workaround for [installing and running the driver](FAQ#How_do_I_install_the_driver_in_64_bit_edition_of_Vista?.md). The 64 bit version of XP and the 32 bit versions of 2000, XP, Vista and 7 are however fully supported.

#### The latest release is 1.2.6 (July 13th 2009). ####

One of the key features is the support for [bitperfect](Bitperfect.md) lossless digital transmission through [S/PDIF](http://en.wikipedia.org/wiki/Spdif), meaning that there is no tampering with the signal whatsoever. This may sound trivial, but almost all consumer grade devices lack such capabilities. In this sense, the driver is specifically designed with audiophile users in mind.

The current version features support for Dolby Digital (AC3)/DTS passthrough, analog multi-channel audio, recording and full mixer control. It comes in both [WaveRT](http://www.microsoft.com/whdc/device/audio/wavertport.mspx) (limited to Vista) and non-WaveRT (2000/XP/Vista) flavours.

The source code of the driver is distributed under the terms of the BSD license. If you want to compile the driver from the source code, you need a current version of the [Windows Driver Development Kit](http://www.microsoft.com/whdc/devtools/wdk/default.mspx). The WDK is, however, **not** required for running the driver.

If you have any suggestions for enhancements or bug fixes, feel free to contact me. I speak english and german.
