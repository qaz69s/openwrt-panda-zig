#
# Copyright (C) 2026 qaz69s
#
# This is free software, licensed under the MIT License.
#

include $(TOPDIR)/rules.mk

PKG_NAME:=panda-zig
PKG_VERSION:=0.3.1
PKG_RELEASE:=1

# Map OpenWrt ARCH to panda-zig release asset name
PANDA_ASSET:=panda-zig
ifneq ($(filter aarch64%,$(ARCH)),)
  PANDA_ASSET:=panda-zig-aarch64
else ifneq ($(filter arm%,$(ARCH)),)
  PANDA_ASSET:=panda-zig-armv7
else ifneq ($(filter i386 i586 i686%,$(ARCH)),)
  PANDA_ASSET:=panda-zig-i686
else ifneq ($(filter x86_64%,$(ARCH)),)
  PANDA_ASSET:=panda-zig-x86_64
endif

PKG_SOURCE:=$(PANDA_ASSET)
PKG_SOURCE_URL:=https://github.com/qaz69s/panda-zig/releases/download/v$(PKG_VERSION)/
PKG_HASH:=skip

PKG_BUILD_DIR:=$(BUILD_DIR)/$(PKG_NAME)-$(PKG_VERSION)

include $(INCLUDE_DIR)/package.mk

define Package/panda-zig
  SECTION:=net
  CATEGORY:=Network
  TITLE:=Panda Zig DDNS
  URL:=https://github.com/qaz69s/panda-zig
  DEPENDS:=@(x86_64||aarch64||arm||i386)
endef

define Package/panda-zig/description
  Lightweight dynamic DNS update daemon written in Zig.
  Supports Cloudflare, DNSPod, Aliyun, No-IP, DuckDNS, Baidu,
  and custom update URLs. ~780KB on disk.
endef

# ---------- No build needed (precompiled binary) ----------

define Build/Prepare
	mkdir -p $(PKG_BUILD_DIR)
	cp $(DL_DIR)/$(PKG_SOURCE) $(PKG_BUILD_DIR)/panda-zig
	chmod 0755 $(PKG_BUILD_DIR)/panda-zig
endef

define Build/Configure
endef

define Build/Compile
endef

# ---------- Install ----------

define Package/panda-zig/install
	$(INSTALL_DIR) $(1)/usr/bin
	$(INSTALL_BIN) $(PKG_BUILD_DIR)/panda-zig $(1)/usr/bin/
	$(INSTALL_DIR) $(1)/etc/init.d
	$(INSTALL_BIN) ./files/etc/init.d/panda-zig $(1)/etc/init.d/
	$(INSTALL_DIR) $(1)/etc/config
	$(INSTALL_CONF) ./files/etc/config/panda-zig $(1)/etc/config/
endef

$(eval $(call BuildPackage,panda-zig))
