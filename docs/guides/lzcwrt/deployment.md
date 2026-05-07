# 懒猫微服旁路由部署指南

- LZCWrt + iStoreOS
- LZCWrt + OpenWrt
- LZCWrt + ImmortalWrt

## 前言

本教程通过 LZCWrt 在微服中配置旁路由，需要提前在微服中安装好 LZCWrt。[点击下载仓库内置的 LZCWrt v0.1.6](../../../packages/lzcwrt/cloud.lazycat.app.lzcwrt-v0.1.6.lpk)

> 注意事项：
>
> 1. 仅限微服连接有线网使用
>
> 2. 限制最低系统版本 `1.5.0`，仅限管理员使用

## 1. 公用配置介绍

![image-20260506143612101](https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/image-20260506143612101-1778050345385-1-1778050376661-3.png)

<img src="https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/image-20260507094452650.png" alt="image-20260507094452650" style="zoom:80%;" />

选项说明：

- 实例 ID：当前创建的旁路由实例在 LZCWrt 中的 ID
- 系统来源：在这里提供了三个内置的旁路由镜像
  - OpenWrt
    - 优点：纯官方、最稳定、适配设备极多
    - 缺点：**对小白不友好**、界面简陋、配置多、容易出错
    - 适合群体：喜欢自己折腾、要高度定制
  - ImmortalWrt
    - 优点：基于 OpenWrt，**专为中国大陆优化**，界面比原版 OpenWrt 更友好一点
    - 缺点：还是偏技术向，比 OpenWrt 简单，但不如 iStoreOS 傻瓜化
    - 适合群体：想要**功能多、稳定、国内优化好**，又不想从零编译
  - iStoreOS
    - 优点：**极度简单**：界面现代化、中文
    - 缺点：自由度最低：只能用商店里的插件
    - 适合群体：想要开箱即用、不想折腾
- 自定义 URL（可选）：通过链接的方式获取旁路由镜像来运行实例
- 上传本地文件（可选）：通过上传本地已经下载好的旁路由镜像来运行实例
- 网络模式：在这里提供了三种网络模式给旁路由实例使用，目前推荐使用 `macvlan` 模式
- 静态 IP：配置当前旁路由实例在当前网络下的静态 IP
- 自动探测推荐配置：您可以手动设置旁路由实例的网络环境，如果您对当前实例的网络环境不太了解，可以直接使用**自动探测**功能，会为您自动配置好当前实例的网络环境
- 高级网络设置：您可以手动设置当前旁路由实例的网关、子网和 DNS

## 2. iStoreOS 旁路由实例创建

### 2.1 创建信息填写

<img src="https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/image-20260507094911454.png" alt="image-20260507094911454" style="zoom:80%;" />

**注意：如果您对当前实例的网络环境不太了解，可以直接使用自动探测功能，会为您找到当前网络环境下空闲的IP和相关的网络配置**

### 2.2 访问 iStoreOS Web 页面

在创建好实例后，可以通过两种方式进入 iStoreOS Web 页面

- 点击**进入 LuCI**按钮
- 复制网络配置中的 IP 地址，将 IP 地址复制到浏览器打开

![image-20260507095345788](https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/image-20260507095345788.png)

默认账号密码

- 账号：root
- 密码：root

![image-20260506152211779](https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/image-20260506152211779.png)

![image-20260507095039141](https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/image-20260507095039141.png)

### 2.3 特别注意

**使用 iStoreOS 软路由实例时，一定不要操作和硬件有关的内容**

![image-20260507095115766](https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/image-20260507095115766.png)

## 3. OpenWrt 软路由实例创建

### 3.1 创建信息填写

<img src="https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/image-20260507095246849.png" alt="image-20260507095246849" style="zoom:80%;" />

**注意：如果您对当前实例的网络环境不太了解，可以直接使用自动探测功能，会为您找到当前网络环境下空闲的IP和相关的网络配置**

### 3.2 访问 OpenWrt Web 页面

在创建好实例后，可以通过两种方式进入 OpenWrt Web 页面

- 点击**进入 LuCI**按钮
- 复制网络配置中的 IP 地址，将 IP 地址复制到浏览器打开

![image-20260507095320344](https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/image-20260507095320344.png)

默认账号密码

- 账号：root
- 密码：root

![image-20260506152920997](https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/image-20260506152920997.png)

![image-20260507095407770](https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/image-20260507095407770.png)

## 4. ImmortalWrt 软路由实例创建

### 4.1 创建信息填写

<img src="https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/image-20260507095539442.png" alt="image-20260507095539442" style="zoom:80%;" />

**注意：如果您对当前实例的网络环境不太了解，可以直接使用自动探测功能，会为您找到当前网络环境下空闲的IP和相关的网络配置**

### 4.2 访问 ImmortalWrt Web 页面

在创建好实例后，可以通过两种方式进入 ImmortalWrt Web 页面

- 点击**进入 LuCI**按钮
- 复制网络配置中的 IP 地址，将 IP 地址复制到浏览器打开

![image-20260507095604275](https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/image-20260507095604275.png)

默认账号密码

- 账号：root
- 密码：root

![image-20260506153205157](https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/image-20260506153205157.png)

![image-20260507095616802](https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/image-20260507095616802.png)
