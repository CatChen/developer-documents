# Media Microdata

## 概述

媒体微格式的主要作用是让豌豆荚的浏览器能够识别出第三方页面上的一段 HTML 描述的是一个媒体文件（文本、图片、音频、视频），在用户想要下载时为用户提供更丰富的信息。

## 引用文件

所有使用此微格式的页面都引用同一个 JavaScript 文件。

	<script type="text/javascript" src="http://cdn-prefix.wandoujia.com/path-prefix/micro-format.js">

## 微格式

豌豆荚对符合以下类型的微格式进行处理：

* [Article](http://schema.org/Article)
	* [BlogPosting](http://schema.org/BlogPosting)
	* [NewsArticle](http://schema.org/NewsArticle)
	* [ScholarlyArticle](http://schema.org/ScholarlyArticle)
* [MediaObject](http://schema.org/MediaObject)
	* [AudioObject](http://schema.org/AudioObject)
	* [ImageObject](http://schema.org/ImageObject)
	* [MusicVideoObject](http://schema.org/MusicVideoObject)
	* [VideoObject](http://schema.org/VideoObject)

对于 Article 及其派生类，豌豆荚会尝试在页面上抽取文本提供给用户下载。对于 MediaObject 及其派生类，豌豆荚会尝试在页面上寻找链接，将链接目标提供给用户下载。

### Article

对于 Article 及其派生类来说，只有 `articleBody` 属性是必须的，其他属性可以为豌豆荚提供更多信息。

	<div itemscope itemtype="http://schema.org/Article">
		<span itemprop="name">My speech</span>
		by <span itemprop="author">Cat Chen</span>
		<div itemprop="articleBody">
			<p>Blah blah blah...</p>
			<p>Blah blah blah...</p>
			<p>Blah blah blah...</p>
		</div>
	</div>

#### *\[itemprop=articleBody]

文章正文内容。

### MediaObject

对于 MediaObject 及其派生类来说，只有 `contentUrl` 属性是必须的，其他属性可以为豌豆荚提供更多信息。

	<div itemscope itemtype="http://schema.org/AudioObject">
		<span itemprop="name">12oclock_girona.mp3</span>
		<script type="text/javascript">
			var fo = new FlashObject(
				"http://google.com/flash/preview-player.swf",
				"flashPlayer_719", "358", "16", "6", "#FFFFFF");
			fo.addVariable("url","http://media.freesound.org/"
				+ "data/0/previews/"
				+ "719__elmomo__12oclock_girona_preview.mp3");
			fo.addVariable("autostart", "0");
			fo.write("flashcontent_719");
		</script>
		<meta itemprop="encodingFormat" content="mp3" />
		<meta itemprop="contentURL"
			content="http://media.freesound.org/data/0/previews/719__elmomo__12oclock_girona_preview.mp3" />
		<span class="description">
			<meta itemprop="duration" content="T0M15S" />
			<span itemprop="description">Recorded on a terrace of Girona a sunday morning</span>
		</span>
	</div>

#### *\[itemprop=contentUrl]

媒体文件的下载（播放）地址。

### 其它

增加其他属性可以为豌豆荚提供更丰富的展示信息。将上述类型作为输入嵌入到其他类型当中，其他类型的属性也能为豌豆荚提供更丰富的信息。例如将 VideoObject 嵌入到 Movie 中，豌豆荚可以通过 Movie 的属性获取到关于 VideoObject 的更多信息。

豌豆荚具体支持的类型和信息如下：

#### *\[itemprop=name]

媒体资源的名称，适用于任何类型的媒体。

#### *\[itemprop=contentSize]

媒体资源的下载文件体积，适用于 MediaObject 及其派生类。

#### *\[itemprop=encodingFormat]

媒体资源的编码格式，适用于 MediaObject 及其派生类。

#### *\[itemprop=icon]

缩略图地址，适用于任何类型的媒体。

#### *\[itemprop=thumbnailUrl]

缩略图地址，适用于任何类型的媒体。

#### *\[itemprop=thumbnail]

缩略图对象，适用于 ImageObject 和 VideoObject。豌豆荚只读取里面的 `*\[itemprop=image]` 属性。

#### *\[itemprop=byArtist]

表演者，适用于通过 encoding 包含了 MediaObject 及其派生类的 MusicRecording。
