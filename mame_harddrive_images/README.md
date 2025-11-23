## Hard drive images for mame

* NABU_CPM3_HD.chd            : bootable 'hard drive' image with three 8mb drives
* NABU_CPM3_HD_80.chd         : F18A VGA (80 column) bootable 'hard drive' image with three 8mb drives

Include something like '-option2 hdd -hard NABU_CPM3_HD.chd' in the mame startup command line, and be sure that you are using a ROM that supports booting from the hard drive, such as [this one](https://github.com/labomb/NABU_PC_Stuff/tree/master/ROM-version-14-patched).

## Managing files on hard drive images using cpmtools

The cpmtools diskdef file found [here](https://github.com/labomb/NABU_PC_CPM_3.1/tree/master/cpmtools) contains definitions for the three hard drives contained in the image... nabu3hda, nabu3hdb, and nabu3hdc for drives A, B, and C respectively. To add, delete, rename, etc... files on any of the drives, do the following:

1. Extract a raw binary image from the harddrive .chd file
	- chdman extracthd -i NABU_CPM3_HD.chd -o NABU_CPM3_HD.raw

2. Use cpmtools to manage files on the raw image... for example:
	- to copy PC file galaxian.com to drive a: user area 0
		* cpmcp -f nabu3hda NABU_CPM3_HD.raw galaxian.com 0:
	- to copy all files in PC directory 'games' to drive b: user area 1
		* cpmcp -f nabu3hdb NABU_CPM3_HD.raw games/\*.* 1:
	- to delete file 'test.com' from drive c: user area 2
		* cpmrm -f nabu3hdc 2:test.com
	- to copy file mbasic.com from drive b: user area 4 to the PC
		* cpmcp -f nabu3hdb NABU_CPM3_HD.raw 4:mbasic.com mbasic.com
	- to list files on drive a: user area 0
		* cpmls -f nabu3hda NABU_CPM3_HD.raw

3. When you are done with changes, convert the raw image back to a chd file
	- chdman createhd -f -chs 1536,2,16 -c none -i NABU_CPM3_HD.raw -o NABU_CPM3_HD_new.chd

>**Note:**
 The chdman utility is a utility provided with mame. If building mame yourself, be sure to enable building the optional tools as well.
 