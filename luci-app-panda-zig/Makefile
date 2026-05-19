include $(TOPDIR)/rules.mk

PKG_VERSION:=0.2.1

LUCI_TITLE:=LuCI support for Panda Zig DDNS
LUCI_DEPENDS:=+luci-base +panda-zig

PKG_LICENSE:=MIT
PKG_MAINTAINER:=Pi <qaz69s@github>

include $(TOPDIR)/feeds/luci/luci.mk

define Package/luci-app-panda-zig/install
	$(call BuildPackage/luci-app-panda-zig/install,$(1))
	$(INSTALL_DIR) $(1)/usr/libexec/rpcd
	$(INSTALL_BIN) $(CURDIR)/root/usr/libexec/rpcd/luci.panda-zig \
		$(1)/usr/libexec/rpcd/luci.panda-zig
endef

ifndef Package/luci-app-panda-zig/postinst
define Package/luci-app-panda-zig/postinst
[ -n "$${IPKG_INSTROOT}" ] || { \
	rm -f /tmp/luci-indexcache.* \
	rm -rf /tmp/luci-modulecache/ \
	/etc/init.d/rpcd reload 2>/dev/null
	exit 0
}
endef
endif

$(eval $(call BuildPackage,luci-app-panda-zig))
