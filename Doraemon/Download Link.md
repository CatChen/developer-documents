# Download Link

## 概述

这个文档说明豌豆荚 Windows 版百宝袋如何识别下载链接，以及如何从下载链接中提取目标文件的相关信息（meta data）。

一个典型的百宝袋下载链接应该是这样子的：（请注意提供给豌豆荚 Windows 版使用的参数键值对放在 `#` 井号后面，且不需要做url encoding，而非 `?` 问号后面。）

	<a href="app.apk#name=app&image=%2Fimages%2Fapp-icon.png" rel="download">Download</a>

豌豆荚 Windows 版百宝袋会对 `a` 标签中的如下信息作出响应：

## download="filename.ext"

`download="filename.ext"` 属性向豌豆荚表明这个链接的目标用于下载，同时给出下载时所建议使用的文件名。(不需要做url encoding)

在一般情况下，豌豆荚会根据链接目标内容的 content-type 属性做出判断，到底应该是下载还是直接展示。但如果要想要下载的内容是纯文本或者 HTML，豌豆荚的默认行为会是直接展示，这时候可以通过 `download="filename.ext"` 来提示豌豆荚将默认行为变更为下载，同时通过属性取值（`"filename.ext"` 部分）给出建议使用的文件名。对于默认行为已经是下载的链接目标，这个属性同样能用于给出建议使用的文件名。

## rel="download"

_DEPRECATED!_

`rel="download"` 是一个已经不再建议使用的属性，它曾经的作用与 `download="filename.ext"` 相似，用于向豌豆荚声明链接目标应该用于下载而非直接显示。

## href="...\#key1=value1&key2=value2"

豌豆荚可以通过 `href` 属性获取到下载地址，但无法获取到下载内容的相关信息（meta data），例如说是应用的图标。这些信息可以以键值对（key-value）的形式在 `#` 井号（注意不是 `?` 问号）后面的锚点传递给豌豆荚，使用起来类似于查询字符串（query string）。

其中有一些取值是跟 HTTP header 取值同名的，这些取值用于补充下载目标 HTTP header 不提供的信息。例如说，如果下载目标不提供 `content-disposition` header，且 URL 不包括文件名信息（如 `http://example.com/download?id=123`），浏览器就没办法获得文件名，这时候锚点后的 `content-disposition` 属性就可以用于提供此信息。

需要注意的是，无论何时 HTTP header 的同名取值总会覆盖锚点后的属性。

豌豆荚对可以处理锚点里面的这些键值：

### name

名称。会显示在资源管理界面和下载任务管理器。(不需要做url encoding)

如果下载链接所在的网页上使用了 microdata，在锚点不提供 `name` 属性时，该属性从同一个 `itemscope` 内的 `*[itemprop=name]` 元素上获取。

### image

图标。会显示在资源管理界面和下载任务管理器。(不需要做url encoding)

如果下载链接所在的网页上使用了 microdata，在锚点不提供 `image` 属性时，该属性从同一个 `itemscope` 内的 `*[itemprop=image]` 或 `*[itemprop=thumbnail] *[itemprop=image]` 或 `*[itemprop=thumbnailUrl]` 元素上获取。

### content-type

文件类型。取值应该为合法的 MIME-type。

### content-length

文件体积。文件在下载过程中如果提供了 HTTP header 的 `content-length` 属性，则以 HTTP header 属性为准。文件下载后，以实际存储的文件体积为准。会显示在资源管理界面和下载任务管理器。

如果下载链接所在的网页上使用了 microdata，在锚点不提供 `content-length` 属性时，该属性从同一个 `itemscope` 内的 `*[itemprop=fileSize]` 或 `*[itemprop=contentSize]` 元素上获取。

### content-disposition

文件处置方式。必须以 HTTP header 的 `content-disposition` 取值格式提供，即 `attachment; filename="filename.txt"; filepath="/sdcard"; `。

根据[标准](http://www.iana.org/assignments/mail-cont-disp/mail-cont-disp.xml)，`content-disposition` 的取值必须有一个值（value）和任意多个参数（parameter）组成。豌豆荚要求值（value）必须是 `attachment`。豌豆荚支持的参数（parameter）包括 `filename` 和 `filepath`。

#### filename

文件名。豌豆荚在考虑文件保存为什么文件名时，会参考这一参数。如果这一参数不是系统（豌豆荚 Windows 版需要同时考虑 Windows 和 Android）有效的文件名，则豌豆荚会做出必要的调整。(不需要做url encoding)

需要注意的是，在 `filename` 设置的文件名会覆盖在 `download` 设置的文件名，但 HTTP header 设置的文件名依然有最高优先级。

#### filepath

文件路径。豌豆荚在考虑文件保存路径时，会参考这一参数。由于下载资源是提供给 Android 设备使用的，所以这里的文件路径应该基于 Android 文件系统。(不需要做url encoding)

## 1.x 兼容性（豌豆荚2.0以上版本忽略）

为了保持与之前的豌豆荚版本兼容，豌豆荚提供了下面这种下载方式（sample）：

修改js sample：

下载应用（apk）:

    var m = {};
    m.downloadUrl = url; // url
    m.title = title; // title
    window.externalCall('portal', 'appdownload', JSON.stringify([m]));

下载电子书（txt, pdf）:

    var m = {};
    m.url = url; // url
    m.title = title; // title
    window.externalCall('portal', 'book', JSON.stringify([m]));

下载图片（jpg）:

    var m = {};
    m.url = url; // url
    m.title = title; // title
    window.externalCall('photo', 'api_download', JSON.stringify([m]));

下载音乐（mp3）:

    var m = {};
    m.url = url; // url
    m.title = title; // title
    window.externalCall('portal', '-musicurlarray', JSON.stringify([m]));

下载视频（mp4）:

    var m = {};
    m.url = url; // url
    m.title = title; // title
    window.externalCall('portal', '-videourl', JSON.stringify([m]));

这种方式支持批量下载。