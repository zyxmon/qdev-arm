# 
# Copyright (C) 2008 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#
# This Makefile is a skeleton
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libebml
PKG_VERSION:=1.3.0

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.bz2
PKG_SOURCE_URL:=http://dl.matroska.org/downloads/libebml
PKG_MD5SUM:=efec729bf5a51e649e1d9d1f61c0ae7a

include $(INCLUDE_DIR)/package.mk

define Package/libebml
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=libebml
  URL:=http://dl.matroska.org/downloads/libebml
endef

define Package/libebml/description
libEBML - low-level access to Matroska files
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/opt/include/ebml
	$(CP) $(PKG_BUILD_DIR)/ebml/* $(1)/opt/include/ebml
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_BUILD_DIR)/libebml.so* $(1)/opt/lib
	$(CP) $(PKG_BUILD_DIR)/libebml.a $(1)/opt/lib/
endef

BINARIES:= \
	Debug         EbmlDate     EbmlHead      EbmlString         EbmlVersion \
	EbmlBinary    EbmlDummy    EbmlMaster    EbmlSubHead        EbmlVoid       StdIOCallback \
	EbmlContexts  EbmlElement  EbmlSInteger  EbmlUInteger       IOCallback \
	EbmlCrc32     EbmlFloat    EbmlStream    EbmlUnicodeString  MemIOCallback


define Build/Compile
	for bin in $(BINARIES); \
	do \
		$(TARGET_CC) -fPIC -c $(TARGET_CFLAGS) -I $(PKG_BUILD_DIR) \
			-I $(STAGING_DIR)/opt/include/ -I $(PKG_BUILD_DIR)/ebml/ -L $(STAGING_DIR)/opt/lib/ \
			-o $(PKG_BUILD_DIR)/src/$$$${bin}.o $(PKG_BUILD_DIR)/src/$$$${bin}.cpp; \
	done
	$(TARGET_CC) -fPIC $(TARGET_CFLAGS) -I $(PKG_BUILD_DIR) \
		-I $(STAGING_DIR)/opt/include/ -I $(PKG_BUILD_DIR)/ebml/ -L $(STAGING_DIR)/opt/lib/ \
		-shared -Wl,-soname,libebml.so.4 -o $(PKG_BUILD_DIR)/libebml.so.4 \
		$(PKG_BUILD_DIR)/src/*.o
	$(AR) crv $(LD_FLAGS) $(PKG_BUILD_DIR)/libebml.a $(PKG_BUILD_DIR)/src/*.o
	$(TARGET_CROSS)ranlib $(PKG_BUILD_DIR)/libebml.a
	ln -sf libebml.so.4 $(PKG_BUILD_DIR)/libebml.so
endef


define Package/libebml/install
	$(INSTALL_DIR) $(1)/opt/lib
	$(CP) $(PKG_BUILD_DIR)/libebml.so* $(1)/opt/lib/
endef

$(eval $(call BuildPackage,libebml))
