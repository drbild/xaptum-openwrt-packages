#
# Copyright (C) 2021 Xaptum, Inc.
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=amcl
PKG_VERSION:=4.7.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://codeload.github.com/xaptum/amcl/tar.gz/$(PKG_VERSION)?
PKG_HASH:=0b1641d6830858a3885195b08cf2aeb1a149718a3d570a9d3e3fb196be319221

PKG_MAINTAINER:=David R. Bild <david.bild@xaptum.com>
PKG_LICENSE:=Apache-2.0
PKG_LICENSE_FILES:=LICENSE

CMAKE_INSTALL:=1
CMAKE_BINARY_SUBDIR:=out/cmake
PKG_BUILD_PARALLEL:=1

include $(INCLUDE_DIR)/package.mk
include $(INCLUDE_DIR)/cmake.mk

define Package/amcl
  TITLE:=Apache Milagro Crypto Library
  URL:=https://github.com/xaptum/amcl
  SECTION:=libs
  CATEGORY:=Libraries
endef

define Package/amcl/description
  AMCL is a standards compliant C cryptographic library with no external dependencies, specifically designed to support the Internet of Things (IoT).
endef

define Package/amcl/config
	source "$(SOURCE)/Config.in"
endef

CMAKE_OPTIONS += -DAMCL_INCLUDE_SUBDIR=amcl
CMAKE_OPTIONS += -DBUILD_BENCHMARKS=OFF
CMAKE_OPTIONS += -DWORD_SIZE=$(if $(CONFIG_ARCH_64BIT),64,32)

AMCL_CURVE += $(if $(CONFIG_AMCL_CURVE_ANSSI),ANSSI,)
AMCL_CURVE += $(if $(CONFIG_AMCL_CURVE_BLS383),BLS383,)
AMCL_CURVE += $(if $(CONFIG_AMCL_CURVE_BLS461),BLS461,)
AMCL_CURVE += $(if $(CONFIG_AMCL_CURVE_BN254),BN254,)
AMCL_CURVE += $(if $(CONFIG_AMCL_CURVE_BN254CX),BN254CX,)
AMCL_CURVE += $(if $(CONFIG_AMCL_CURVE_BRAINPOOL),BRAINPOOL,)
AMCL_CURVE += $(if $(CONFIG_AMCL_CURVE_C25519),C25519,)
AMCL_CURVE += $(if $(CONFIG_AMCL_CURVE_C41417),C41417,)
AMCL_CURVE += $(if $(CONFIG_AMCL_CURVE_ED25519),ED25519,)
AMCL_CURVE += $(if $(CONFIG_AMCL_CURVE_FP256BN),FP256BN,)
AMCL_CURVE += $(if $(CONFIG_AMCL_CURVE_FP512BN),FP512BN,)
AMCL_CURVE += $(if $(CONFIG_AMCL_CURVE_GOLDILOCKS),GOLDILOCKS,)
AMCL_CURVE += $(if $(CONFIG_AMCL_CURVE_HIFIVE),HIFIVE,)
AMCL_CURVE += $(if $(CONFIG_AMCL_CURVE_NIST256),NIST256,)
AMCL_CURVE += $(if $(CONFIG_AMCL_CURVE_NIST384),NIST384,)
AMCL_CURVE += $(if $(CONFIG_AMCL_CURVE_NIST521),NIST521,)
AMCL_CURVE += $(if $(CONFIG_AMCL_CURVE_NUMS256E),NUMS256E,)
AMCL_CURVE += $(if $(CONFIG_AMCL_CURVE_NUMS256W),NUMS256W,)
AMCL_CURVE += $(if $(CONFIG_AMCL_CURVE_NUMS384E),NUMS384E,)
AMCL_CURVE += $(if $(CONFIG_AMCL_CURVE_NUMS384W),NUMS384W,)
AMCL_CURVE += $(if $(CONFIG_AMCL_CURVE_NUMS512E),NUMS512E,)
AMCL_CURVE += $(if $(CONFIG_AMCL_CURVE_NUMS512W),NUMS512W,)

AMCL_CURVE_COMMASEPARATED += $(subst $(space),$(comma),$(strip $(AMCL_CURVE)))
CMAKE_OPTIONS += -DAMCL_CURVE=$(AMCL_CURVE_COMMASEPARATED)

AMCL_RSA += $(if $(CONFIG_AMCL_RSA_2048),2048,)
AMCL_RSA += $(if $(CONFIG_AMCL_RSA_3072),3072,)
AMCL_RSA += $(if $(CONFIG_AMCL_RSA_4096),4096,)

AMCL_RSA_COMMASEPARATED += $(subst $(space),$(comma),$(strip $(AMCL_RSA)))
CMAKE_OPTIONS += -DAMCL_RSA=$(AMCL_RSA_COMMASEPARATED)

CMAKE_OPTIONS += -DBUILD_MPIN=$(if $(CONFIG_AMCL_MPIN),ON,OFF)
ifeq ($(CONFIG_AMCL_MPIN),y)
	CMAKE_OPTIONS += -DAMCL_MAXPIN=$(CONFIG_AMCL_MPIN_MAXPIN)
	CMAKE_OPTIONS += -DAMCL_PBLEN=$(CONFIG_AMCL_MPIN_PBLEN)
endif

define Build/InstallDev
	$(call Build/InstallDev/cmake,$(1))
	$(SED) 's,/usr/include,$$$${prefix}/include,g' $(1)/usr/lib/pkgconfig/amcl.pc
	$(SED) 's,/usr/lib,$$$${prefix}/lib,g' $(1)/usr/lib/pkgconfig/amcl.pc
endef

define Package/amcl/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libamcl_*.so.* $(1)/usr/lib/
endef

$(eval $(call BuildPackage,amcl))
