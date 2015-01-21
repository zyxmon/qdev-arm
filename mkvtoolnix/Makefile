#
# Copyright (C) 2010-2014 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=mkvtoolnix
PKG_VERSION:=4.2.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=http://bunkus.org/videotools/mkvtoolnix/sources
PKG_MD5SUM:=de3e99598d47d0a2226269f79faabbfd


PKG_FIXUP:=autoreconf

#include $(INCLUDE_DIR)/uclibc++.mk
include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/nls.mk

define Package/mkvtoolnix
  SECTION:=multimedia
  CATEGORY:=Multimedia
  TITLE:=MKVToolNix -- Cross-platform tools for Matroska
  URL:=https://www.bunkus.org/videotools/mkvtoolnix/
  DEPENDS:= +libpthread +boost-regex +boost-system +boost-filesystem \
  	+libexpat +libmagic +libflac +libogg +libvorbis +zlib +liblzo +libbz2 \
  	+libebml +libmatroska \
  	$(ICONV_DEPENDS) $(INTL_DEPENDS)
endef

define Package/mkvtoolnix/description
A set of tools to create, alter and inspect Matroska files
endef

TARGET_LDFLAGS += \
	-lstdc++ -lintl \

CONFIGURE_ARGS +=\
	--with-boost=$(STAGING_DIR)/opt \


define Package/mkvtoolnix/install
	$(INSTALL_DIR) $(1)/opt/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/src/mkv* $(1)/opt/bin/
endef

$(eval $(call BuildPackage,mkvtoolnix))
