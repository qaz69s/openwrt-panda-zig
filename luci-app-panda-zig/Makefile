include $(TOPDIR)/rules.mk

PKG_VERSION:=0.2.1

LUCI_TITLE:=LuCI support for Panda Zig DDNS
LUCI_DEPENDS:=+luci-base +panda-zig

PKG_LICENSE:=MIT
PKG_MAINTAINER:=Pi <qaz69s@github>

include $(TOPDIR)/feeds/luci/luci.mk

define Package/luci-app-panda-zig/install
	$(INSTALL_DIR) $(1)/www/luci-static/resources/view/panda-zig
	$(INSTALL_DIR) $(1)/www/luci-static/resources/view/panda-zig
	$(INSTALL_DIR) $(1)/usr/share/luci/menu.d
	$(INSTALL_DIR) $(1)/usr/share/rpcd/acl.d
	$(INSTALL_DIR) $(1)/usr/libexec/rpcd
	cp -pR $(PKG_BUILD_DIR)/htdocs/luci-static/resources/view/panda-zig/* $(1)/www/luci-static/resources/view/panda-zig/
	cp -pR $(PKG_BUILD_DIR)/root/usr/share/luci/menu.d/* $(1)/usr/share/luci/menu.d/
	cp -pR $(PKG_BUILD_DIR)/root/usr/share/rpcd/acl.d/* $(1)/usr/share/rpcd/acl.d/
	$(INSTALL_BIN) $(CURDIR)/root/usr/libexec/rpcd/luci.panda-zig $(1)/usr/libexec/rpcd/luci.panda-zig
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

# call BuildPackage - OpenWrt buildroot signature
