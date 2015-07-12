#
# Copyright (C) 2007-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=dos2unix
PKG_VERSION:=7.2.3
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://waterlan.home.xs4all.nl/dos2unix
PKG_MD5SUM:=b4cd9540de21148555ee690cbb9b1bb7


include $(INCLUDE_DIR)/package.mk

define Package/dos2unix
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=DOS/Mac to Unix and vice versa text file format converter
  URL:=http://waterlan.home.xs4all.nl/dos2unix.html
endef

define Package/dos2unix/description
  DOS/Mac to Unix and vice versa text file format converter
endef



define Build/Compile
	(cd $(PKG_BUILD_DIR); $(TARGET_CC) $(TARGET_CFLAGS) $(TARGET_CPPFLAGS) $(TARGET_LDFLAGS) -DVER_REVISION=\"7.2.3\" -DVER_DATE=\"2015-07-01\" -DVER_AUTHOR='Erwin Waterlander' -o dos2unix dos2unix.c querycp.c common.c)
	(cd $(PKG_BUILD_DIR); $(TARGET_CC) $(TARGET_CFLAGS) $(TARGET_CPPFLAGS) $(TARGET_LDFLAGS) -DVER_REVISION=\"7.2.3\" -DVER_DATE=\"2015-07-01\" -DVER_AUTHOR='Erwin Waterlander' -o unix2dos unix2dos.c querycp.c common.c)
endef


define Package/dos2unix/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(CP) $(PKG_BUILD_DIR)/dos2unix $(1)/opt/bin/
	$(CP) $(PKG_BUILD_DIR)/unix2dos $(1)/opt/bin/
endef

$(eval $(call BuildPackage,dos2unix))
