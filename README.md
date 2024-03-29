//=============================================================================
// Copyright (c) 2001-2018 FLIR Systems, Inc. All Rights Reserved.
//
// This software is the confidential and proprietary information of FLIR
// Integrated Imaging Solutions, Inc. ("Confidential Information"). You
// shall not disclose such Confidential Information and shall use it only in
// accordance with the terms of the license agreement you entered into
// with FLIR Integrated Imaging Solutions, Inc. (FLIR).
//
// FLIR MAKES NO REPRESENTATIONS OR WARRANTIES ABOUT THE SUITABILITY OF THE
// SOFTWARE, EITHER EXPRESSED OR IMPLIED, INCLUDING, BUT NOT LIMITED TO, THE
// IMPLIED WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR
// PURPOSE, OR NON-INFRINGEMENT. FLIR SHALL NOT BE LIABLE FOR ANY DAMAGES
// SUFFERED BY LICENSEE AS A RESULT OF USING, MODIFYING OR DISTRIBUTING
// THIS SOFTWARE OR ITS DERIVATIVES.
//=============================================================================

===============================================================================
==
== README
==
===============================================================================

===============================================================================
TABLE OF CONTENTS
===============================================================================
1. DEPENDENCIES
1.1. DEPENDENCY INSTALLATION
2. USB RELATED NOTES
3. FLYCAPTURE2 INSTALLATION
4. FLYCAPTURE2 REMOVAL
5. RUNNING PREBUILT UTILITIES
5.1. FLYCAP2
5.2. UPDATORGUI2
5.3. UPDATORCLI2


===============================================================================
1. DEPENDENCIES
===============================================================================

To install FlyCapture2 on linux you will need to have a few prerequisite
libraries installed.  Below is a list of libs that flycapture2 depends on.

Required:
1) libraw1394-11
2) libavcodec57
3) libavformat57
4) libswscale4
5) libswresample2
6) libavutil55
7) libgtkmm-2.4-dev
8) libglademm-2.4-dev
9) libgtkglextmm-x11-1.2-dev
10) libusb-1.0-0 (version 1.0.17 or greater recommended)

Strongly recommended:
Ubuntu 16.04 LTS:   Linux kernel version 4.4.19-35 or later.

-------------------------------------------------------------------------------
1.1. DEPENDENCY INSTALLATION
-------------------------------------------------------------------------------

To install these dependencies, the most straightforward approach is to use your
system's built-in package management utility. In the case of Ubuntu, the utility
is named "apt". Below is a set of one-line commands that can be used to install
all the required dependencies for various releases of Ubuntu Long Term Support
(LTS).

Ubuntu 18.04:
user$:  sudo apt-get install libraw1394-11 libavcodec57 libavformat57        \
        libswscale4 libswresample2 libavutil55 libgtkmm-2.4-1v5              \
        libglademm-2.4-1v5 libgtkglextmm-x11-1.2-0v5 libgtkmm-2.4-dev        \
        libglademm-2.4-dev libgtkglextmm-x11-1.2-dev libusb-1.0-0

Ubuntu 16.04:
user$:  sudo apt-get install libraw1394-11 libavcodec-ffmpeg56               \
        libavformat-ffmpeg56 libswscale-ffmpeg3 libswresample-ffmpeg1        \
        libavutil-ffmpeg54 libgtkmm-2.4-dev libglademm-2.4-dev               \
        libgtkglextmm-x11-1.2-dev libusb-1.0-0

After installing raw1394 you may need to add the raw1394 module to be loaded on
start.  To do this just add "raw1394" to the /etc/modules file.


===============================================================================
2. USB RELATED NOTES
===============================================================================

On Linux systems, image size is restricted to 2MiB or less by default. To
increase this limit so that you can make use of your imaging hardware's full
capabilities, you will need to make a minor change to your system. Full
instructions on making this change can be found at
<https://www.ptgrey.com/tan/10685#ConfiguringUSBFS>.


