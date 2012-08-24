# App Microdata

## 概述

应用微格式的主要作用是让豌豆荚和其它搜索引擎能够识别出网页上的一段 HTML 描述的是一个应用，在用户想要下载和升级应用的时候，为用户提供名称、版本、图标、描述等更丰富的信息。此机制将来会用于：

* 用于一键安装中传递下载相关信息
* 用于搜索爬虫抓取数据时进行识别

## 微格式

	<div itemscope itemtype="http://schema.org/SoftwareApplication" class="download">
		<img itemprop="icon" src="https://ssl.gstatic.com/android/market/com.zeptolab.ctr.paid/hi-124-11" />
		<a itemprop="url" href="">
			<span itemprop="name">Cut the Rope</span>
			(<span itemprop="softwareVersion">1.3</span>)
		</a>
		<div itemprop="description">Cut the Rope, catch a star, and feed Om Nom candy in this award-winning game! The long-awaited hit game has finally arrived at Android!</div>
		<a itemprop="downloadURL" href="">Download</a> (<span itemprop="fileSize">18,123,456</span>)
	</div>

所有跟应用相关的操作都使用 `*[itemscope]` 标签，具体信息由 `class` 属性及里面的 `*[itemprop]` 元素给出。
微格式sample：
* 文档1《[microdata-to-download-link-processor-demo.html]》
* 文档2《[microdata-to-download-link-processor.js]》
              

### class

如果 `class` 包含了 `snp-app-download` 类，豌豆荚客户端将会通过 `packageName` 和 `softwareVersion` 检测用户是否已经拥有此应用的过往版本或最新版本。如果是的话，则会将 `snp-app-download` 更新为 `snp-app-update`（代表可更新）或 `snp-app-downloaded`（代表已下载）。

### *\[itemprop=name]

直接展示给用户看的应用名称。

### *\[itemprop=packageName]

应用包名称。

### *\[itemprop=softwareVersion]

应用版本号。

### *\[itemprop=fileMd5]

应用 apk 文件的 md5 摘要信息。

### *\[itemprop=url]

应用详情页地址。

### *\[itemprop=downloadUrl]

应用 apk 文件下载地址。

### *\[itemprop=description]

直接展示给用户看的应用描述。

### *\[itemprop=icon]

直接展示给用户看的应用图标。

### *\[itemprop=fileSize]

应用 apk 文件体积，用按字节计算的整数表示。

### *\[applicationCategory]

应用类别。

### 其他

除去上述必要的属性外，其它自定义属性可以参考 [Schema.org 的文档](http://schema.org/SoftwareApplication)。



  [microdata-to-download-link-processor-demo.html]:https://github.com/wandoulabs/developer-documents/blob/master/Microdata/microdata-to-download-link-processor-demo.html
  [microdata-to-download-link-processor.js]:https://github.com/wandoulabs/developer-documents/blob/master/Microdata/microdata-to-download-link-processor.js
