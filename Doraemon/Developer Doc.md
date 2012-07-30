百宝袋开发指南（开发者版本）
================
1. 豌豆荚的百宝袋概述
----------

    百宝袋是一种新的扩展机制，可以快速帮助开发者简单、自动、批量化的把各个内容站接入到豌豆荚 Windows 版。
    对开发者而言，这是一个良性的生态系统，拥有千万用户的豌豆荚将为开发者提供免费的推广平台。
    在这里，开发者不需要担心如何寻找用户、如何优化SEO、如何进行品牌推广，百宝袋开放平台将给开发者带来网站流量、下载量、用户数、活跃度、品牌口碑。
    如果您是一位开发者，欢迎您加入豌豆荚开发者交流群：250241844（申请时请表明自己的开发者身份哈）

2. 扩展系统开发说明（开发者详读）
----------

    每一个扩展对应着一个内容站。扩展系统使开发者有能力快速、大量的提供适合展现在豌豆荚的内容。

### 2.1 如果您是网站站长
* MicroData介绍：文档《[MicroData]》
* Manifest.json介绍：文档《[manifest files]》

### 2.2 如果您是第三方开发者
* Manifest.json介绍：文档《[manifest files]》
* Download介绍：文档《[Download Link]》

### 2.3 目前扩展中webkit/css支持的特性（通用）
* 《[Wandoujia Supported Specifications]》

### 2.4 开发扩展系统时Content Script的Guideline
* 页面宽度修改为适应豌豆荚的默认宽度：780px（考虑会有滚动条，建议控制在760px内）

* 新扩展不允许篡改已经在线上的其它开发者开发的扩展

* 新扩展不允许山寨或完全抄袭线上已有扩展

* 页面中的主要内容可调用豌豆荚的 Download API （可下载资源应该遵循microdata中定义的格式，否则无法下载）进行下载，不支持的部分应打开外部浏览器(target="_default")或予以隐藏

* 如果是难以隐藏的站外链接，直接打开外部浏览器(target="_default")

* manifest中字段：name、description为用户可见的内容，必须有完整的文案描述

* 原则上扩展的页面尊重原内容站的页面构成，这里面包括原内容站的登录、广告、分享、评论等等，对这些内容的去留由开发者在开发过程中自行决定，但如果保留，需要保证其在豌豆荚能够正常work 

* manifest.json匹配规则禁止使用http://\*/\*

* 扩展包必须包含72*72的图标

* 扩展包的文件格式必须是UTF-8编码（无BOM）

* 下载时任务管理器中的任务名称不允许出现“未名名称”或乱码字符

* 若扩展是涉及动态数据，数据须是真实数据，不可用假数据

* 如果出现特殊情况跳转到了一个非内容页，可以通过后退回来

* 页面内的浮出层，不做特殊处理

* content-type 的主要类型(特殊类型的格式需要特殊约定):

    - {"application", "apps", "apk"},
    - {"application/vnd.android.package-archive", "apps", "apk"},
    - {"image", "photo", "*"},
    - {"image/jpeg", "photo", "jpg"},
    - {"image/png", "photo", "png"},
    - {"image/bmp", "photo", "bmp"},
    - {"image/tiff", "photo", "tiff"},
    - {"video", "video", "*"},
    - {"video/mp4", "video", "mp4"},
    - {"audio", "music", "*"},
    - {"audio/mp3", "music", "mp3"},
    - {"book", "book", "*"},
    - {"file", "file", "*"},

3. 百宝袋扩展Sample
---------

###3.1 一个百宝袋扩展必须要包含一个manifest.json文件，下面是一个例子：


    {
        "name": "应用搜索",
        "version": "1.0.0.0",
        "description": "豌豆荚应用搜索.",
        "content_scripts": [
        {
            "matches":["http://*.wandoujia.com/*", "http://*.wandou.in/*"],
            "run_at": "document_end",
            "js": ["jquery-1.7.min.js", "changeDownload.js"],
            "css": ["contentcss.css"],
            "all_frames":false
        }
        ],
        "icons": {
            "12": "icon12.png",
            "72": "icon72.png"
        },
        "app": {
            "launch": {
                "web_url": "http://apps.wandoujia.com/"
            }
            "navigation": [
            {
                "label": "全部应用",
                "web_url": "http://apps.wandoujia.com/category?id=app"
            },
            {
                "label": "全部游戏",
                "web_url": "http://apps.wandoujia.com/category?id=game"
            },
            {
                "label": "装机必备",
                "web_url": "http://apps.wandoujia.com/install"
            },
            {
                "label": "榜单家族",
                "web_url": "http://apps.wandoujia.com/top"
            },
            {
                "label": "豌豆荚设计奖",
                "web_url": "http://awardtest.wandoujia.com/p/list"
            }
            ]
        }
    }

