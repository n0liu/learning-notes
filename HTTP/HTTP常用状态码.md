# Http 相关分享

> HTTP 协议一般指 HTTP（超文本传输协议）。超文本传输协议（英语：HyperText Transfer Protocol，缩写：HTTP）是一种用于分布式、协作式和超媒体信息系统的应用层协议，是因特网上应用最为广泛的一种网络传输协议，所有的 WWW 文件都必须遵守这个标准。

HTTP 是为 Web 浏览器与 Web 服务器之间的通信而设计的，但也可以用于其他目的。

HTTP 是一个基于 TCP/IP 通信协议来传递数据的（HTML 文件、图片文件、查询结果等）。


## HTTP 常见状态码及其应用

### 1.HTTP 状态码分类

> 状态码的职责是当客户端向服务器端发送请求时,描述返回的请求结果.用户可以知道服务器是正常处理了请求,还是出现了错误.

| 分类 | 分类描述 |
| :---: | :---: |
| 1** | 信息，服务器收到请求，需要请求者继续执行操作 |
| 2** | 成功，操作被成功接收并处理 |
| 3** | 重定向，需要进一步的操作以完成请求 |
| 4** | 客户端错误，请求包含语法错误或无法完成请求 |
| 5** | 服务器错误，服务器在处理请求的过程中发生了错误 |


### 2.HTTP 常见状态码

