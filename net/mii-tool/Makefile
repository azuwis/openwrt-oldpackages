#
# Copyright (C) 2006-2010 OpenWrt.org
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=mii-tool
PKG_VERSION:=2016-02-15
PKG_RELEASE:=1

PKG_SOURCE_PROTO:=git
PKG_SOURCE_URL:=git://git.code.sf.net/p/net-tools/code
PKG_SOURCE_SUBDIR:=$(PKG_NAME)-$(PKG_VERSION)
PKG_SOURCE_VERSION:=bd8bceaed2311651710331a7f8990c3e31be9840
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz

include $(INCLUDE_DIR)/package.mk

define Package/mii-tool
  SECTION:=net
  CATEGORY:=Network
  TITLE:=configure media type using MII commands
  URL:=http://freshmeat.net/projects/mii-tool/
endef

define Package/mii-tool/description
	The mii-tool command allows you to set or autodetect the media type
	or mii chipset-based ethernet devices. It traditionally had been
	distributed in the net-tools package. This is a single distribution
	optimized for embedded systems and fully automated cross/-sysroot-builds
endef

define Build/Configure
	# Failed configure.sh leaves stub config.h around.
	rm -f $(PKG_BUILD_DIR)/config.h
	(cd $(PKG_BUILD_DIR) && yes $$$$'\n' | ./configure.sh config.in )
endef

define Build/Compile
	$(call Build/Compile/Default,mii-tool)
endef

define Package/mii-tool/install
	$(INSTALL_DIR) $(1)/usr/sbin
	$(CP) $(PKG_BUILD_DIR)/mii-tool $(1)/usr/sbin/
endef

$(eval $(call BuildPackage,mii-tool))
