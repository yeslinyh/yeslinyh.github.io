# 如何部署

```powershell
docker run -d \
	--name=alist \
	--restart=unless-stopped \
	-v /home/alist:/opt/alist/data \
	-p 5244:5244 \
	-e PUID=0 \
	-e PGID=0 \
	-e UMASK=022 \
	xhofe/alist:latest
```

# 默认账户密码

用户名: `admin`​

密码设置命令：

```powershell
docker exec -it alist ./alist admin set XXXXXX
```

其中 `alsit`​ 为 `容器名`​ ，与 `--name=alist`​ 设置的一致

# `nginx`​ 文件的设置 (非必要，用于解决无法上传大文件的问题)

```nginx
location / {
  proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
  proxy_set_header X-Forwarded-Proto $scheme;
  proxy_set_header Host $http_host;
  proxy_set_header X-Real-IP $remote_addr;
  proxy_set_header Range $http_range;
	proxy_set_header If-Range $http_if_range;
  proxy_redirect off;
  proxy_pass http://127.0.0.1:5244;
  # the max size of file to upload
  client_max_body_size 20000m;
}
```

# 页面美化

## 自定义头部

1. 自定义 API 背景

    ```javascript
    /*白天背景图*/
    .hope-ui-light{
      background-image: url("https://bing.img.run/1920x1080.php") !important;
      background-repeat:no-repeat;background-size:cover;background-attachment:fixed;background-position-x:center;
    }
    /*夜间背景图*/
    .hope-ui-dark {
        background-image: url("https://bing.img.run/1920x1080.php") !important;
        background-repeat:no-repeat;background-size:cover;background-attachment:fixed;background-position-x:center;
    }
    ```

    其中，`https://bing.img.run/1920x1080.php`​ 可自定义 `图片`​ 或 `api`​
2. 列表透明

    ```javascript
    /*主列表白天模式透明*/
     .obj-box.hope-stack.hope-c-dhzjXW.hope-c-PJLV.hope-c-PJLV-igScBhH-css {
        background-color: rgba(255, 255, 255, 0.5) !important;
    }
    /*主列表夜间模式透明*/
     .obj-box.hope-stack.hope-c-dhzjXW.hope-c-PJLV.hope-c-PJLV-iigjoxS-css {
        background-color:rgb(0 0 0 / 50%) !important;
    }
    /*readme白天模式透明*/
     .hope-c-PJLV.hope-c-PJLV-ikSuVsl-css {
        background-color: rgba(255, 255, 255, 0.5) !important;
    }
    /*readme夜间模式透明*/
     .hope-c-PJLV.hope-c-PJLV-iiuDLME-css {
        background-color:rgb(0 0 0 / 50%) !important;
    }

    /*顶部右上角切换按钮透明*/
     .hope-ui-light .hope-c-ivMHWx-hZistB-cv.hope-icon-button {
        background-color: rgba(255, 255, 255, 0.5) !important;
    }
    .hope-ui-dark .hope-c-ivMHWx-hZistB-cv.hope-icon-button {
        background-color:rgb(0 0 0 / 50%) !important;
    }

    /*右下角侧边栏按钮透明 第一个是白天 第二个是夜间*/
     .hope-ui-light .hope-c-PJLV-ijgzmFG-css {
        background-color: rgba(255, 255, 255, 0.5) !important;
    }
    .hope-ui-dark .hope-c-PJLV-ijgzmFG-css {
        background-color:rgb(0 0 0 / 50%) !important;
    }

    /*白天模式代码块透明*/
     .hope-ui-light pre {
        background-color: rgba(255, 255, 255, 0.1)!important;
    }
    /*夜间模式代码块透明*/
     .hope-ui-dark pre {
        background-color: rgba(255, 255, 255, 0)!important;
    }

    /*左侧侧边栏目录*/
    /*白天模式*/
     .hope-ui-light .hope-c-PJLV-ieGWMbI-css {
        background: rgba(255, 255, 255, 0.5) !important;
    }
    /*夜间模式*/
     .hope-ui-dark .hope-c-PJLV-ieGWMbI-css {
        background-color:rgb(0 0 0 / 50%) !important;
    }

    /* 返回顶部 */
     .hope-c-PJLV-ihVEsOa-css {
        background: rgba(255, 255, 255, 0.5) !important;
    }
    .hope-ui-dark .hope-c-PJLV-ihVEsOa-css {
        background-color:rgb(0 0 0 / 50%) !important;
    }

    /*正常情况未使用吸附功能*/
    /*顶部*/
     .hope-c-PJLV-ikaMhsQ-css {
        background: rgba(255, 255, 255, 0) !important;
    }
    /*导航条*/ 
    /*白天模式*/
     .hope-ui-light .hope-c-PJLV-idaeksS-css {
        background-color: rgba(255, 255, 255, 0.5) !important;
        border-radius: var(--hope-radii-xl) !important;
    }
    /*夜间模式*/
     .hope-ui-dark .hope-c-PJLV-idaeksS-css {
        background-color:rgb(0 0 0 / 50%) !important;
        border-radius: var(--hope-radii-xl) !important;
    }
    /* 吸附到页面顶部 */
    /*顶部*/
     .hope-c-PJLV-icWrYmg-css {
        background: rgba(255, 255, 255, 0) !important;
    }
    /*导航条*/
     .hope-c-PJLV-icKsjdm-css::after {
        background: rgba(255, 255, 255, 0) !important;
    }
    /*白天模式*/
     .hope-ui-light .hope-c-PJLV-icKsjdm-css {
        background-color: rgba(255, 255, 255, 0.5) !important;
        border-radius: var(--hope-radii-xl) !important;
    }
    /*夜间模式*/
     .hope-ui-dark .hope-c-PJLV-icKsjdm-css {
        background-color:rgb(0 0 0 / 50%) !important;
        border-radius: var(--hope-radii-xl) !important;
    }

    /*仅吸附导航栏*/
    /*导航条*/
     .hope-c-PJLV-ifdXShc-css::after {
        background: rgba(255, 255, 255, 0) !important;
    }
    /*白天模式*/
     .hope-ui-light .hope-c-hrsMRY {
        background-color: rgba(255, 255, 255, 0.5) !important;
        border-radius: var(--hope-radii-xl) !important;
    }
    /*夜间模式*/
     .hope-ui-dark .hope-c-hrsMRY {
        background-color:rgb(0 0 0 / 50%) !important;
        border-radius: var(--hope-radii-xl) !important;
    }
    ```
