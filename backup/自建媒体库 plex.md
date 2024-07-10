​![](https://ca6d7cae.telegraph-image-6yx.pages.dev/file/14cad8ab038ba25a19ae5.png)​

# 如何部署

```powershell
docker run -d \
  --name=plex \
  --net=host \
  --restart unless-stopped \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=Etc/UTC \
  -e VERSION=docker \
  -e PLEX_CLAIM= `#optional` \
  -v [配置文件路径]:/config \
  -v [媒体库路径]:/media \
  linuxserver/plex:latest
```

以下为我个人的例子，每个人路径不同，请勿盲目复制：

```powershell
docker run -d \
  --name=plex \
  --net=host \
  --restart unless-stopped \
  -e PUID=1000 \
  -e PGID=1000 \
  -e TZ=Etc/UTC \
  -e VERSION=docker \
  -e PLEX_CLAIM= `#optional` \
  -v /volume4/docker/plex/library:/config \
  -v /volume1/media:/media \
  -v /volume1/sync/OneDrive/Media/Music/QQMusic:/mymusic \
  linuxserver/plex:latest
```

# 解决由于媒体库过大，而无法正常硬件解码的问题

0. 本教程完全参考自 [GitHub issues](https://github.com/flathub/com.visualstudio.code/issues/29) 中的 [apsrcreatix](https://github.com/apsrcreatix) 大佬给出的解决方案；感谢原作者的分享
1. 首先确定 log 中报错为以下内容，方可继续操作

    ```
    May 28, 2024 06:46:44.000 [139632948570936] ERROR - [Req#184/Transcode/ipb4thtpwg71j3z4nigp75k7/96a2561c-30bb-4885-98ae-ad63e3290f89] [truehd_eae @ 0x7f9ed3441940] EAE timeout! EAE not running, or wrong folder? Could not read ‘/tmp/pms-20fb6ae1-5ba6-429b-b623-0b0dc443f00b/EasyAudioEncoder/Convert to WAV (to 8ch or less)/ipb4thtpwg71j3z4nigp75k7_373-0-0.wav
    ```
    ```
    May 28, 2024 06:46:44.001 [139632892279608] ERROR - [Req#196/Transcode/ipb4thtpwg71j3z4nigp75k7/96a2561c-30bb-4885-98ae-ad63e3290f89] [truehd_eae @ 0x7f9ed3441940] error reading output: -5 (I/O error)
    ```
    ```
    May 28, 2024 06:46:44.001 [139632885189432] ERROR - [Req19b/Transcode/ipb4thtpwg71j3z4nigp75k7/96a2561c-30bb-4885-98ae-ad63e3290f89] Error while decoding stream **0:1:** I/O error
    ```
2. 解决方案

    1. 进入 SSH 并进入 root 用户

        ```powershell
        sudo -i
        ```
        ​![](https://ca6d7cae.telegraph-image-6yx.pages.dev/file/ed65b9838f3ae5cf7cd19.png)​
    2. 打开并编辑 sysctl.conf 文件

        1. 编辑 sysctl.conf 文件

            ```powershell
            vim /etc/sysctl.conf
            ```
        2. 在该文本中加入以下内容

            ```ini
            fs.inotify.max_user_watches=524288
            ```
            ​![](https://ca6d7cae.telegraph-image-6yx.pages.dev/file/5e01802ad21d71de27586.png)​
    3. 重启系统

        ```powershell
        reboot
        ```
3. 再打开 PLEX 时，已经可以正常硬件转码
