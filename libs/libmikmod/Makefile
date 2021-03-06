#
# Copyright (C) 2010-2011 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=libmikmod
PKG_VERSION:=3.3.7
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=http://prdownloads.sourceforge.net/mikmod
PKG_MD5SUM:=bc6bea190cb8d2ce2b105cc0ff811681

PKG_FIXUP:=autoreconf
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/libmikmod
  SECTION:=libs
  CATEGORY:=Libraries
  TITLE:=Mikmod sound library
  URL:=http://mikmod.raphnet.net/
  DEPENDS:=+alsa-lib +libpthread
endef

define Package/libmikmod/description
  Mikmod is a library supporting many formats, including mod, s3m, it, and xm.
endef

define Build/Configure
	$(call Build/Configure/Default, \
		--disable-af \
		--enable-alsa \
		--disable-oss \
		--disable-esd \
		--disable-sam9407 \
		--disable-ultra \
		--enable-dl \
		--disable-debug \
		--enable-threads \
	)
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include $(1)/usr/lib
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/include/mikmod.h \
		$(1)/usr/include/
	$(CP) \
		$(PKG_INSTALL_DIR)/usr/lib/libmikmod.{a,la,so*} \
		$(1)/usr/lib/

	$(INSTALL_DIR) $(2)/bin
	$(INSTALL_BIN) \
		$(PKG_INSTALL_DIR)/usr/bin/libmikmod-config \
		$(2)/bin

	$(SED) 's,^\(exec_prefix\|prefix\)=.*,\1=\"$(STAGING_DIR)/usr/\",g' \
		$(2)/bin/libmikmod-config

	$(INSTALL_DIR) $(1)/usr/share/aclocal
	$(INSTALL_DATA) \
		$(PKG_INSTALL_DIR)/usr/share/aclocal/* \
		$(1)/usr/share/aclocal/
endef

define Package/libmikmod/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libmikmod.so* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,libmikmod))
