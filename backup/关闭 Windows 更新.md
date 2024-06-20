### 关闭 Windows 更新

1. 暂停更新 3000 天

    键盘输入`Win+R`，在框内输入以下内容并回车，然后重启电脑

    ```
    reg add "HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\WindowsUpdate\UX\Settings" /v FlightSettingsMaxPauseDays /t reg_dword /d 3000 /f
    ```

    ![](https://ca6d7cae.telegraph-image-6yx.pages.dev/file/0f02bbccd537e4d8f394b.png)

2. 使用软件关闭更新

    1. 下载软件 [[Windows Update Blocker](https://pcdiy.xyz/d/Cloudflare%20R2/Windows/Windows_%E7%A6%81%E6%AD%A2%E6%9B%B4%E6%96%B0/Windows_Update_Blocker_v1.8.7z?sign=XSZjq2MXSoVMMkgLqJlgF53xby2lBmiFPm0168Obw84=:0)](https://pcdiy.xyz/d/Cloudflare%20R2/Windows/Windows_%E7%A6%81%E6%AD%A2%E6%9B%B4%E6%96%B0/Windows_Update_Blocker_v1.8.7z?sign=XSZjq2MXSoVMMkgLqJlgF53xby2lBmiFPm0168Obw84=:0)
    2. **解压**软件后，右键**管理员运行**​`Wub_x64.exe`

        ![](https://ca6d7cae.telegraph-image-6yx.pages.dev/file/aaecd64d54f88e954e3a7.png)
    3. 按照如图所示设置后重启电脑

        ![](https://ca6d7cae.telegraph-image-6yx.pages.dev/file/38e8c802fbd5cc4b66ae1.png)