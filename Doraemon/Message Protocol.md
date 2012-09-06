# Message Protocol

豌豆荚扩展可以调用豌豆荚操作用户手机联系人、短信、应用等信息，并且也可以通过订阅豌豆荚相关事件以得知上述信息的变更。本文档用于描述扩展与豌豆荚互操作所使用的数据格式。

扩展与豌豆荚通信主要有两种方式，一种是操作资源，另一种是订阅事件。

## 操作资源

	snappea.request({
		resource: "snappea://contacts/1",
		method: "get"
	}, function(response) {
		console.log(response.statusCode);
		console.log(response.data);
	});

扩展操作豌豆荚资源的方式，本质上跟请求一个 URI 的资源无异，最基本的元素是资源（`resource`）与方法（`method`）。返回也跟一个 HTTP 返回类似，状态码（`statusCode`）表示操作结果状态，同时还可能有更详细的返回数据（`data`）。

### 参数和数据

请求除去资源与方法外，还可以带上参数（`meta`）和数据（`data`）。特定资源允许使用的方法及对应参数、数据请参考该资源文档。返回同样可能带有参数（`meta`），这些参数能够帮助你更好地处理返回。

### 方法快捷方式

对资源常见的操作方法都有对应的快捷方式，使得你可以在调用时省略 `method` 属性：

* `snappea.get`
* `snappea.post`
* `snappea.put`
* `snappea['delete']`

## 订阅事件

	snappea.subscribe({
		resource: "snappea://messages/",
	}, function(event) {
		console.log(event.data);	
	});

