#
# Copyright (C) 2021 Xaptum, Inc.
#
# This is free software, licensed under the GNU General Public License v2.
# See /LICENSE for more information.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=tpm2-tools
PKG_VERSION:=5.0
PKG_RELEASE:=1

PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/tpm2-software/tpm2-tools/releases/download/$(PKG_VERSION)
PKG_HASH:=e1b907fe29877628052e08ad84eebc6c3f7646d29505ed4862e96162a8c91ba1

PKG_MAINTAINER:=David R. Bild <david.bild@xaptum.com>
PKG_LICENSE:=BSD-3-Clause
PKG_LICENSE_FILES:=LICENSE

PKG_FIXUP:=configure
PKG_INSTALL:=1

include $(INCLUDE_DIR)/package.mk

define Package/tpm2-tools
  TITLE:=TPM2-Tools
  URL:=https://github.com/tpm2-software/tpm2-tools
  SECTION:=utils
  CATEGORY:=Utilities
  SUBMENU:=TPM2
  DEPENDS+= +tpm2-tss +libopenssl +libcurl +libuuid
endef

TARGET_CFLAGS:= -U_FORTIFY_SOURCE $(TARGET_OPTIMIZATION)$(if $(CONFIG_DEBUG), -g3) $(EXTRA_OPTIMIZATION)

define Package/tpm2-tools/description
Trusted Platform Module (TPM2.0) tools
endef

define Package/tpm2-tools/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_INSTALL_DIR)/usr/bin/tpm2_* $(1)/usr/bin
endef

$(eval $(call BuildPackage,$(PKG_NAME)))
