#
# Copyright (C) 2021 Xaptum, Inc.
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=enftun
PKG_VERSION:=0.8.3
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/xaptum/enftun/tar.gz/v$(PKG_VERSION)?
PKG_HASH:=4f45e1a2b7c585154a496d46ac6e8e5bcc52739eac69d46faca013d9cbab7bc5

PKG_MAINTAINER:=David R. Bild <david.bild@xaptum.com>
PKG_LICENSE:=Apache-2.0
PKG_LICENSE_FILES:=LICENSE

CMAKE_INSTALL:=1
CMAKE_BINARY_SUBDIR:=out/cmake
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/enftun
  TITLE:=enftun
  URL:=https://github.com/xaptum/enftun
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=VPN
  DEPENDS+= +libconfig +libuv +libopenssl +kmod-tun +bash +ip-full
  DEPENDS+= +ENFTUN_TPM_SUPPORT:xaptum-tpm +ENFTUN_TPM_SUPPORT:tpm2-tss +ENFTUN_TPM_SUPPORT:tpm2-tss-engine
  DEPENDS+= +ENFTUN_XTT_SUPPORT:libsodium +ENFTUN_XTT_SUPPORT:xtt
  DEPENDS+= +ENFTUN_KEYGEN_SUPPORT:libcurl +ENFTUN_KEYGEN_SUPPORT:jansson
endef

define Package/enftun/description
  Client to connect to the Xaptum ENF, a secure IPv6 overlay network for IoT.
endef

define Package/enftun/config
	source "$(SOURCE)/Config.in"
endef

CMAKE_OPTIONS += -DBUILD_KEYGEN=$(if $(CONFIG_ENFTUN_KEYGEN_SUPPORT),ON,OFF)
CMAKE_OPTIONS += -DBUILD_TPM=$(if $(CONFIG_ENFTUN_TPM_SUPPORT),ON,OFF)
CMAKE_OPTIONS += -DBUILD_XTT=$(if $(CONFIG_ENFTUN_XTT_SUPPORT),ON,OFF)

CMAKE_OPTIONS += -DBUILD_TEST=OFF
CMAKE_OPTIONS += -DBUILD_SYSTEMD=OFF

define Package/enftun/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin/

	$(INSTALL_DIR) $(1)/usr/share/doc/enftun
	$(CP) $(PKG_INSTALL_DIR)/usr/share/doc/enftun/* $(1)/usr/share/doc/enftun

	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/enftun.init $(1)/etc/init.d/enftun

	$(INSTALL_DIR) $(1)/etc/enftun
	$(CP) $(PKG_INSTALL_DIR)/usr/etc/enftun/* $(1)/etc/enftun
endef

$(eval $(call BuildPackage,enftun))