如果manifest.json文件中用到了其他文件，比如*.js, *.css等，也需要在这个目录中创建这些文件。
这些文件可以使用相对路径和绝对路径。

本例中需要的文件列表如下：

    manifest.json
    jquery-1.7.min.js
    changeDownload.js
    contentcss.css
    icon16.png
    icon72.png

下载sample包：[sample package]

4. 百宝袋开发工具介绍
-----------

### 4.1 前提
进入开发者版本的前提是必须注册豌豆荚账号，并在豌豆荚Windows客户端登录：
![登录豌豆荚Windows客户端][register]

### 4.2 进入开发者模式
![进入开发者模式][settings_1]
![进入开发者模式][settings_2]

### 4.3 管理扩展
![进入管理扩展页面][manage]

### 4.4 加载本地扩展
![加载本地扩展][load_extensions_1]
![加载本地扩展][load_extensions_2]
![加载本地扩展][load_extensions_3]

### 4.5 调试
![页面调试][debug_1]
![页面调试][debug_2]

### 4.6 刷新扩展
点击“更新扩展”即可重新加载本地扩展。
需要注意的是，有可能需要手动刷新网页。

![刷新扩展][reload_extension]

### 4.7 打包扩展
点击“打包扩展”，即可立即生成打包好的\*.wdx文件，同时会打开该文件的位置。

![打包扩展][package_extension]

### 4.7 扩展上线
* 开发者扩展开发完毕，可以提交到豌豆荚扩展中心：http://developer.wandoujia.com/
* 扩展的上线流程如下：

![打包扩展][extension_online]

* 注：

 - 第一次提交扩展包后，豌豆荚的审核时间是1～3天，审核通过之后会在当天上线。
 - 扩展包因失效（改版、服务不稳定、下线、法律原因）或违反豌豆荚规定下线，待扩展包恢复正常之后，须观察24小时，开发者
   需按上线流程重新申请上线。
 - 开发者将扩展包升级之后，需要重新走审核流程。

* 审核及扩展下线原则：
 - 扩展的内容包括色情，淫秽，擦边球等成人内容
 - 扩展的内容涉及或影射政治敏感信息及内容
 - 扩展内含病毒
 - 扩展的内容存在误导欺骗用户的行为或者乱扣费、暗扣费
 - 扩展存在严重的bug，不能够正常使用
 - 扩展未遵守豌豆荚Content Script的Guideline规范
 - 扩展因内容站改版、开发者下线、法律限制等导致失效

  [manifest files]: https://github.com/wandoulabs/developer-documents/blob/master/Doraemon/Manifest%20Files.md
  [Download Link]: https://github.com/wandoulabs/developer-documents/blob/master/Doraemon/Download%20Link.md
  [MicroData]: https://github.com/wandoulabs/developer-documents/blob/master/Microdata/App%20Microdata.md
  [Wandoujia Supported Specifications]: https://github.com/wandoulabs/developer-documents/blob/master/Doraemon/Wandoujia%20Supported%20Specifications.md
  [register]: https://github.com/wandoulabs/developer-documents/blob/master/Doraemon/pictures/register.jpg?raw=true
  [settings_1]: https://github.com/wandoulabs/developer-documents/blob/master/Doraemon/pictures/settings_1.jpg?raw=true
  [settings_2]: https://github.com/wandoulabs/developer-documents/blob/master/Doraemon/pictures/settings_2.jpg?raw=true
  [manage]: https://github.com/wandoulabs/developer-documents/blob/master/Doraemon/pictures/manage.jpg?raw=true
  [load_extensions_1]: https://github.com/wandoulabs/developer-documents/blob/master/Doraemon/pictures/load_extensions_1.jpg?raw=true
  [load_extensions_2]: https://github.com/wandoulabs/developer-documents/blob/master/Doraemon/pictures/load_extensions_2.jpg?raw=true
  [load_extensions_3]: https://github.com/wandoulabs/developer-documents/blob/master/Doraemon/pictures/load_extensions_3.jpg?raw=true
  [debug_1]: https://github.com/wandoulabs/developer-documents/blob/master/Doraemon/pictures/debug_1.jpg?raw=true
  [debug_2]: https://github.com/wandoulabs/developer-documents/blob/master/Doraemon/pictures/debug_2.jpg?raw=true
  [reload_extension]: https://github.com/wandoulabs/developer-documents/blob/master/Doraemon/pictures/reload_extension.jpg?raw=true
  [package_extension]: https://github.com/wandoulabs/developer-documents/blob/master/Doraemon/pictures/package_extension.jpg?raw=true
  [extension_online]: https://github.com/wandoulabs/developer-documents/blob/master/Doraemon/pictures/extension_online.jpg?raw=true
  [sample package]: https://github.com/wandoulabs/developer-documents/blob/master/Doraemon/files/search.zip?raw=true