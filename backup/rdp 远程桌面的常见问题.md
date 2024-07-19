# 如何开启

​`Windows 设置`​ - `系统`​ - `远程桌面`​ - 勾选 `启用远程桌面`​

​![](https://img.pcdiy.xyz/file/6e2c65bec376a4bb0dfc2.png)​

# 某些设置由你的组织管理

## 问题截图

​![](https://img.pcdiy.xyz/file/f7edf521fd3eddabed3f6.png)​

## 解决方案

1. ​`win + R`​ 输入 `gpedit.msc`​ ，点击 `确定`​

    ​![](https://img.pcdiy.xyz/file/d930ca650bcf3d3cf3390.png)​
2. 依次打开 `计算机配置`​ - `管理模块`​ - `Windows组件`​ - `远程桌面服务`​ - `远程桌面会话主机`​ - `连接`​
3. 在右边找到 `允许用户通过使用远程桌面服务进行远程连接`​ ，右键点击 `编辑`​ - 设置为 `启动`​，最后点击 `应用`​

    ​![](https://img.pcdiy.xyz/file/a70bac33c7147dff1b81a.png)​

# 实现免密码远程控制

0. 通常来说，默认配置下不允许不设置密码进行远程控制，以下给出解决方案
1. ​`win + R`​ 输入 `secpol.msc`​ ，点击 `确定`​

    ​![](https://img.pcdiy.xyz/file/849fff65e738f72236f97.png)​
2. 依次打开 `安全设置`​ - `本地策略`​ - `安全选项`​

    ​![](https://img.pcdiy.xyz/file/7374429b79cd06acf4dce.png)​
3. 右边往下拉，找到 `帐户：使用空密码的本地帐户只允许`​ ，双击，选择 `已禁用`​

    ​![](https://img.pcdiy.xyz/file/4e94280ae7769d0ed43d5.png)​

# 出现身份验证错误，无法连接到本地安全机构

## 问题截图

​![](https://img.pcdiy.xyz/file/2138aa6dd35c042ec44f1.png)​

## 解决方案

### 方法一

1. ​`win + R`​ 输入 `secpol.msc`​ ，点击 `确定`​

    ​![](https://img.pcdiy.xyz/file/849fff65e738f72236f97.png)​
2. 依次打开 `安全设置`​ - `本地策略`​ - `安全选项`​，右边往下拉，找到 `网络访问：本地账户的共享和安全模型`​ ，双击，选择 `经典 - 对本地用户进行身份验证，不改变其本来身份`​

    ​![](https://img.pcdiy.xyz/file/a1cf6f99bee4d048c05e3.png)​

### 方法二

1. ​`win + R`​ 输入 `gpedit.msc`​ ，点击 `确定`​

    ​![](https://img.pcdiy.xyz/file/d930ca650bcf3d3cf3390.png)​
2. 依次打开 `计算机配置`​ - `管理模块`​ - `Windows组件`​ - `远程桌面服务`​ - `远程桌面会话主机`​ - `安全`​
3. 在右边找到 `要求使用网络级别的身份验证对远程连接的用户进行身份验证`​ ，右键点击 `编辑`​ - 设置为 `已禁用`​，最后点击 `应用`​

    ​![](https://img.pcdiy.xyz/file/16c5ab95c196b9236a58e.png)​

‍