3. 字体相关

    * 环境变量

      ```html
      <!--引入字体，全局字体使用-->
      <link rel="stylesheet" href="https://npm.elemecdn.com/lxgw-wenkai-webfont@1.1.0/lxgwwenkai-regular.css" />

      <!-- Font6，自定义底部使用和看板娘使用的图标和字体文件-->
      <link type='text/css' rel="stylesheet" href="https://npm.elemecdn.com/font6pro@6.3.0/css/fontawesome.min.css" media='all'>
      <link href="https://npm.elemecdn.com/font6pro@6.3.0/css/all.min.css" rel="stylesheet">
      ```
    * 替换字体

      ```javascript
      /*全局字体*/
       * {
          font-family:LXGW WenKai
      }
      * {
          font-weight:bold
      }
      body {
          font-family: LXGW WenKai;
      }
      ```

## 美化 自定义内容

1. 延迟加载

    ```html
    <!--延迟加载-->
    <!--如果要写自定义内容建议都加到这个延迟加载的范围内-->
    <div id="customize" style="display: none;">
        <div>
    	<!--自定义内容都应加在该部分-->
        </div>
    <!--延迟加载配套使用JS-->
    <script>
        let interval = setInterval(() => {
            if (document.querySelector(".footer")) {
                document.querySelector("#customize").style.display = "";
                clearInterval(interval);
            }
        }, 200);
    </script>
    ```
2. 底部自定义

    ```html
            <br />
            <center class="dibu">

                <div style="font-size: 20px; font-weight: bold;">
                    <span class="nav-item">
                        <a class="nav-link" href="http://qm.qq.com/cgi-bin/qm/qr?_wv=1027&k=vS4Jyt8wSecObdv7LNLtwxP7U_SBIeqg&authKey=5UXdAh1sOrSevtuUpHJOZ02BjE9STWrEXdzwArqBQ3ooeJmeUtNei84%2BGmFbpt4J&noverify=0&group_code=885781238"
                            target="_blank">
                            <i class="fab fa-qq" style="color:#FE9900" aria-hidden="true">
                            </i>
                            QQ |
                        </a>
                    </span>
                    <span class="nav-item">
                        <a class="nav-link" href="https://kdocs.cn/l/cbHE1IEOZyOj" target="_blank">
                            <i class="fa-duotone fa-envelope-open" style="color:#FE9900" aria-hidden="true">
                            </i>
                            文档 |
                        </a>
                    </span>
                    <span class="nav-item">
                        <a class="nav-link" href="https://blog.pcdiy.xyz" target="_blank">
                            <i class="fas fa-edit" style="color:#FE9900" aria-hidden="true">
                            </i>
                            博客 |
                        </a>
                    </span>
                    <span class="nav-item">
                        <a class="nav-link" href="https://tieba.baidu.com/f?kw=diy%E9%9B%B6%E4%BB%B6%E7%BB%84%E8%A3%85&ie=utf-8" target="_blank">
                            <i class="fas fa-comment-lines" style="color:#FE9900;" aria-hidden="true">
                            </i>
                            贴吧 |
                        </a>
                    </span>
                    <span class="nav-item">
                        <a class="nav-link" href="https://nezha.pcdiy.xyz" target="_blank">
                            <i class="fa fa-tachometer" style="color:#FE9900;" aria-hidden="true">
                            </i>
                            探针 |
                        </a>
                    </span>
                    <span class="nav-item">
                        <a class="nav-link" href="https://bing.pcdiy.xyz" target="_blank">
                            <i class="fa fa-wifi" style="color:#FE9900" aria-hidden="true">
                            </i>
                            AI |
                        </a>
                    </span>
                    <!--后台入口-->
                    <span class="nav-item">
                        <a class="nav-link" href="/@manage" target="_blank">
                            <i class="fa-solid fa-folder-gear" style="color:#FE9900;" aria-hidden="true">
                            </i>
                            管理 |
                        </a>
                    </span>
                    <!--版权，请尊重作者-->
                    <span class="nav-item">
                        <a class="nav-link" href="https://github.com/Xhofe/alist" target="_blank">
                            <i class="fa-solid fa-copyright" style="color:#FE9900;" aria-hidden="true">
                            </i>
                            版权
                        </a>
                    </span>
    				<br />
    ```
3. 去掉 `power by`​ 和 `管理`​

    ```html
    	<!---去掉底部文字--->
    	<style
    		type="text/css"> .footer { 
    		display: none !important; } 
    	</style>
    ```