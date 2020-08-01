# MT7688 4G WIFI 路由器

本项目基于 MT7688 与 EC20 配置个人 4G WIFI 路由器，编译环境基于 docker； 只完成基础功能。

使用的核心板为 8MB Flash，64MB RAM，串口用uart0，在LINKIT7688的基础配置上修改

Openwrt 版本为 19.07, 使用 MT76 WIFI 驱动

使用自带 qmi 支持

使用 mwan3 实现有线与4G网络的切换

## 编译

运行

```
git submodule update --init

```
或者手动下载 openwrt 源码到 /src/openwrt 目录（只在 openwrt 19.07 下测试过）

本机安装好docker与docker-compose, 运行

```
docker-compose up --build
```

启动编译环境。

```
docker-compose exec -u docker compiler /bin/bash
```

进入编译环境


修改 openwrt/target/linux/ramips/dts/LINKIT7688.dts，包括内存大小，Flash大小，console 串口

```
    chosen {
		bootargs = "console=ttyS0,57600";
	};

	memory@0 {
		device_type = "memory";
		reg = <0x0 0x4000000>;
	};

```

```
            partition@50000 {
				compatible = "denx,uimage";
				label = "firmware";
				reg = <0x50000 0x7b0000>;
			};
```

```
cd /src/openwrt
./scripts/feeds update -a
./scripts/feeds install -a
make menuconfig
```

选择 

MediaTek Ralink MIPS - MT76x8 based boards - MediaTek LinkIt Smart 7688

Network - mt7688-4g

```
make V=99
```

烧写，登录，配置

* 路由器默认IP为 192.16.0.1
* WIFI SSID 为 ot4g 密码 12345678
* 默认 root 用户密码为空，请登录后设置
* 有线网卡默认为dhcp client的方式获取IP
* 如果同时接入有线网与4G，将优先使用有线网，如果有线网断开，将切换到4G