# 
# Copyright (C) 2008 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# This Makefile is a skeleton
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libmatroska
PKG_VERSION:=1.4.1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=http://dl.matroska.org/downloads/libmatroska
PKG_MD5SUM:=f61b2e5086f4bb9d24a43cc8af43a719

include $(INCLUDE_DIR)/package.mk

define Package/libmatroska
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS:=+libebml
  TITLE:=libmatroska
  URL:=http://dl.matroska.org/downloads/libmatroska
endef

define Package/libmatroska/description
lbmatroska - low-level access to Matroska files
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include/matroska
	$(CP) $(PKG_BUILD_DIR)/matroska/* $(1)/opt/include/matroska
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_BUILD_DIR)/libmatroska.so* $(1)/opt/lib
	$(CP) $(PKG_BUILD_DIR)/libmatroska.a $(1)/opt/lib/
endef

BINARIES:= \
	FileKax KaxAttached KaxAttachments KaxBlock KaxBlockData KaxCluster KaxContexts \
	KaxCues KaxCuesData KaxInfoData KaxSeekHead KaxSegment KaxSemantic KaxTracks KaxVersion


define Build/Compile
	for bin in $(BINARIES); \
	do \
		$(TARGET_CC) -fPIC -c $(TARGET_CFLAGS) -I $(PKG_BUILD_DIR) -I $(STAGING_DIR)/opt/include/ebml \
			-I $(STAGING_DIR)/opt/include/ -I $(PKG_BUILD_DIR)/matroska/ -L $(STAGING_DIR)/lib/ \
			-o $(PKG_BUILD_DIR)/src/$$$${bin}.o $(PKG_BUILD_DIR)/src/$$$${bin}.cpp; \
	done
	$(TARGET_CC) -fPIC $(TARGET_CFLAGS) -I $(PKG_BUILD_DIR) -I $(STAGING_DIR)/opt/include/ \
		-I $(PKG_BUILD_DIR)/matroska/ -L $(STAGING_DIR)/opt/lib/ \
		-lebml -shared -Wl,-soname,libmatroska.so.6 -o $(PKG_BUILD_DIR)/libmatroska.so.6 \
		$(PKG_BUILD_DIR)/src/*.o
	$(AR) crv $(LD_FLAGS) $(PKG_BUILD_DIR)/libmatroska.a $(PKG_BUILD_DIR)/src/*.o
	$(TARGET_CROSS)ranlib $(PKG_BUILD_DIR)/libmatroska.a
	ln -sf libmatroska.so.6 $(PKG_BUILD_DIR)/libmatroska.so
endef


define Package/libmatroska/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_BUILD_DIR)/libmatroska.so* $(1)/opt/lib/
endef

$(eval $(call BuildPackage,libmatroska))
