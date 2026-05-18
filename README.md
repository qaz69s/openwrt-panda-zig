# OpenWrt Panda Zig DDNS

Panda Zig DDNS 的 OpenWrt 打包仓库。从上游 GitHub Releases 下载预编译静态二进制，无需 Zig 工具链。

## 包

| 包 | 说明 |
|---|---|
| `panda-zig` | Zig DDNS 守护进程二进制 + 启动脚本 + 默认配置 |
| `luci-app-panda-zig` | LuCI 管理面板 + 日志查看器 |

## 结构

```
panda-zig/
├── Makefile              # 构建文件（下载预编译包）
└── files/
    ├── etc/config/panda-zig   # 默认 UCI 配置
    └── etc/init.d/panda-zig   # procd 启动脚本

luci-app-panda-zig/
├── Makefile              # 构建文件（luci.mk）
├── htdocs/
│   └── luci-static/resources/view/panda-zig/
│       ├── ddns.js       # 设置面板
│       └── log.js        # 日志面板
└── root/
    └── usr/
        ├── libexec/rpcd/luci.panda-zig        # rpcd 插件
        └── share/
            ├── luci/menu.d/luci-app-panda-zig.json
            └── rpcd/acl.d/luci-app-panda-zig.json
```

## 构建

作为 feeds 添加到 OpenWrt 源码：

```bash
echo "src-git panda-zig https://github.com/qaz69s/openwrt-panda-zig.git" >> feeds.conf.default
./scripts/feeds update panda-zig
./scripts/feeds install panda-zig
./scripts/feeds install luci-app-panda-zig

make package/panda-zig/compile V=s
make package/luci-app-panda-zig/compile V=s
```

编译时会自动根据架构（x86_64 / aarch64 / armv7 / i686）下载对应的预编译二进制。

## 支持架构

| Release 二进制 | 架构 |
|---|---|
| `panda-zig` (x86_64) | x86_64 |
| `panda-zig-aarch64` | ARM64 (aarch64) |
| `panda-zig-armv7` | ARMv7 HF |
| `panda-zig-i686` | i686 |

## 上游

Zig 源码：https://github.com/qaz69s/panda-zig
预编译二进制：https://github.com/qaz69s/panda-zig/releases
