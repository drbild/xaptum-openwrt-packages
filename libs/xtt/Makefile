#
# Copyright (C) 2021 Xaptum, Inc.
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=xtt
PKG_VERSION:=0.12.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/xaptum/xtt/tar.gz/v$(PKG_VERSION)?
PKG_HASH:=13896ed5c01fd46a764eee7b0e1db0a5a7183d8eb4e8ce7c277ecc7581936745

PKG_MAINTAINER:=David R. Bild <david.bild@xaptum.com>
PKG_LICENSE:=Apache-2.0
PKG_LICENSE_FILES:=LICENSE

CMAKE_INSTALL:=1
CMAKE_BINARY_SUBDIR:=out/cmake
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/xtt
  TITLE:=xtt
  URL:=https://github.com/xaptum/xtt
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS+= +libsodium +amcl +ecdaa +XTT_TPM_SUPPORT:tpm2-tss +XTT_TPM_SUPPORT:xaptum-tpm
endef

define Package/xtt/description
  A C implementation of the Trusted Transit protocol for securing Internet of Things (IoT) network traffic.
endef

define Package/xtt/config
	select AMCL_CURVE_NIST256
	select ECDAA_CURVE_FP256BN

	source "$(SOURCE)/Config.in"
endef

CMAKE_OPTIONS += -DBUILD_TESTING=OFF
CMAKE_OPTIONS += -DUSE_TPM=$(if $(CONFIG_XTT_TPM_SUPPORT),ON,OFF)
CMAKE_OPTIONS += -DBUILD_TOOL=$(if $(CONFIG_XTT_TOOL),ON,OFF)

define Build/InstallDev
	$(call Build/InstallDev/cmake,$(1))
	$(SED) 's,/usr/include,$$$${prefix}/include,g' $(1)/usr/lib/pkgconfig/xtt.pc
	$(SED) 's,/usr/lib,$$$${prefix}/lib,g' $(1)/usr/lib/pkgconfig/xtt.pc
endef

define Package/xtt/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so.* $(1)/usr/lib/

ifeq ($(CONFIG_XTT_TOOL),y)
	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin/
endif
endef

$(eval $(call BuildPackage,xtt))
