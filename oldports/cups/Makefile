#
# Copyright (C) 2006-2012 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# v2.2.1 suffers from "'ppd_file_t' does not name a type" bug in depended packages

include $(TOPDIR)/rules.mk

PKG_NAME:=cups
PKG_VERSION:=2.1.4
PKG_RELEASE:=2

#PKG_BUILD_DEPENDS:=avahi 


PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION)-source.tar.gz
PKG_SOURCE_URL:=https://github.com/apple/cups/releases/download/release-$(PKG_VERSION)
PKG_MD5SUM:=9f9bf6e3b9c20a3519b4dc409666d6e7

include $(INCLUDE_DIR)/package.mk

define Package/cups/Default
  URL:=http://www.cups.org/
  SUBMENU:=Printing
endef

define Package/cups
$(call Package/cups/Default)
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libcups +libcupsmime +libcupscgi +libcupsppdc +libcupsimage +libusb-1.0
  TITLE:=Common UNIX Printing System (daemon)
endef

define Package/cups/description
	Common UNIX Printing System (daemon)
endef

define Package/cups/conffiles
/opt/etc/cups/classes.conf
/opt/etc/cups/cupsd.conf
/opt/etc/cups/printers.conf
/opt/etc/cups/cups-files.conf
endef

define Package/cups-bsd
$(call Package/cups/Default)
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libcups
  TITLE:=Common UNIX Printing System - BSD commands (old)
endef

define Package/cups-bsd/description
	Common UNIX Printing System - BSD commands (old)
endef

define Package/cups-client
$(call Package/cups/Default)
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libcups +libcupsimage +libcupsmime
  TITLE:=Common UNIX Printing System - Client commands
endef

define Package/cups-client/conffiles
/opt/etc/cups/client.conf
endef

define Package/cups-client/description
	Common UNIX Printing System - Client commands
endef

define Package/cups-ppdc
$(call Package/cups/Default)
  SECTION:=net
  CATEGORY:=Network
  DEPENDS:=+libcupsppdc
  TITLE:=Common UNIX Printing System - PPDC utils
endef

define Package/cups-ppdc/description
	Common UNIX Printing System - PPDC utils
endef

define Package/libcups
$(call Package/cups/Default)
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+zlib +libpthread +libpng +libjpeg +libavahi-client
  TITLE:=Common UNIX Printing System - Core library
endef

define Package/libcups/description
	Common UNIX Printing System - Core library
endef

define Package/libcupscgi
$(call Package/cups/Default)
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+libcups
  TITLE:=Common UNIX Printing System - CGI library
endef

define Package/libcupscgi/description
	Common UNIX Printing System - CGI library
endef

define Package/libcupsimage
$(call Package/cups/Default)
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+libcups +libpng +libjpeg
  TITLE:=Common UNIX Printing System - Image library
endef

define Package/libcupsimage/description
	Common UNIX Printing System - Image library
endef

define Package/libcupsmime
$(call Package/cups/Default)
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+libcups
  TITLE:=Common UNIX Printing System - MIME library
endef

define Package/libcupsmime/description
	Common UNIX Printing System - MIME library
endef

define Package/libcupsppdc
$(call Package/cups/Default)
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+libcups +libstdcpp
  TITLE:=Common UNIX Printing System - PPDC library
endef

define Package/libcupsppdc/description
	Common UNIX Printing System - PPDC library
endef

define Package/cups-locales
$(call Package/cups/Default)
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Common UNIX Printing System - Locales
endef

define Package/cups-locales/description
	Common UNIX Printing System - Locales
endef

define Build/Configure
	$(call Build/Configure/Default, \
		--with-cups-user="nobody" \
		--with-cups-group="nogroup" \
		--with-components="embedded" \
		--without-java \
		--without-perl \
		--without-python \
		--without-php \
		--enable-shared \
		--enable-libusb \
		--disable-dbus \
		--enable-avahi \
		--enable-dnssd \
		--disable-launchd \
		--disable-systemd \
		--disable-pam \
		--disable-gnutls \
		--disable-cdsassl \
		--disable-ssl \
		--disable-gssapi \
		--disable-acl \
		UNAME="Linux" \
		LIBS="$(TARGET_LDFLAGS) -lz -lpng -ljpeg -lssp" \
	)
endef

define Build/Compile
	$(MAKE) -C $(PKG_BUILD_DIR) \
		$(TARGET_CONFIGURE_OPTS) \
		DSTROOT="$(PKG_INSTALL_DIR)" \
		STRIP="/bin/true" \
		all install
endef

