# softrouter

在懒猫微服上部署软路由 / 旁路由的资料仓库，已整合 `Dockge + iStoreOS` 手动方案与 `LZCWrt` 应用方案。

## 方案选择

| 方案 | 适合场景 | 入口 |
| --- | --- | --- |
| `LZCWrt` | 想通过微服应用快速创建 iStoreOS / OpenWrt / ImmortalWrt 旁路由实例，实现 **全屋科学上网，全屋可以上网** | [LZCWrt 完整指南](docs/guides/lzcwrt/guide.md) |
| `Dockge + iStoreOS` | 想手动管理 Docker Compose、macvlan 和开机自启 | [Dockge + iStoreOS 部署指南](docs/guides/dockge-istoreos.md) |

## 快速开始

1. 确认微服使用有线网络，并准备好管理员权限。
2. 新用户优先阅读 [`docs/guides/lzcwrt/guide.md`](docs/guides/lzcwrt/guide.md)，完成 LZCWrt 安装、实例创建和插件示例。
3. 如果选择手动容器方案，阅读 [`docs/guides/dockge-istoreos.md`](docs/guides/dockge-istoreos.md)。

## 关键前提

- 微服必须使用有线网络，旁路由和 `macvlan` 场景不建议走无线网络。
- LZCWrt 方案要求微服系统版本不低于 `1.5.0`，并且需要管理员操作。
- Dockge 手动方案需要 SSH 权限、`lzc-docker` 命令权限，并按实际网卡名替换示例里的 `enp2s0`。
- 创建旁路由实例前，先规划好局域网 IP、网关、子网和 DNS，避免和现有设备冲突。

## 常用链接

- 文档索引：[`docs/README.md`](docs/README.md)
- LZCWrt 指南索引：[`docs/guides/lzcwrt/README.md`](docs/guides/lzcwrt/README.md)
- LZCWrt 应用包：[`packages/lzcwrt/cloud.lazycat.app.lzcwrt-v0.1.6.lpk`](packages/lzcwrt/cloud.lazycat.app.lzcwrt-v0.1.6.lpk)
- systemd 示例：[`examples/systemd/auto-start-promisc-mode.service`](examples/systemd/auto-start-promisc-mode.service)
- Dockge 应用页：[LazyCat App Store - Dockge](https://appstore.lazycat.cloud/#/shop/detail/cloud.lazycat.app.dockge)

## 目录结构

```text
.
├── README.md
├── docs
│   ├── README.md
│   └── guides
│       ├── dockge-istoreos.md
│       └── lzcwrt
│           ├── README.md
│           └── guide.md
├── examples
│   └── systemd
│       └── auto-start-promisc-mode.service
└── packages
    └── lzcwrt
        └── cloud.lazycat.app.lzcwrt-v0.1.6.lpk
```
