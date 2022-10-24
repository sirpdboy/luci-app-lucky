
include $(TOPDIR)/rules.mk

PKG_NAME:=lucky
PKG_VERSION:=1.4.10
PKG_RELEASE:=$(AUTORELEASE)

PKG_SOURCE_PROTO:=git
PKG_SOURCE:=$(PKG_NAME)-$(PKG_VERSION).tar.gz
PKG_SOURCE_URL:=https://github.com/gdy666/lucky.git
PKG_SOURCE_VERSION:=5e820e65551c686b822924702747472bca702b67
PKG_MIRROR_HASH:=auto

PKG_LICENSE:=AGPL-3.0-only
PKG_LICENSE_FILES:=LICENSE
PKG_MAINTAINER:=herboy2008 <herboy2008@gmail.com>

PKG_BUILD_DEPENDS:=golang/host
PKG_BUILD_PARALLEL:=1
PKG_USE_MIPS16:=0

GO_PKG:=github.com/jeessy2/ddns-go/v4
GO_PKG_LDFLAGS:=-s -w
GO_PKG_LDFLAGS_X:=m.version=$(PKG_VERSION)
include $(INCLUDE_DIR)/package.mk
include $(TOPDIR)/feeds/packages/lang/golang/golang-package.mk

define Package/lucky
  TITLE:=A Linux web GUI client of lucky
  SECTION:=net
  CATEGORY:=Network
  SUBMENU:=Web Servers/Proxies
  DEPENDS:=$(GO_ARCH_DEPENDS) +ca-bundle 
  URL:=https://github.com/gdy666/lucky
endef

define Package/lucky/description
  lucky is DDNS-GO,SOCAT,FRPC
endef

define Package/lucky/postinst
#!/bin/sh
if [ -z "$${IPKG_INSTROOT}" ]; then
	[ -f /etc/uci-defaults/luci-lucky ] && /etc/uci-defaults/luci-lucky && rm -f /etc/uci-defaults/luci-lucky
fi
endef



define Package/lucky/install
	$(call GoPackage/Package/Install/Bin,$(1))
	$(INSTALL_DIR) $(1)/usr/bin $(1)/etc/init.d $(1)/etc/uci-defaults $(1)/etc/lucky
	$(INSTALL_BIN) ./files/lucky.init $(1)/etc/init.d/lucky
	$(INSTALL_BIN) ./files/luci-lucky.uci-default $(1)/etc/uci-defaults/luci-lucky
	$(INSTALL_DATA) ./files/lucky-default.conf $(1)/etc/lucky/lucky-default.conf

endef

$(eval $(call GoBinPackage,lucky))
$(eval $(call BuildPackage,lucky))