据查,仅记录在 [RFC2616](https://cloud.tencent.com/developer/section/1190064) 上的 HTTP 状态码就达到 40 种,若再加上 WebDAV(Web-based Distributed Authoring and Versioning,基于万维网的分布式创作和版本控制)([RFC4918](https://cloud.tencent.com/developer/section/1190067),5842)和附加 HTTP 状态码([RFC6585](https://www.rfc-editor.org/rfc/rfc6585))等扩展,数量就达 60 余种.别看种类繁多,实际上经常使用的大概只有 14 种,如下表所示:

| 状态码 | 状态码英文名称 | 中文描述 |
| :---: | :--- | :--- |
| 200 | OK | 请求成功。一般用于 GET 与 POST 请求 |
| 204 | No Content | 无内容。服务器成功处理，但未返回内容。在未更新网页的情况下，可确保浏览器继续显示当前文档 |
| 206 | Partial Content | 部分内容。服务器成功处理了部分 GET 请求 |
| 301 | Moved Permanently | 永久移动。请求的资源已被永久的移动到新 URI，返回信息会包括新的 URI，浏览器会自动定向到新 URI。今后任何新的请求都应使用新的 URI 代替 |
| 302 | Found | 临时移动。与 301 类似。但资源只是临时被移动。客户端应继续使用原有 URI |
| 303 | See Other | 查看其它地址。与 301 类似。使用 GET 和 POST 请求查看 |
| 304 | Not Modified | 未修改。所请求的资源未修改，服务器返回此状态码时，不会返回任何资源。客户端通常会缓存访问过的资源，通过提供一个头信息指出客户端希望只返回在指定日期之后修改的资源 |
| 307 | Temporary Redirect | 临时重定向。与 302 类似。使用 GET 请求重定向 |
| 400 | Bad Request | 客户端请求的语法错误，服务器无法理解 |
| 401 | Unauthorized | 请求要求用户的身份认证 |
| 403 | Forbidden | 服务器理解请求客户端的请求，但是拒绝执行此请求 |
| 404 | Not Found | 服务器无法根据客户端的请求找到资源（网页）。通过此代码，网站设计人员可设置"您所请求的资源无法找到"的个性页面 |
| 405 | Method Not Allowed | 客户端请求中的方法被禁止 |
| 500 | Internal Server Error | 服务器内部错误，无法完成请求 |
| 503 | Service Unavailable | 由于超载或系统维护，服务器暂时的无法处理客户端的请求。延时的长度可包含在服务器的 Retry-After 头信息中 |


- 更多状态码 [https://www.runoob.com/http/http-status-codes.html]()

## HTTP 常见请求头/响应头及其应用

HTTP 协议的请求和响应报文中必定包含 HTTP 首部。首部内容为客户端和服务器分别处理请求和响应提供所需要的信息，主要包括报文主体大小，所使用的语言，认证信息等。

### 3.首部字段的类型

HTTP 首部字段根据实际用途被分为以下四种类型：

- 通用首部字段：请求与响应报文都会使用的首部
- 请求首部字段：请求报文使用，补充请求的附加内容，客户端信息，响应内容相关优先级等信息
- 响应首部字段：响应报文使用，补充响应的附加内容，也会要求客户端附加额外的内容信息
- 实体首部字段：针对请求和响应报文的实体部分使用的首部，补充了资源内容更新时间等与实体有关的信息。

### 4.通用首部字段
| 首部字段名 | 说明 |
| :---: | :---: |
| Cache-Control | 控制缓存的行为 |
| Connection | 逐跳首部、连接的管理 |
| Date | 创建报文的日期时间 |
| Pragma | 报文指令 |
| Trailer | 报文末端的首部一览 |
| Transfer-Encoding | 指定报文主体的传输编码方式 |
| Upgrade | 升级为其他协议 |
| Via | 代理服务器的相关信息 |
| Warning | 错误通知 |


### 5.请求首部字段
| 首部字段名 | 说明 |
| :---: | :---: |
| Accept | 用户代理可处理的媒体类型 |
| Accept-Charset | 优先的字符集 |
| Accept-Encoding | 优先的内容编码 |
| Accept-Language | 优先的语言（自然语言） |
| Authorization | Web 认证信息 |
| Expect | 期待服务器的特定行为 |
| From | 用户的电子邮箱地址 |
| Host | 请求资源所在服务器 |
| If-Match | 比较实体标记（ETag) |
| If-Modified-Since | 比较资源的更新时间 |
| If-None-Match | 比较实体标记（与 If-Match 相反） |
| If-Range | 资源未更新时发送实体 Byte 的范围请求 |
| If-Unmodified-Since | 比较资源的更新时间（与 If-Modified-Since 相反） |
| Max-Forwards | 最大传输逐跳数 |
| Proxy-Authorization | 代理服务器要求客户端的认证信息 |
| Range | 实体的字节范围请求 |
| Referer | 对请求中 URI 的原始获取方 |
| TE | 传输编码的优先级 |
| User-Agent | HTTP 客户端程序的信息 |


### 6.请求首部字段
| 首部字段名 | 说明 |
| :---: | :---: |
| Accept-Ranges | 是否接受字节范围请求 |
| Age | 推算资源创建经过时间 |
| ETag | 资源的匹配信息 |
| Location | 令客户端重定向至指定 URI |
| Proxy-Authenticate | 代理服务器对客户端的认证信息 |
| Retry-After | 对再次发起请求的时机要求 |
| Server | HTTP 服务器的安装信息 |
| Vary | 代理服务器缓存的管理信息 |
| WWW-Authenticate | 服务器对客户端的认证信息 |


### 7.实体首部字段
| 首部字段名 | 说明 |
| :---: | :---: |
| Allow | 资源可支持的 HTTP 方法 |
| Content-Encoding | 实体主体适用的编码方式 |
| Content-Language | 实体主体的自然语言 |
| Content-Length | 实体主体的大小（单位：字节） |
| Content-Location | 替代对应资源的 URI |
| Content-MD5 | 实体主体的报文摘要 |
| Content-Range | 实体主体的位置范围 |
| Content-Type | 实体主体的媒体类型 |
| Expires | 实体主体过期的日期时间 |
| Last-Modified | 资源的最后修改日期时间 |


## 演示常用的字段作用

example:Content-Type 的常见格式

text/html ： HTML 格式

text/plain ：纯文本格式

text/xml ： XML 格式

image/gif ：gif 图片格式

image/jpeg ：jpg 图片格式

image/png：png 图片格式

application/xhtml+xml ：XHTML 格式

application/xml ： XML 数据格式

application/atom+xml ：Atom XML 聚合格式

application/json ： JSON 数据格式

application/pdf ：pdf 格式

application/msword ： Word 文档格式

application/octet-stream ： 二进制流数据（如常见的文件下载）

application/x-www-form-urlencoded ： 中默认的 encType，form 表单数据被编码为 key/value 格式发送到服务器（表单默认的提交数据的格式）

multipart/form-data ： 需要在表单中进行文件上传时，就需要使用该格式 以上就是我们在日常的开发中，经常会用到的若干 content-type 的内容格式。

...
