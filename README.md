# CP/M 3.1 for the NABU PC

This repository contains disk images and related configuration files that will enable booting a standard implementation of the CP/M version 3.1 operating system on the NABU PC.

 
## Features

* Supports multiple disk formats:
	- 5.25" single-side, double-density, 40 track, 48 TPI
	- 5.25" double-side, double-density, 80 track, 48 TPI
	- 3.5" double-side, double-density, 160 track, 96 TPI
* Dynamically re-configures for SSDD or DSDD disks on 5.25" drives
* Standard RAW format disk images that can easily be manipulated with cpmtools
* Bootable harddrive images for use with the mame
	- `Bonus:` Check out drive B for the many included games! See the readme file in the [mame_harddrive_images](https://github.com/labomb/NABU_PC_CPM_3.1/tree/master/mame_harddrive_images) directory for details.
* Serial option board support
* Parallel port support
* Virtual 80 column mode
* Support for the F18A/Pico9918 video adapters (offers true 80 column support)
* ADM-3A terminal emulation
* Includes several custom utilities
* Official patches provided by DRI have been applied
* Uses standard DRI CP/M operating system components
* No external server software or network/RS-422 connectivity needed

 
## Directories

* The 'images' directory contains the CP/M floppy boot disk and blank images
* The 'flashfloppy' directory contains a configuration file suitable for a Gotek device running the [flashfloppy firmware](https://github.com/keirf/flashfloppy)
* The 'cpmtools' directory contains the cpmtools utility disk definitions for the various image formats supported by this release of CP/M
* The 'mame_harddrive_images' directory contains bootable 24mb images (three 8mb drives) for use with the mame Nabu PC emulator
* The 'extras' directory contains disk images with WordStar version 4 (both standard and 80 column versions), configured for the ADM-3A terminal, and the Kermit Users Guide

 
## Prerequisites

- A floppy disk controller is required. You can find an excellent replica of the original floppy controller [here](https://klyball.com/nabu-page).
- A ROM that supports booting from floppy disks. Note that the standard ROM included with the NABU PC does *not* support booting from disk. An excellent alternative ROM that supports everything the original ROM does but with the added capability of booting from disks can be found [here](https://github.com/labomb/NABU_PC_Stuff/tree/master/ROM-version-14-patched).
- A serial board (available at the same floppy controller link above) is optional. The serial board opens up support for attaching an external terminal if desired, support for xmodem file transfers to/from the NABU PC using the included transfer utilities, Kermit terminal emulation and file transfers, and much more.

 
## Documentation

Please review the NABU_CPM_3.1_Readme.pdf file for an overview of this implementation of CP/M 3.1 and the included custom utilities.

 
# Bug reports, feedback, etc...

Please use the [github issues page](https://github.com/labomb/NABU_PC_CPM_3.1/issues) to report any problems.

>**Please Note:**
 I cannot provide general support for the NABU PC, it's usage, or issues that you may have with it. Accordingly, I ask that you please not post anything relative to general usage/issues/questions here. There are several other venues for these types of questions, including websites, forums, and a Discord server. Thanks!
 
