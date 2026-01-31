## What is 'Hybrid CP/M' ?

This implementation of CP/M supports floppy drives (A and B) and a harddrive (with C and D partitions) concurrently. If booting with one of these floppy images in drive A, floppy drive B and harddrives C and D and also fully accessible. Likewise, if booting from harddrive C, floppy drives A and B as well as harddrive D are fully accessible.

Note that there is a bit of a trade-off with this variation of CP/M. Specifically, it requires more memory to support both drive devices and as such less usable memory (TPA) is available for applications. You may discover that larger applications, game loaders, large Basic programs, etc... may not work properly because they require more usable memory than is available when running with this CP/M release.


## Hybrid CP/M images for mame

Floppy images:
* NABU_CPM3_BOOT_HD_HY.s4.img       : bootable single-side, double-density, 40 track, 48 TPI
* NABU_CPM3_BOOT_HD_HY.d8.img       : bootable double-side, double-density, 80 track, 48 TPI
* NABU_CPM3_BOOT_HD_HY.d16.img      : bootable double-side, double-density, 160 track, 96 TPI
* NABU_CPM3_80_BOOT_HD_HY.s4.img    : F18A/Pico9918 VGA (80 column) bootable single-side, double-density, 40 track, 48 TPI
* NABU_CPM3_80_BOOT_HD_HY.d8.img    : F18A/Pico9918 VGA (80 column) bootable double-side, double-density, 80 track, 48 TPI
* NABU_CPM3_80_BOOT_HD_HY.d16.img   : F18A/Pico9918 VGA (80 column) bootable double-side, double-density, 160 track, 96 TPI

Harddrive images:
* NABU_CPM3_HD_HY.chd               : bootable 'hard drive' image with two 8mb drives
* NABU_CPM3_HD_HY_80.chd            : F18A/Pico9918 (80 column) bootable 'hard drive' image with two 8mb drives

Include something like '-option2 hdd -hard NABU_CPM3_HD_HY.chd' in the mame startup command line, and be sure that you are using a ROM that supports booting from the hard drive, such as [this one](https://github.com/labomb/NABU_PC_Stuff/tree/master/ROM-version-14-patched).


## Managing files on hard drive images using cpmtools

The cpmtools diskdef file found [here](https://github.com/labomb/NABU_PC_CPM_3.1/tree/master/cpmtools) contains definitions for the two hard drives contained in the image... nabu3hda and nabu3hdb for drives A and B respectively. It is important to note that even though the drives appear in CP/M as C and D, they are accessed via cpmtools using the A and B diskdef profiles.

To add, delete, rename, etc... files on any of the drives, do the following:

1. Extract a raw binary image from the harddrive .chd file
	- chdman extracthd -i NABU_CPM3_HD_HY.chd -o NABU_CPM3_HD_HY.raw

2. Use cpmtools to manage files on the raw image... for example:
	- to copy PC file galaxian.com to drive a: user area 0
		* cpmcp -f nabu3hda NABU_CPM3_HD_HY.raw galaxian.com 0:
	- to copy all files in PC directory 'games' to drive b: user area 1
		* cpmcp -f nabu3hdb NABU_CPM3_HD_HY.raw games/\*.* 1:
	- to delete file 'test.com' from drive b: user area 2
		* cpmrm -f nabu3hdb NABU_CPM3_HD_HY.raw 2:test.com
	- to copy file mbasic.com from drive b: user area 4 to the PC
		* cpmcp -f nabu3hdb NABU_CPM3_HD_HY.raw 4:mbasic.com mbasic.com
	- to list files on drive a: user area 0
		* cpmls -f nabu3hda NABU_CPM3_HD_HY.raw

3. When you are done with changes, convert the raw image back to a chd file
	- chdman createhd -f -chs 1024,2,16 -c none -i NABU_CPM3_HD_HY.raw -o NABU_CPM3_HD_HY_new.chd

>**Note:**
 The chdman utility is provided with the mame package. If building mame yourself, be sure to enable building the optional tools as well. If using a pre-compiled variation of mame that does not include this utility, you can use the Windows chdman.exe file found in this directory.
 