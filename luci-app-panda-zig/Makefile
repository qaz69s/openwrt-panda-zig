# LuCI web interface for Panda Zig DDNS
# 遵循 OpenWrt 25.12 包规范

include $(TOPDIR)/rules.mk

LUCI_TITLE     := Panda Zig DDNS
LUCI_DEPENDS   := +luci-base +panda-zig
LUCI_PKGARCH   := all

include $(TOPDIR)/feeds/luci/luci.mk

# call BuildPackage - OpenWrt buildroot signature
