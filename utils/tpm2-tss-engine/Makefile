#
# Copyright (C) 2021 Xaptum, Inc.
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=tpm2-tss-engine
PKG_VERSION:=1.1.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/tpm2-software/tpm2-tss-engine/releases/download/v$(PKG_VERSION)
PKG_HASH:=ea2941695ac221d23a7f3e1321140e75b1495ae6ade876f2f4c2ed807c65e2a5

PKG_MAINTAINER:=David R. Bild <david.bild@xaptum.com>
PKG_LICENSE:=BSD-2-Clause
PKG_LICENSE_FILES:=LICENSE

PKG_FIXUP:=autoreconf
PKG_BUILD_DEPENDS:= m4
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

CONFIGURE_ARGS += --with-enginesdir=/usr/lib/engines-1.1

define Package/tpm2-tss-engine
  TITLE:=TPM2-TSS-Engine
  URL:=https://github.com/tpm2-software/tpm2-tss-engine
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=TPM2
  DEPENDS+= +tpm2-tss +libopenssl
endef

define Package/tpm2-tss-engine/description
  OpenSSL Engine for TPM2 devices
endef

define Package/tpm2-tss-engine/install
	$(INSTALL_DIR) $(1)/usr/lib/engines-1.1
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/engines-1.1/libtpm2tss.so* $(1)/usr/lib/engines-1.1/
	$(CP) $(PKG_INSTALL_DIR)/usr/lib/engines-1.1/tpm2tss.so* $(1)/usr/lib/engines-1.1/

	$(INSTALL_DIR) $(1)/usr/bin
	$(CP) $(PKG_INSTALL_DIR)/usr/bin/* $(1)/usr/bin/
endef

define Build/InstallDev
	$(INSTALL_DIR) $(1)/usr/include
	$(CP) $(PKG_INSTALL_DIR)/usr/include/tpm2-tss-engine.h $(1)/usr/include/
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
