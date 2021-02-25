#
# Copyright (C) 2021 Xaptum, Inc.
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=xaptum-tpm
PKG_VERSION:=1.0.1
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/xaptum/xaptum-tpm/tar.gz/v$(PKG_VERSION)?
PKG_HASH:=6bc58e8a674c9ba57d5da1b282d4a03ffb9b0d30a80164d759330979bad64655

PKG_MAINTAINER:=David R. Bild <david.bild@xaptum.com>
PKG_LICENSE:=Apache-2.0
PKG_LICENSE_FILES:=LICENSE

CMAKE_INSTALL:=1
CMAKE_BINARY_SUBDIR:=out/cmake
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/xaptum-tpm
  TITLE:=Xaptum TPM Utilities
  URL:=https://github.com/xaptum/xaptum-tpm
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS+= +tpm2-tss
endef

define Package/xaptum-tpm/description
  Utilities for interacting with the TPM2.0 used to access the Xaptum Edge Network Fabric, an IoT Network Solution.
endef

CMAKE_OPTIONS += -DBUILD_TESTING=OFF

define Build/InstallDev
	$(call Build/InstallDev/cmake,$(1))
	$(SED) 's,/usr/include,$$$${prefix}/include,g' $(1)/usr/lib/pkgconfig/xaptum-tpm.pc
	$(SED) 's,/usr/lib,$$$${prefix}/lib,g' $(1)/usr/lib/pkgconfig/xaptum-tpm.pc
endef

define Package/xaptum-tpm/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so.* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,xaptum-tpm))
