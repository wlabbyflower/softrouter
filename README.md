# **softrouter？使用lazycat也可以！！！**

> 需要用到lazycat商店中的[dockge](https://appstore.lazycat.cloud/#/shop/detail/cloud.lazycat.app.dockge)

## 前言

本教程使用istore做为教程配置软路由（理论上其他如openwrt也可以这样配置），配置成功之后开机软路由系统就会自动启动。无需任何额外的启动。

**本教程需要微服使用有线网络才可以配置！！！**
**本教程需要微服使用有线网络才可以配置！！！**
**本教程需要微服使用有线网络才可以配置！！！**

## 配置lazy cat网络

```bash
# 开启网卡混杂模式
ip link set enp2s0 promisc on
```

#### 判断是否启动成功

```bash
ip a | grep enp2s0
```

![eeeae88a8ea345417166ca32becf7e3e](https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/eeeae88a8ea345417166ca32becf7e3e.png)

有红框里面的表示启动成功

[什么是网口混杂模式？开启它有什么效果？](https://zdyxry.github.io/2020/03/18/%E7%90%86%E8%A7%A3%E7%BD%91%E5%8D%A1%E6%B7%B7%E6%9D%82%E6%A8%A1%E5%BC%8F/)

### 给pg-docker新建一个macvlan网络供istore使用

ssh到微服上依次执行以下命令

```bash
#1. 进入dockge
lzc-docker exec -it cloudlazycatappdockge-back-1 bash
#2. 创建网络
docker network create -d macvlan --subnet=局域网ip网络/24 --gateway=局域网网关 -o parent=enp2s0 istore
#3. 查看docker网络
docker network ls
```

如果成功会有一个名为istore的网络

![02b8d13a134bc22e0fbbe5f488de6c8a](https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/02b8d13a134bc22e0fbbe5f488de6c8a.png)

### 添加istore容器

![c164a3cdbc8b04963f958e8e7e504479](https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/c164a3cdbc8b04963f958e8e7e504479.png)

#### componse 配置

**ipv4_address 字段需要修改！！！**
**ipv4_address 字段需要修改！！！**
**ipv4_address 字段需要修改！！！**

```yaml
services:
  iStoreOS:
    image: registry.lazycat.cloud/longixaoyi/xkand/istoreos:be7ab531e46d3f8b
    container_name: iStoreOS
    restart: always
    privileged: true
    volumes:
      - /lib/modules:/lib/modules:ro
      - /dev:/dev
    command: /sbin/init
    cap_add:
      - NET_ADMIN
      - SYS_MODULE
    devices:
      - /dev/net/tun
    networks:
      istore:
        ipv4_address: 您局域网ip地址填一个
networks:
  istore:
    external: true
```

在此填一个自己钟意的名字

![21d7135dcbc4270bb601654bb3b91ca9](https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/21d7135dcbc4270bb601654bb3b91ca9.png)

保存、启动容器

![26df69f9a68e0b0fb26060fca4327a13](https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/26df69f9a68e0b0fb26060fca4327a13.png)

启动成功的标识

![44c46ab5d426dd5d835a1afcdda3c233](https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/44c46ab5d426dd5d835a1afcdda3c233.png)

## 最后一步

获取istore自己的ip，进入istore web页面

```bash
1. ssh 到微服上
2. 进入dockge容器
lzc-docker exec -it cloudlazycatappdockge-back-1 bash
3. 进入 istore容器
docker exec -it iStoreOS bash
4. 查看 istore ip
ip a
```

![c5f2bc8814927939ce48c68c04fdf8a6](https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/c5f2bc8814927939ce48c68c04fdf8a6.png)

直接浏览器访问ip

默认用户密码： root/root

![f20bdc8c616a585a433e88dfef823a6e](https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/f20bdc8c616a585a433e88dfef823a6e.png)

![f890b544dc3b7fb14434b8b081e49eb9](https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/f890b544dc3b7fb14434b8b081e49eb9.png)

### 配置开机自启

### 配置dockge自启

![998d199a6b2b638e5efeb2b1f0b62781](https://lzc-playground-1301583638.cos.ap-chengdu.myqcloud.com/guidelines/395/998d199a6b2b638e5efeb2b1f0b62781.png)

### 配置自动开启微服混杂模式

因为微服重启会回滚，所以需要写一个开机自启服务去自动开启 

1.创建目录

```bash
mkdir -p ~/.config/systemd/user
```

2.创建服务 

`vim auto-start-promisc-mode.service` 

内容为：

```bash
[Unit]
Description=开机切换网卡为混杂模式
After=network.target

[Service]
Type=oneshot
ExecStart=sh -c 'ip link set enp2s0 promisc on'

[Install]
WantedBy=default.target
```

3.设置开机自启

```bash
systemctl --user enable auto-start-promisc-mode.service
```

至此全部配置好了，微服启动就会启动脚本开启网卡混杂模式，然后启动dockge，dockge会启动istore容器。
