# LZCWrt 旁路由完整指南

本指南介绍如何在懒猫微服中安装 LZCWrt，并通过 LZCWrt 创建 iStoreOS、OpenWrt 或 ImmortalWrt 旁路由实例。最后附带 iStoreOS 安装 OpenClash 插件的示例，适合需要 **全屋科学上网，全屋可以上网** 的场景。

## 适用场景

- 想在微服里快速创建旁路由实例，不想手动维护 Docker Compose 和 `macvlan` 网络。
- 想在 iStoreOS、OpenWrt、ImmortalWrt 之间按使用习惯选择系统镜像。
- 想让家里设备通过旁路由统一使用网络能力，例如插件、透明代理或其他 OpenWrt 生态功能。

## 前置条件

- 微服需要连接有线网络。
- 微服系统版本不低于 `1.5.0`。
- 需要管理员权限。
- 创建实例前，请提前确认局域网网关、子网、DNS 和一个未被占用的静态 IP。

## 1. 安装 LZCWrt

### 1.1 下载应用包

[点击下载仓库内置的 LZCWrt v0.1.6](../../../packages/lzcwrt/cloud.lazycat.app.lzcwrt-v0.1.6.lpk)

### 1.2 将软件包移动到懒猫网盘

![image-20260507094237317](https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/image-20260507094237317.png)

### 1.3 在微服安装 LZCWrt

![image-20260507094306986](https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/image-20260507094306986.png)

## 2. 认识实例配置

进入 LZCWrt 后，创建旁路由实例前先确认公用配置。

![image-20260506143612101](https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/image-20260506143612101-1778050345385-1-1778050376661-3.png)

<img src="https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/image-20260507094452650.png" alt="image-20260507094452650" style="zoom:80%;" />

配置项说明：

- 实例 ID：当前旁路由实例在 LZCWrt 中的 ID。
- 系统来源：可以选择内置 OpenWrt、ImmortalWrt、iStoreOS，也可以使用自定义镜像。
- 自定义 URL：通过镜像链接运行旁路由实例。
- 上传本地文件：通过本地镜像文件运行旁路由实例。
- 网络模式：提供多种网络模式，当前旁路由场景优先使用 `macvlan`。
- 静态 IP：旁路由实例在局域网中的固定地址。
- 自动探测推荐配置：不了解当前网络环境时，可以让 LZCWrt 自动寻找空闲 IP 并填充网络配置。
- 高级网络设置：手动设置网关、子网和 DNS。

系统选择建议：

| 系统 | 优点 | 注意点 | 适合用户 |
| --- | --- | --- | --- |
| iStoreOS | 中文界面、上手简单、插件安装方便 | 自由度相对低，主要依赖商店生态 | 想开箱即用、不想折腾 |
| OpenWrt | 官方、稳定、可定制性强 | 配置门槛高，对新手不友好 | 熟悉网络配置、需要高度定制 |
| ImmortalWrt | 基于 OpenWrt，国内场景优化较多 | 仍然偏技术向 | 想要功能丰富并兼顾国内使用习惯 |

## 3. 创建 iStoreOS 旁路由实例

如果目标是快速使用旁路由，优先建议从 iStoreOS 开始。

### 3.1 填写创建信息

<img src="https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/image-20260507094911454.png" alt="image-20260507094911454" style="zoom:80%;" />

如果不确定当前网络环境，可以使用自动探测功能，让 LZCWrt 自动寻找空闲 IP 和推荐网络配置。

### 3.2 访问 iStoreOS Web 页面

实例创建完成后，可以通过两种方式进入 iStoreOS Web 页面：

- 点击**进入 LuCI**按钮。
- 复制网络配置中的 IP 地址，在浏览器中打开。

![image-20260507095345788](https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/image-20260507095345788.png)

默认账号密码：

- 账号：`root`
- 密码：`root`

![image-20260506152211779](https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/image-20260506152211779.png)

![image-20260507095039141](https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/image-20260507095039141.png)

### 3.3 使用注意

**使用 iStoreOS 软路由实例时，不要操作和硬件有关的内容。**

![image-20260507095115766](https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/image-20260507095115766.png)

## 4. 创建 OpenWrt 旁路由实例

### 4.1 填写创建信息

<img src="https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/image-20260507095246849.png" alt="image-20260507095246849" style="zoom:80%;" />

如果不确定当前网络环境，可以使用自动探测功能，让 LZCWrt 自动寻找空闲 IP 和推荐网络配置。

### 4.2 访问 OpenWrt Web 页面

实例创建完成后，可以通过两种方式进入 OpenWrt Web 页面：

- 点击**进入 LuCI**按钮。
- 复制网络配置中的 IP 地址，在浏览器中打开。

![image-20260507095320344](https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/image-20260507095320344.png)

默认账号密码：

- 账号：`root`
- 密码：`root`

![image-20260506152920997](https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/image-20260506152920997.png)

![image-20260507095407770](https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/image-20260507095407770.png)

## 5. 创建 ImmortalWrt 旁路由实例

### 5.1 填写创建信息

<img src="https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/image-20260507095539442.png" alt="image-20260507095539442" style="zoom:80%;" />

如果不确定当前网络环境，可以使用自动探测功能，让 LZCWrt 自动寻找空闲 IP 和推荐网络配置。

### 5.2 访问 ImmortalWrt Web 页面

实例创建完成后，可以通过两种方式进入 ImmortalWrt Web 页面：

- 点击**进入 LuCI**按钮。
- 复制网络配置中的 IP 地址，在浏览器中打开。

![image-20260507095604275](https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/image-20260507095604275.png)

默认账号密码：

- 账号：`root`
- 密码：`root`

![image-20260506153205157](https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/image-20260506153205157.png)

![image-20260507095616802](https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/image-20260507095616802.png)

## 6. iStoreOS 安装 OpenClash 插件

这一节以 `iStoreOS + OpenClash` 为例。iStoreOS 可以通过社区提供的 `.run` 包安装插件，步骤比较直接。

### 6.1 下载插件

[下载插件：bcseputetto/Are-u-ok](https://github.com/bcseputetto/Are-u-ok)

下载时需要根据当前系统版本选择对应插件。LZCWrt 内置示例使用的是 **iStoreOS 24.10.6**。

![image-20260506163925060](https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/image-20260506163925060.png)

![image-20260506164029747](https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/image-20260506164029747.png)

请根据当前系统平台选择下载版本。可以通过 SSH 连接微服后执行以下命令查看架构：

```bash
uname -m
```

![image-20260506164224693](https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/image-20260506164224693.png)

如果输出是 `x86_64`，就选择 `x86_64` 平台版本下载。

![image-20260506164047087](https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/image-20260506164047087.png)

### 6.2 安装插件

在 iStoreOS 的插件安装页面中，选择刚下载的 `.run` 文件并提交。

![image-20260506164757488](https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/image-20260506164757488.png)

安装完成后，按插件页面提示继续配置订阅、规则和运行模式。
