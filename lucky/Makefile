# SPDX-License-Identifier: GPL-3.0-only
#
# Copyright (C) 2021-2022  sirpdboy  <herboy2008@gmail.com>
# 
# This is free software, licensed under the Apache License, Version 2.0 .
#

include $(TOPDIR)/rules.mk

PKG_ARCH:=$(ARCH)
PKG_NAME:=lucky
PKG_VERSION:=1.5.1
PKG_RELEASE:=$(AUTORELEASE)

PKG_SOURCE:=$(PKG_NAME)_$(PKG_VERSION)_Linux_$(PKG_ARCH).tar.gz
PKG_SOURCE_URL:=https://github.com/gdy666/lucky/releases/download/v$(PKG_VERSION)/
PKG_HASH:=skip
PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)_$(PKG_VERSION)

PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0

include $(INCLUDE_DIR)/package.mk

define Package/$(PKG_NAME)
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Web Servers/Proxies

  TITLE:=A Linux web GUI client of lucky
  DEPENDS:=
  PKGARCH:=all
  URL:=https://github.com/gdy666/lucky
endef

define Package/$(PKG_NAME)/description
  Main functions of Lucky: dynamic domain name ddns-go service, socat,frp 
endef

define Package/$(PKG_NAME)/postinst
#!/bin/sh
if [ -z "$${IPKG_INSTROOT}" ]; then
	[ -f /etc/uci-defaults/luci-lucky ] && /etc/uci-defaults/luci-lucky && rm -f /etc/uci-defaults/luci-lucky
fi
endef

define Build/Configure
endef

define Build/Compile
endef

define Package/$(PKG_NAME)/install
	$(INSTALL_DIR) $(1)/usr/bin $(1)/etc/init.d $(1)/etc/uci-defaults $(1)/etc/lucky
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/lucky/usr/bin $(1)/usr/bin
	$(INSTALL_BIN) ./files/lucky.init $(1)/etc/init.d/lucky
	$(INSTALL_BIN) ./files/luci-lucky.uci-default $(1)/etc/uci-defaults/luci-lucky
	$(INSTALL_DATA) ./files/lucky-default.conf $(1)/etc/lucky/lucky-default.conf

endef

$(eval $(call BuildPackage,$(PKG_NAME)))
