#
# Copyright (C) 2007-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=aspell
PKG_VERSION:=0.60.6.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=ftp://ftp.gnu.org/gnu/aspell
PKG_MD5SUM:=e66a9c9af6a60dc46134fdacf6ce97d7

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/aspell
  SECTION:=utils
  CATEGORY:=Utilities
  TITLE:=Spell checker
  URL:=http://aspell.net/
  DEPENDS:=+libncursesw +libaspell
endef

define Package/libaspell
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Spell checker library
  URL:=http://aspell.net/
  DEPENDS:=+libstdcpp
endef

define Package/aspell/description
  GNU Aspell is a Free and Open Source spell checker designed to eventually replace Ispell.
  It can either be used as a library or as an independent spell checker.
  Its main feature is that it does a superior job of suggesting possible replacements
  for a misspelled word than just about any other spell checker out there for the English language.
endef

define Package/libaspell/description
  GNU Aspell library
endef


define Package/aspell/postinst
#!/bin/sh


echo -e "\n#####Available dictionaries at ftp://ftp.gnu.org/gnu/aspell/dict/0index.html \n\
Sample English dictionary install for aspell: \n\
     cd /Apps/opt/tmp \n\
     opkg install make \n\
     wget ftp://ftp.gnu.org/gnu/aspell/dict/en/aspell6-en-7.1-0.tar.bz2 \n\
     tar xvjf aspell6-en-7.1-0.tar.bz2 \n\
     cd aspell6-en-7.1-0 \n\
     ./configure \n\
     make \n\
     make install \n\
Note that some dictionaries require lot of memory for word compression."
endef

CONFIGURE_ARGS += \
	--disable-nls \
	--disable-static \
	--program-transform-name='' \

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include $(1)/opt/lib
	$(CP) $(PKG_INSTALL_DIR)/Apps/opt/include/* $(1)/opt/include/
	$(CP) $(PKG_INSTALL_DIR)/Apps/opt/lib/libpspell.{la,so*} $(1)/opt/lib/
	$(CP) $(PKG_INSTALL_DIR)/Apps/opt/lib/libaspell.{la,so*} $(1)/opt/lib/
endef

define Package/aspell/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(CP) $(PKG_INSTALL_DIR)/Apps/opt/bin/* $(1)/opt/bin/
	$(SED) 's,/bin/perl,/Apps/opt/bin/perl,g' $(1)/opt/bin/aspell-import
	$(INSTALL_DIR) $(1)/opt/etc
	$(CP) ./files/aspell.conf $(1)/opt/etc/
endef

define Package/libaspell/install
	$(INSTALL_DIR) $(1)/opt/lib/aspell-0.60
	$(CP) $(PKG_INSTALL_DIR)/Apps/opt/lib/*.so* $(1)/opt/lib/
	$(CP) $(PKG_INSTALL_DIR)/Apps/opt/lib/aspell-0.60/* $(1)/opt/lib/aspell-0.60
endef

$(eval $(call BuildPackage,aspell))
$(eval $(call BuildPackage,libaspell))
