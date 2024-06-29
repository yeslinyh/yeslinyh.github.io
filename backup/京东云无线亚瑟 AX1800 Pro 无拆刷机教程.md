0. 刷前必须看

    1. 本教程**完全自用**，**完全参考**自[猫神iTyc](https://www.bilibili.com/read/cv34316745/)
    2. 机器拿到手千万**不能联网**，**WAN 口**千万**不能接网线**
1. 刷 uboot

    1. 电脑网口接路由器 LAN 口，打开浏览器输入：`192.168.68.1`，进入路由器管理界面
    2. `上网指导` -> `你可以选择其他模式` -> `手动配置` -> `DHCP上网`
    3. 页面底部检查版本号：**JDC02-1.2.2.r2080**（不保证其他高版本可用）
    4. 在 `192.168.68.1` 页面，浏览器按 F12 **打开开发人员工具**，在**控制台**中输入以下内容后，回车

        ```
        $.ajax({
            url: 'http://' + $.cookie("HostAddrIP") + '/jdcapi',
            async: false,
            data: JSON.stringify({
                jsonrpc: "2.0",
                id: 1,
                method: "call",
                params: [
                    $.cookie("sessionid"),
                    "service",
                    "set",
                    {
                        "name": "dropbear",
                        "instances": {"instance1": {"command": ["/usr/sbin/dropbear"]}}
                    }
                ]
            }),
            dataType: 'json',
            type: 'POST'
        })
        ```
    5. 下载[大雕](https://github.com/coolsnowwolf)的[不死 uboot](https://mbd.pub/o/bread/ZJeXk59v)，解压出文件备用
    6. 下载 [WinSCP](http://172.207.128.150:5244/d/R2_zhuabafish/%E5%B8%B8%E7%94%A8%E8%BD%AF%E4%BB%B6/%E7%BD%91%E7%BB%9C%E7%9B%B8%E5%85%B3/WinSCP-6.3.3-Setup.exe?sign=w5-XrXSGzgvivdP40V9kFWMVbbyG-p-LDQucHiim5cE=:0) 软件，选择 SCP 协议，主机名填 root，密码是你初始化路由器时输入的 WiFi 密码

        ![](https://ca6d7cae.telegraph-image-6yx.pages.dev/file/cc35853df694858769bc9.png)
    7. 在 WinSCP 登录后，上传刚刚下载的文件：`gpt.bin` 和 `uboot.bin` 到路由器的 `/tmp` 目录下
    8. 下载 ssh 软件：[MobaXterm](https://pcdiy.xyz/d/Cloudflare%20R2/%E7%94%B5%E8%84%91%E8%BD%AF%E4%BB%B6/%E7%BD%91%E7%BB%9C%E7%9B%B8%E5%85%B3/SSH_%E5%B7%A5%E5%85%B7.MobaXterm_Personal/MobaXterm_Portable_v24.1.zip?sign=wMpKNN0lbJS9JZkSMs0jQqIyqsTVA_w6sFz13g383pY=:0) ，使用和 ((20240512171639-p5x42gw "WinSCP")) 一样的账户密码登录 ssh
    9. ssh 进入路由器后，依次一条一条输入以下命令，每次输入后均要按回车

        ```
        cd /tmp
        ```

        ```
        dd if=uboot.bin of=/dev/mmcblk0p13
        ```

        ```
        dd if=gpt.bin of=/dev/mmcblk0 bs=512 count=34
        ```

        ```
        dd if=/dev/zero of=/dev/mmcblk0p2
        ```

        ```
        dd if=/dev/zero of=/dev/mmcblk0p3
        ```

        ```
        sync
        ```
2. 刷入 OpenWrt 初始固件：[openwrt-05.02.2024-qualcommax-ipq60xx-jdc_ax1800-pro-squashfs-factory.bin](https://pcdiy.xyz/d/Cloudflare%20R2/Linux/Openwrt/%E4%BA%AC%E4%B8%9C%E4%BA%91%E6%97%A0%E7%BA%BF%E4%BA%9A%E7%91%9F_AX1800_Pro/1_%E5%88%9D%E5%A7%8B%E5%9B%BA%E4%BB%B6/openwrt-05.02.2024-qualcommax-ipq60xx-jdc_ax1800-pro-squashfs-factory.bin?sign=OyTFYQ2Qo0GguKfelCxhuxwY9MFFlbPjnxPnOaWo1Fo=:0)

    1. 断电路由器，然后戳住 `reset` 通电开机，等 10s 后松开
    2. 设置电脑与路由器相连的那个网卡 IP 为 `192.168.1.2`

        ![](https://ca6d7cae.telegraph-image-6yx.pages.dev/file/e48f19917dccb47c92baa.png)
    3. 在浏览器中输入 `192.168.1.1` 进入 Web 不死界面
    4. 在不死界面上传刚刚下载的 ((20240512201250-0f9yicl "OpenWrt 初始固件"))
    5. uboot 中出现大圈圈旋转后，等等待 15s，把电脑网卡改为自动获取 IP

        ![](https://ca6d7cae.telegraph-image-6yx.pages.dev/file/e9f54b32c900774859143.png)

        ![](https://ca6d7cae.telegraph-image-6yx.pages.dev/file/dba5a2cf3d227ce96bb36.png)
3. 刷入 istoreOS 或大雕的 QWRT 固件，获取方法：V 大雕 50 进 VIP 固件群

    ![](https://ca6d7cae.telegraph-image-6yx.pages.dev/file/ee3baf4243226b5dbed24.jpg)

    1. 在浏览器中输入 `10.0.0.1`，进入初始固件后台，登录账户密码均为：`root`
    2. 依次打开 `系统` -> `备份/升级` -> `刷写新的固件` ->`选择文件`

        ![](https://ca6d7cae.telegraph-image-6yx.pages.dev/file/149ca600ad6d06d83737c.png)
    3. 继续按照如图所示勾选，一个也不能勾错，然后点继续，等待些许时间即可刷机完成

        ![](https://ca6d7cae.telegraph-image-6yx.pages.dev/file/b6fb7e4d25d59c4cbdb42.png)
    4. QWRT 默认登陆地址是`http://192.168.1.1`，默认帐号密码是`admin`/`password`
    5. 芝麻开门

        ```
        echo 0xDEADBEEF > /etc/config/google_fu_mode
        ```