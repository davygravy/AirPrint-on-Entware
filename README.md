# AirPrint on Entware-ng

###_**SEE THE WIKI (menu above) FOR HOW-TO SPECIFICS, DIRECTIONS, AND DETAILS.**_###

AirPrint emulation on Entware-ng with fewer hiccups

This intends to be a predictable, no-surprises, quick-starting, no-mess, no-fuss and relatively painless way to get AirPrint emulation working on any capable Entware-ng equipped router or other device. I've tested it extensively on my TomatoUSB and MerlinWRT mipsel/mipselsf routers.  I have not tested it on ARM or other devices. 

A main goal was to make AirPrint emulation work out-of-the-box.  The package set is not minimal, but rather displays all the features an end-user would see on say, Debian/Jessie.  If you don't want this wide a feature set, then modify it to your liking and roll your own.  For my part, I can only see one reason to install CUPS on a router:  AirPrint!  So, I set it up with no regard to size of the packages.  I want it to work right away, and not have to apply another set of patches, adjust, mess around, etc.

The modified files (and parent directories) are contained in the 'packages', 'oldports' and 'rtndev'.  You should be able to drop the hplip, CUPS, cups-filters and python-lxml directories directly into the correct location in the OpenWRT Buildroot setup that Entware-ng uses, if you are going to build your own ipkg files.  These four packages built correctly using the above-mentioned Buildroot system , cloned from Entware-ng in January 2017.

NOTE:  Mind your own security with CUPS.  Read the fancy manual pages, know what security level is right for you, and implement it.

*Changes:*

  * 1/9/17 - pull request for **python-lxml** was committed:  https://github.com/Entware-ng/entware-oldpackages-ports/commit/f1111943f6a020f8dabf93766a993f22d2d5ad22 .   As a consequence, you no longer have to install the non-vanilla/custom lxml package: the one in the Entware-ng feed.

  * 1/20/17 - pull request for **hplip** was committed :  https://github.com/Entware-ng/entware-oldpackages-ports/commit/c5b2fd3751da6f4837c86275280f866940c7412c .  As a consequence, you no longer have to install the non-vanilla/custom hplip package: the one in the Entware-ng feed. 
  
  * 1/24/17 -  ARM7soft tarball was added for newer Broadcom ARM routers, e.g. RT-AC1900. Not yet tested.

  * 2/15/17 -  ARM7soft tarball was tested and works on Asus RT-AC68R/U [ Tomato v1.28.0000 -138 K26ARM USB AIO-64K ].  Note that due to some newer versions of CUPS being listed in the official feeds, certain "force-" options such as "--force-checksum" might have to be used to install the packaged items.  Worked for me, YMMV.
   
