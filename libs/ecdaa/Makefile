#
# Copyright (C) 2021 Xaptum, Inc.
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=ecdaa
PKG_VERSION:=1.0.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/xaptum/ecdaa/tar.gz/v$(PKG_VERSION)?
PKG_HASH:=1e0bb0de74eb88e3f3b6209c603ae34f24fbe7760f83f1295491e9ec786b7ea6

PKG_MAINTAINER:=David R. Bild <david.bild@xaptum.com>
PKG_LICENSE:=Apache-2.0
PKG_LICENSE_FILES:=LICENSE

CMAKE_INSTALL:=1
CMAKE_BINARY_SUBDIR:=out/cmake
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/ecdaa
  TITLE:=ecdaa
  URL:=https://github.com/xaptum/ecdaa
  SECTION:=libs
  CATEGORY:=Libraries
  DEPENDS+= +amcl +ECDAA_TPM_SUPPORT:xaptum-tpm
endef

define Package/ecdaa/description
  A C implementation of elliptic-curve-based Direct Anonymous Attestation (DAA) signatures.
endef

define Package/ecdaa/config
	source "$(SOURCE)/Config.in"
endef

CMAKE_OPTIONS += -DWORD_SIZE=$(if $(CONFIG_ARCH_64BIT),64,32)

ECDAA_CURVES += $(if $(CONFIG_ECDAA_CURVE_BLS383),BLS383,)
ECDAA_CURVES += $(if $(CONFIG_ECDAA_CURVE_BN254),BN254,)
ECDAA_CURVES += $(if $(CONFIG_ECDAA_CURVE_BN254CX),BN254CX,)
ECDAA_CURVES += $(if $(CONFIG_ECDAA_CURVE_FP256BN),FP256BN,)
ECDAA_CURVES_COMMASEPARATED += $(subst $(space),$(comma),$(strip $(ECDAA_CURVES)))

CMAKE_OPTIONS += -DECDAA_CURVES=$(ECDAA_CURVES_COMMASEPARATED)
CMAKE_OPTIONS += -DECDAA_TPM_SUPPORT=$(if $(CONFIG_ECDAA_TPM_SUPPORT),ON,OFF)
CMAKE_OPTIONS += -DBUILD_BENCHMARKS=$(if $(CONFIG_ECDAA_BENCHMARKS),ON,OFF)
CMAKE_OPTIONS += -DBUILD_TOOL=$(if $(CONFIG_ECDAA_TOOL),ON,OFF)

define Build/InstallDev
	$(call Build/InstallDev/cmake,$(1))
	$(SED) 's,/usr/include,$$$${prefix}/include,g' $(1)/usr/lib/pkgconfig/ecdaa.pc
	$(SED) 's,/usr/lib,$$$${prefix}/lib,g' $(1)/usr/lib/pkgconfig/ecdaa.pc
endef

define Package/ecdaa/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/*.so.* $(1)/usr/lib/

	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin/
endef

$(eval $(call BuildPackage,ecdaa))
