百宝袋开发指南（开发者版本）
================
1. 豌豆荚的百宝袋概述
----------

    百宝袋是一种新的扩展机制，帮助豌豆荚简单、自动、批量化的把各个内容站接入到豌豆荚 Windows 版。
    对开发者而言，这是一个良性的生态系统，拥有千万用户的豌豆荚将为开发者提供免费的推广平台。
    在这里，不需要担心如何寻找用户、如何优化SEO、如何进行品牌推广，百宝袋开放平台将给开发者带来网站流量、下载量、用户数、活跃度、品牌口碑。

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

* 页面中的主要内容可调用豌豆荚的 Download API （可下载资源应该遵循microdata中定义的格式，否则无法下载）进行下载，不支持的部分应打开外部浏览器或予以隐藏

* 如果是难以隐藏的站外链接，直接打开外部浏览器

* 原则上扩展的页面尊重原内容站的页面构成，这里面包括原内容站的登录、广告、分享、评论等等，对这些内容的去留由开发者在开发过程中自行决定，但如果保留，需要保证其在豌豆荚能够正常work 

* manifest.json匹配规则禁止使用http://*/*

* 扩展包的文件格式必须是UTF-8编码（无BOM）

* 如果出现特殊情况跳转到了一个非内容页，可以通过后退回来

* 页面内的浮出层，不做特殊处理

* content-type 的主要类型(特殊类型的格式需要特殊约定):

    - {"application/vnd.android.package-archive", "apps", "apk"},
    - {"image/jpeg", "photo", "jpg"},
    - {"image/png", "photo", "png"},
    - {"image/bmp", "photo", "bmp"},
    - {"image/tiff", "photo", "tiff"},
    - {"video/mp4", "video", "mp4"},
    - {"audio/mp3", "music", "mp3"},

3. 百宝袋扩展Sample
---------
    {
        "name": "应用搜索",             // 默认将会是豌豆荚侧边栏中显示的名称
        "version": "1.0.0.0",
        "description": "把豌豆荚应用搜索老的下载API转化成新的下载方式。",
        "content_scripts": [
        {
            "matches":["http://*.wandoujia.com/*", "http://*.wandou.in/*"],
            "run_at": "document_end",
            "js": ["jquery-1.7.min.js", "changeDownload.js"],
            "css": ["contentcss.css"],
            "all_frames":false
        }
        ],
        "app": {
            "launch": {
                "web_url": "http://apps.wandoujia.com/"          // 点击侧边栏之后加载的页面
            },
            "icons": {          // 图标
                "12": "icon12.png",   // 侧边栏显示的图标
                "72": "icon72.png"    // 更多市场显示时会用到的图标
            },
            "navigation": [        // 以下为顶部导航，最多支持8个
            {
                "label": "全部应用",          // 顶部导航名称
                "web_url": "http://apps.wandoujia.com/category?id=app" // 顶部导航对应的页面
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
![加载本地扩展][load_extensions]

### 4.5 调试
![页面调试][debug_1]
![页面调试][debug_2]

### 4.6 刷新扩展
![刷新扩展][refresh_extension]

### 4.7 打包扩展
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
  [MicroData]: https://github.com/wandoulabs/developer-documents/blob/master/Doraemon/Download%20Link.md
  [Wandoujia Supported Specifications]: https://github.com/wandoulabs/developer-documents/blob/master/Doraemon/Wandoujia%20Supported%20Specifications.md
  [register]: https://github.com/wandoulabs/developer-documents/blob/master/Doraemon/pictures/register.jpg?raw=true
  [settings_1]: https://github.com/wandoulabs/developer-documents/blob/master/Doraemon/pictures/settings_1.jpg?raw=true
  [settings_2]: https://github.com/wandoulabs/developer-documents/blob/master/Doraemon/pictures/settings_2.jpg?raw=true
  [manage]: https://github.com/wandoulabs/developer-documents/blob/master/Doraemon/pictures/manage.jpg?raw=true
  [load_extensions]: https://github.com/wandoulabs/developer-documents/blob/master/Doraemon/pictures/load_extensions.jpg?raw=true
  [debug_1]: https://github.com/wandoulabs/developer-documents/blob/master/Doraemon/pictures/debug_1.jpg?raw=true
  [debug_2]: https://github.com/wandoulabs/developer-documents/blob/master/Doraemon/pictures/debug_2.jpg?raw=true
  [refresh_extension]: https://github.com/wandoulabs/developer-documents/blob/master/Doraemon/pictures/refresh_extension.jpg?raw=true
  [package_extension]: https://github.com/wandoulabs/developer-documents/blob/master/Doraemon/pictures/package_extension.jpg?raw=true
  [extension_online]: https://github.com/wandoulabs/developer-documents/blob/master/Doraemon/pictures/extension_online.jpg?raw=true