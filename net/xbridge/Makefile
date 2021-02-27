#
# Copyright (C) 2021 Xaptum, Inc.
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=xbridge
PKG_VERSION:=0908798ad34fed2ed0d9d92cf86574e53699ca65
PKG_RELEASE:=1

PKG_SOURCE:=xaprc-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/xaptum/xaprc/tar.gz/$(PKG_VERSION)?
PKG_HASH:=0f57180b3189ffa802e5942cdb9c642ee6cf5f5e5f34e118291ef9d15409585e
PKG_BUILD_DIR:=$(BUILD_DIR)/xbridge-$(PKG_VERSION)/xbridge

PKG_MAINTAINER:=David R. Bild <david.bild@xaptum.com>
PKG_LICENSE:=Apache-2.0
PKG_LICENSE_FILES:=LICENSE

CMAKE_INSTALL:=1
CMAKE_BINARY_SUBDIR:=out/cmake
PKG_BUILD_PARALLEL:=1

TAR_OPTIONS:=--strip-components 1 $(TAR_OPTIONS)

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/xbridge
  TITLE:=xbridge
  URL:=https://github.com/xaptum/xaprc
  SECTION:=net
  CATEGORY:=Network
  DEPENDS+= +libpcap
endef

define Package/xbridge/description
  A userspace application to bridge two network interfaces.
endef

define Package/xbridge/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin/

	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/xbridge.init $(1)/etc/init.d/xbridge
endef

$(eval $(call BuildPackage,xbridge))