===============================================================================
3. FLYCAPTURE2 INSTALLATION
===============================================================================

Once all the Dependencies are installed, just install the flycapture deb files.
There are ten different packages that need to be installed.

The flycapture packages are:
- libflycapture-<version>_<platform>.deb
- libflycapture-<version>_<platform>-dev.deb
- libflycapturegui-<version>_<platform>.deb
- libflycapturegui-<version>_<platform>-dev.deb
- libflycapture-c-<version>_<platform>.deb
- libflycapture-c-<version>_<platform>-dev.deb
- libflycapturegui-c-<version>_<platform>.deb
- libflycapturegui-c-<version>_<platform>-dev.deb
- flycap-<version>_<platform>.deb
- flycapture-doc-<version>_<platform>.deb

The packages with a preceding 'lib' are all the shared objects and their
respective dev packages.  The flycap package installs the capture application
which can be launched by typing 'flycap' in a terminal or through the
Applications menu.  The flycapture-doc package contains our documentation in
pdf format.

To install these packages, we provide an easy to use install script.  You can
run the script in the same directory that you have unpacked the software into.
The install script is called 'install_flycapture.sh'

code eg:
user$ sudo sh install_flycapture.sh

This script will install all the flycapture libraries, example code, example
apps and documentation.  The flycapture install script will also ask you to
configure udev so that a user will be able to use the 1394 and usb devices.  If
you choose to configure the 1394 and usb devices this script will change
permissions on the nodes to give this particular user full read and write
access to the device nodes.  It will overwrite the default ubuntu permissions.
After running this script everything should be installed and set up for use.

Unfortunately restarting udev doesn't seem to set the permissions on the device
nodes immediately.  You may need to restart the machine before the user can
access the device nodes.


===============================================================================
4. FLYCAPTURE2 REMOVAL
===============================================================================

To remove flycapture2 just run the uninstall script that we provide.  The
removal script will also remove the udev rules therefore restoring the original
ubuntu permissions on the device nodes.

code eg:
user$: sudo sh remove_flycapture.sh


===============================================================================
5. RUNNING PREBUILT UTILITIES
===============================================================================
In addition to prebuilt examples (ie: FlyCapture2Test, CustomImageEx, etc),
along with the source code for these examples, FlyCapture2 SDK ships with a
a number of prebuilt tools for evaluating cameras (ie: FlyCap2), upgrading
firmware (ie: UpdatorGUI2, UpdatorCLI2), and so on. Since some of these tools
make use of libglademm, they require their corresponding <.glade> files to be
in the present working directory (ie: "PWD") when launched.

To make using these
tools more convenient, FlyCapture2 SDK ships with a few command-line scripts
used to automatically set the appropriate environment variables so these tools
can be run from any PWD via the command-line, or when launching the tools via
a custom icon/shortcut. To run the following tools, simply invoke their
"launcher" command via the command line, and you will not have to change the PWD
to "/usr/bin" or modify environment variables in order to launch them.

-------------------------------------------------------------------------------
5.1. FLYCAP2
-------------------------------------------------------------------------------
FlyCap2: A graphical application for testing cameras and viewing live streaming
         of image data from all supported FLIR cameras.
Location:   /usr/bin/FlyCap2
Short Name: FlyCap2
Launcher:   flycap

-------------------------------------------------------------------------------
5.2. UPDATORGUI2
-------------------------------------------------------------------------------
UpdatorGUI2: A graphical application for updating the firmware on FLIR cameras.
Location:   /usr/bin/UpdatorGUI2
Short Name: UpdatorGUI2
Launcher:   updatorgui

-------------------------------------------------------------------------------
5.3. UPDATORCLI2
-------------------------------------------------------------------------------
UpdatorCLI2: A command-line application for updating the firmware on FLIR
             cameras so that updates can be run in batch mode, and so that an
             XFree86/Xorg session does not need to be active.
Location:   /usr/bin/UpdatorCLI2
Short Name: UpdatorCLI2
Launcher:   n/a - Doesn't require a launcher script.
