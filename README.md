# softrouter

在懒猫微服上使用 `Dockge + iStoreOS` 搭建软路由的文档仓库。

## 适用场景

- 想在微服环境里运行 iStoreOS / OpenWrt 类软路由系统
- 需要基于 `macvlan` 将容器接入局域网
- 希望微服重启后自动恢复网卡混杂模式与容器启动

## 快速开始

1. 阅读完整教程：[`docs/guides/zh/istore-softrouter-on-lazycat.md`](docs/guides/zh/istore-softrouter-on-lazycat.md)
2. 按教程先开启网卡混杂模式
3. 在 Dockge 中创建 `macvlan` 网络并部署 iStoreOS 容器
4. 配置开机自启（含 `promisc on` 自动执行）

## 关键前提

- 微服必须使用有线网络
- 你需要有 SSH 权限与 `lzc-docker` 命令使用权限
- 网卡名默认示例为 `enp2s0`，请按你的机器实际网卡名修改

## 目录结构

```text
.
├── README.md
├── docs
│   ├── README.md
│   └── guides
│       └── zh
│           └── istore-softrouter-on-lazycat.md
└── examples
    └── systemd
        └── auto-start-promisc-mode.service
```

## 示例文件

- systemd 服务样例：[`examples/systemd/auto-start-promisc-mode.service`](examples/systemd/auto-start-promisc-mode.service)

