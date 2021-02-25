#
# Copyright (C) 2021 Xaptum, Inc.
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=tpm2-tss
PKG_VERSION:=3.0.3
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/tpm2-software/tpm2-tss/releases/download/$(PKG_VERSION)
PKG_HASH:=78392be7309baf47f51b122f566ac915fd4d1760ea78571cba2e1484f9b5be17

PKG_MAINTAINER:=David R. Bild <david.bild@xaptum.com>
PKG_LICENSE:=BSD-2-Clause
PKG_LICENSE_FILES:=LICENSE

PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/tpm2-tss
  TITLE:=TPM2-TSS
  URL:=https://github.com/tpm2-software/tpm2-tss
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=TPM2
  DEPENDS+= +libcurl +libjson-c +libopenssl
endef

TARGET_CFLAGS:= -U_FORTIFY_SOURCE $(TARGET_OPTIMIZATION)$(if $(CONFIG_DEBUG), -g3) $(EXTRA_OPTIMIZATION)

define Package/tpm2-tss/description
OSS implementation of the TCG TPM2 Software Stack (TSS2)
endef

define Package/tpm2-tss/install
	$(INSTALL_DIR) $(1)/usr/lib
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/lib/libtss2*.so* $(1)/usr/lib/
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_BUILD_DIR)/include/tss2 $(1)/usr/include/

	$(INSTALL_DIR) $(1)/usr/lib
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/libtss2*.so* $(1)/usr/lib/

	$(INSTALL_DIR) $(1)/usr/lib/pkgconfig/
	$(CP) $(PKG_BUILD_DIR)/lib/*.pc $(1)/usr/lib/pkgconfig/
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
