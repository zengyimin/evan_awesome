## @ `jsonp`

### 理解同源策略限制

同源策略阻止从一个域上加载的脚本获取或操作另一个域上的文档属性.也就是说,受到请求的 `URL` 的域必须与当前 `Web` 页面的域相同.这意味着浏览器隔离来自不同源的内容,以防止它们之间的操作.这个浏览器策略很旧,从 `Netscape Navigator 2.0` 版本开始就存在.

克服该限制的一个相对简单的方法是让 `Web` 页面向它源自的 `Web` 服务器请求数据,并且让 `Web` 服务器像代理一样将请求转发给真正的第三方服务器.尽管该技术获得了普遍使用,但它是不可伸缩的.另一种方式是使用框架要素在当前 `Web` 页面中创建新区域,并且使用 `GET` 请求获取任何第三方资源.不过,获取资源后,框架中的内容会受到同源策略的限制.

克服该限制更理想方法是在 `Web` 页面中插入动态脚本元素,该页面源指向其他域中的服务 `URL` 并且在自身脚本中获取数据.脚本加载时它开始执行.该方法是可行的,因为同源策略不阻止动态脚本插入,并且将脚本看作是从提供 `Web` 页面的域上加载的.但如果该脚本尝试从另一个域上加载文档,就不会成功.幸运的是,通过添加 `JavaScript Object Notation (JSON)` 可以改进该技术.

### `JSONP` 服务
知道如何使用 `JSONP` 之后,可以开始使用一些现成的 `JSONP Web` 服务来构建应用程序和 `mashup`.下面为接下来的开发项目做准备.(提示: 您可以复制特定的 `URL` 并将其粘贴到浏览器的地址栏,以检查生成的 `JSONP` 响应).

Digg API: 来自 Digg 的头条新闻:

```
http://services.digg.com/stories/top?appkey=http%3A%2F%2Fmashup.com&type=javascript&callback=?
```

Geonames API: 邮编的位置信息:

```
http://www.geonames.org/postalCodeLookupJSON?postalcode=10504&country=US&callback=?
```

### 重要提示

`JSONP` 是构建 `mashup` 的强大技术,但不幸的是,它并不是所有跨域通信需求的万灵药.它有一些缺陷,在提交开发资源之前必须认真考虑它们.

第一,也是最重要的一点,没有关于 `JSONP` 调用的错误处理.如果动态脚本插入有效,就执行调用; 如果无效,就静默失败.失败是没有任何提示的.例如,不能从服务器捕捉到 404 错误,也不能取消或重新开始请求.不过,等待一段时间还没有响应的话,就不用理它了.(未来的 jQuery 版本可能有终止 `JSONP` 请求的特性).

`JSONP` 的另一个主要缺陷是被不信任的服务使用时会很危险.因为 `JSONP` 服务返回打包在函数调用中的 JSON 响应,而函数调用是由浏览器执行的,这使宿主 Web 应用程序更容易受到各类攻击.如果打算使用 `JSONP` 服务,了解它能造成的威胁非常重要.(参见 参考资料 了解更多信息).
