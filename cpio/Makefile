#
# Copyright (C) 2007-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=cpio
PKG_VERSION:=2.11
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://ftp.gnu.org/gnu/cpio
PKG_MD5SUM:=1112bb6c45863468b5496ba128792f6c

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/cpio
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=GNU cpio, a program to manage archives of files
  URL:=http://ftp.gnu.org/gnu/cpio/
endef

define Package/cpio/description
  GNU cpio, a program to manage archives of files
endef



define Package/cpio/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(CP) $(PKG_INSTALL_DIR)/opt/bin/* $(1)/opt/bin/
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/opt/lib/* $(1)/opt/lib/
endef

$(eval $(call BuildPackage,cpio))
