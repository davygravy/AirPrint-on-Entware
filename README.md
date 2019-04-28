# AirPrint on Entware

###_**SEE THE WIKI (menu above) FOR HOW-TO SPECIFICS, DIRECTIONS, AND DETAILS.**_###

AirPrint emulation on Entware with fewer hiccups

This intends to be a predictable, no-surprises, quick-starting, no-mess, no-fuss and relatively painless way to get AirPrint emulation working on any capable Entware equipped router or other device. I've tested it extensively on my TomatoUSB/FreshTomato and MerlinWRT mipsel/mipselsf routers.  It works with both ARM and mipselsf-k2.6.  I have not tested it on the newer mipselsf-k3.4 devices, since I don't have one.

A main goal was to make AirPrint emulation work out-of-the-box.  The package set is probably the most minimal that will support Airprint out-of-the-box.   For my part, I can only see one reason to install CUPS on a router:  AirPrint!  I set it up with regard keeping the packages as small as possible.  I wanted it to work right away, and not have to compile another component, adjust, mess around, etc.

The modified files (and parent directories) are contained in the 'packages/libs', and 'rtndev'.  You should be able to drop the CUPS and cups-filters directories directly into the correct location in the OpenWRT Buildroot setup that Entware uses, if you are going to build your own ipkg files.  These four packages built correctly using the above-mentioned Buildroot system , cloned from Entware in April 2019.

NOTE:  Mind your own security with CUPS.  Read the fancy manual pages, know what security level is right for you, and implement it.

*Changes:*

  * 4/26/19 -  Adding support for legacy routers running Entware-ng (mipselsf-k2.6).  Tested extensively on a Belkin ShareMax N300 running Toastman-TomatoUSB and Entware-ng.
  
  * 4/22/19 -  modifications to **cups-filters** , allowing normal interaction with CUPS and support for printers.  Also DejaVuMono font added as dependency.  https://github.com/Entware/rtndev/commit/abe03767f3557e951ca2f9c13c074fd199e6707 and  https://github.com/Entware/rtndev/commit/3b1b7ea7126b0883cc9ca77d6f05c811085503a6
  
  * 4/18/19 - Moved towards Entware, slightly away from Entware-ng.  At this point for Entware, only three non-vanilla ipk files need to be installed: cups, libcups and cups-filters.
  
  * 4/16/19 -  found "missing cups device" in ghostscript, fixed by @auryzhov in git : https://github.com/Entware/rtndev/commit/c89550308444cc7820beaafa05a4b99d824d807a
  
  * 2/15/17 -  ARM7soft tarball was tested and works on Asus RT-AC68R/U [ FreshTomato (19.1) K26ARM USB AIO-64K ].  Note that due to some newer versions of CUPS being listed in the official feeds, certain "force-" options such as "--force-checksum" might have to be used to install the packaged items.  Worked for me, YMMV.
   
  * 1/24/17 -  ARM7soft tarball was added for newer Broadcom ARM routers, e.g. RT-AC1900. Not yet tested.
  
  * 1/20/17 - pull request for **hplip** was committed :  https://github.com/Entware-ng/entware-oldpackages-ports/commit/c5b2fd3751da6f4837c86275280f866940c7412c .  As a consequence, you no longer have to install the non-vanilla/custom hplip package: use the one in the Entware feed. 
  
  * 1/9/17 - pull request for **python-lxml** was committed:  https://github.com/Entware-ng/entware-oldpackages-ports/commit/f1111943f6a020f8dabf93766a993f22d2d5ad22 .   As a consequence, you no longer have to install the non-vanilla/custom lxml package: use the one in the Entware feed.
  

    
