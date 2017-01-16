# AirPrint
AirPrint emulation on Entware-ng with fewer hiccups

This intends to be a predictable, no-surprises, quick-starting, no-mess, no-fuss and relatively painless way to get AirPrint emulation working on an eligible Entware-ng equipped router or other device. I've tested it extensively on my TomatoUSB and MerlinWRT mipsel/mipselsf routers.  I have not tested it on ARM or other devices. SEE THE WIKI FOR DETAILS.

A main goal was to make AirPrint emulation work out-of-the-box.  The package set is not minimal, but rather displays all the features an end-user would see on say, Debian/Jessie.  If you don't want this wide a feature set, then modify it to your liking and roll your own.  For my part, I can only see one reason to install CUPS on a router:  AirPrint!  So, I set it up with no regard to size of the packages.  I want it to work right away, and not have to apply another set of patches, adjust, mess around, etc.

The modified files (and parent directories) are contained in the 'packages' and 'oldports'.  You should be able to drop the hplip, cups and python-lxml directly if you are going to build your own ipkg files.

NOTE:  Mind your own security with CUPS.  Read the fancy manual pages, know what security level is right for you, and implement it.

