include $(TOPDIR)/rules.mk

PKG_VERSION:=0.2.1

LUCI_TITLE:=LuCI support for Panda Zig DDNS
LUCI_DEPENDS:=+luci-base +panda-zig

PKG_LICENSE:=MIT
PKG_MAINTAINER:=Pi <qaz69s@github>

include $(TOPDIR)/feeds/luci/luci.mk

define Package/luci-app-panda-zig/install
	$(call Package/luci-app-panda-zig/install,$(1))
	$(INSTALL_DIR) $(1)/usr/libexec/rpcd
	$(INSTALL_BIN) $(CURDIR)/root/usr/libexec/rpcd/luci.panda-zig \
		$(1)/usr/libexec/rpcd/luci.panda-zig
endef

$(eval $(call BuildPackage,luci-app-panda-zig))