define Package/cups/install
	rm -rf $(1)/opt/etc/cups
	$(INSTALL_DIR) $(1)/opt/etc/cups
	$(CP) $(PKG_INSTALL_DIR)/opt/etc/cups/* $(1)/opt/etc/cups/
	rm -rf $(1)/opt/etc/cups/certs
	ln -sf /opt/tmp $(1)/opt/etc/cups/certs
	rm -f $(1)/opt/bin/cups-config
	$(INSTALL_DIR) $(1)/opt/lib/cups
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/cups/backend $(1)/opt/lib/cups
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/cups/cgi-bin $(1)/opt/lib/cups
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/cups/daemon $(1)/opt/lib/cups
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/cups/driver $(1)/opt/lib/cups
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/cups/monitor $(1)/opt/lib/cups
	$(INSTALL_DIR) $(1)/opt/lib/cups
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/cups/filter \
		$(1)/opt/lib/cups/
	$(INSTALL_DIR) $(1)/opt/share/cups
	$(CP) $(PKG_INSTALL_DIR)/opt/share/cups/templates \
		$(1)/opt/share/cups/
		
	$(INSTALL_DIR) $(1)/opt/share/cups/mime
	$(CP) $(PKG_INSTALL_DIR)/opt/share/cups/mime/* $(1)/opt/share/cups/mime/
	
	$(INSTALL_DIR) $(1)/opt/share/doc/cups
	$(CP) $(PKG_INSTALL_DIR)/opt/share/doc/cups/* $(1)/opt/share/doc/cups/
	
	$(INSTALL_DIR) $(1)/opt/share/cups/ipptool
	$(CP) $(PKG_INSTALL_DIR)/opt/share/cups/ipptool/* $(1)/opt/share/cups/ipptool/
	
	$(INSTALL_DIR) $(1)/opt/share/cups/ppdc
	$(CP) $(PKG_INSTALL_DIR)/opt/share/cups/ppdc/* $(1)/opt/share/cups/ppdc/

	$(INSTALL_DIR) $(1)/opt/sbin
	# overwrite default config files with our own
	$(CP) ./files/etc/cups/* $(1)/opt/etc/cups/
	$(INSTALL_DIR) $(1)/opt/etc/init.d
	$(INSTALL_BIN) ./files/S60cupsd $(1)/opt/etc/init.d/
	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/opt/sbin/{cupsctl,cupsd} \
		$(1)/opt/sbin/
	# needed for cups to find usb printers per http://wiki.openwrt.org/doc/howto/cups.server
	chmod 700 $(1)/opt/lib/cups/backend/usb
	$(INSTALL_DIR) $(1)/opt/share/cups/{data,drv,ipptool,ppdc,usb}
	$(CP) $(PKG_INSTALL_DIR)/opt/share/cups/usb/* $(1)/opt/share/cups/usb/

	$(INSTALL_DIR) $(1)/opt/var/{cache,log,run}/cups
	$(INSTALL_DIR) $(1)/opt/var/spool/cups/tmp
endef

define Package/cups-bsd/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/{lprm,lpq,lpr} $(1)/opt/bin/
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/sbin/lpc $(1)/opt/sbin/
endef

define Package/cups-client/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/opt/bin/{lp,cancel,cupstestppd,cupstestdsc} \
		$(PKG_INSTALL_DIR)/opt/bin/{ipptool,ippfind,lpoptions,lpstat} \
		$(1)/opt/bin/
	$(INSTALL_DIR) $(1)/opt/sbin
	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/opt/sbin/{cupsaccept,cupsaddsmb,cupsfilter} \
		$(PKG_INSTALL_DIR)/opt/sbin/{lpadmin,lpinfo,lpmove} \
		$(1)/opt/sbin/
	(cd $(1)/opt/sbin; ln -sf cupsaccept accept; ln -sf cupsaccept cupsenable; ln -sf cupsaccept cupsdisable; ln -sf cupsaccept reject; ln -sf cupsaccept cupsreject;)
endef

define Package/cups-ppdc/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/opt/bin/{ppdc,ppdhtml,ppdi,ppdmerge,ppdpo} \
		$(1)/opt/bin/
endef

define Package/libcups/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libcups.so* $(1)/opt/lib/
endef

define Package/libcupscgi/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libcupscgi.so* $(1)/opt/lib/
endef

define Package/libcupsimage/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libcupsimage.so* $(1)/opt/lib/
endef

define Package/libcupsmime/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libcupsmime.so* $(1)/opt/lib/
endef

define Package/libcupsppdc/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libcupsppdc.so* $(1)/opt/lib/
endef

define Package/cups-locales/install
	$(INSTALL_DIR) $(1)/opt/share
	$(CP) $(PKG_INSTALL_DIR)/opt/share/locale $(1)/opt/share/
endef

define Build/InstallDev
	$(INSTALL_DIR) $(2)/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/opt/bin/cups-config $(2)/bin/
	$(INSTALL_DIR) $(1)/opt/include
	$(CP) $(PKG_INSTALL_DIR)/opt/include/cups $(1)/opt/include/
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/libcups*.so* $(1)/opt/lib/
endef

$(eval $(call BuildPackage,cups))
$(eval $(call BuildPackage,libcups))
$(eval $(call BuildPackage,libcupscgi))
$(eval $(call BuildPackage,libcupsimage))
$(eval $(call BuildPackage,libcupsmime))
$(eval $(call BuildPackage,libcupsppdc))
$(eval $(call BuildPackage,cups-bsd))
$(eval $(call BuildPackage,cups-client))
$(eval $(call BuildPackage,cups-ppdc))
$(eval $(call BuildPackage,cups-locales))
