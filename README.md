# AirPrint on Entware

###_**SEE THE WIKI (menu above) FOR HOW-TO SPECIFICS, DIRECTIONS, AND DETAILS.**_###

AirPrint emulation on Entware with fewer hiccups

This intends to be a predictable, no-surprises, quick-starting, no-mess, no-fuss and relatively painless way to get AirPrint emulation working on any capable Entware equipped router or other device. I've tested it extensively on my TomatoUSB and MerlinWRT mipsel/mipselsf routers.  I have not tested it on ARM or other devices. 

A main goal was to make AirPrint emulation work out-of-the-box.  The package set is probably the most minimal that will support Airprint out-of-the-box.   For my part, I can only see one reason to install CUPS on a router:  AirPrint!  I set it up with regard keeping the packages as small as possible.  I wanted it to work right away, and not have to compile another component, adjust, mess around, etc.

The modified files (and parent directories) are contained in the 'packages/libs', and 'rtndev'.  You should be able to drop the CUPS and cups-filters directories directly into the correct location in the OpenWRT Buildroot setup that Entware uses, if you are going to build your own ipkg files.  These four packages built correctly using the above-mentioned Buildroot system , cloned from Entware in April 2019.

NOTE:  Mind your own security with CUPS.  Read the fancy manual pages, know what security level is right for you, and implement it.

*Changes:*

  * 4/18/19 - Moved to Entware, away from Entware-ng.  At this point, only three non-vanilla ipk files need to be installed: cups, libcups and cups-filters.

  * 2/15/17 -  ARM7soft tarball was tested and works on Asus RT-AC68R/U [ FreshTomato (19.1) K26ARM USB AIO-64K ].  Note that due to some newer versions of CUPS being listed in the official feeds, certain "force-" options such as "--force-checksum" might have to be used to install the packaged items.  Worked for me, YMMV.
   
  * 1/24/17 -  ARM7soft tarball was added for newer Broadcom ARM routers, e.g. RT-AC1900. Not yet tested.
  
  * 1/20/17 - pull request for **hplip** was committed :  https://github.com/Entware-ng/entware-oldpackages-ports/commit/c5b2fd3751da6f4837c86275280f866940c7412c .  As a consequence, you no longer have to install the non-vanilla/custom hplip package: use the one in the Entware-ng feed. 
  
  * 1/9/17 - pull request for **python-lxml** was committed:  https://github.com/Entware-ng/entware-oldpackages-ports/commit/f1111943f6a020f8dabf93766a993f22d2d5ad22 .   As a consequence, you no longer have to install the non-vanilla/custom lxml package: use the one in the Entware-ng feed.
  

    
