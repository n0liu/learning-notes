总耗时约30分钟，若时间过长需简短可告知哈~
# 1.Restful API是什么？
## 1.1来源
REST首次出现在2000年[Roy Thomas Fielding](https://zh.wikipedia.org/w/index.php?title=Roy_Thomas_Fielding&action=edit&redlink=1)博士的《架构风格与基于网络的软件架构设计》论文中提出来的一种[万维网](https://zh.wikipedia.org/wiki/%E4%B8%87%E7%BB%B4%E7%BD%91)[软件架构](https://zh.wikipedia.org/wiki/%E8%BD%AF%E4%BB%B6%E6%9E%B6%E6%9E%84)风格，Roy Fielding是HTTP规范的主要编写者之一。 他在论文中提到："我这篇文章的写作目的，就是想在**符合架构原理**的前提下，理解和评估以网络为基础的应用软件的架构设计，得到一个功能强、性能好、适宜通信的架构。"

- REST 本身并没有创造新的技术、组件或服务，它只是一种**软件架构风格**，是一组**架构约束条件和原则**，而不是技术框架。
- 隐藏在RESTful背后的理念就是**使用Web的现有特征和能力**，更好地使用现有Web标准中的一些准则和约束。

论文地址：[Architectural Styles and the Design of Network-based Software Architectures](https://link.zhihu.com/?target=http%3A//www.ics.uci.edu/~fielding/pubs/dissertation/top.htm)
REST章节：[Fielding Dissertation: CHAPTER 5: Representational State Transfer (REST)](https://link.zhihu.com/?target=http%3A//www.ics.uci.edu/~fielding/pubs/dissertation/rest_arch_style.htm)
## 1.2名称解释
### REST
全称： **Re**presentational **S**tate **T**ransfer (省略了主语Resource) 
维基百科翻译为：**表现层状态转换**
通俗来说就是：资源在网络中以某种表现形式进行状态转移。
分解开来：

- Resource：资源，即数据
   - 它可以是一段文本、一张图片、一首歌曲、一种服务等。
   - 每种资源对应一个特定的URI（统一资源定位符）。要获取这个资源，访问它的URI就可以。
- Representational：表现层
   - **我们把"资源"具体呈现出来的形式，叫做它的"表现层"（Representation）。**
   - 比如：
      - 文本可以用txt格式表现，也可以用HTML格式、XML格式、JSON格式表现，甚至可以采用二进制格式；
      - 图片可以用JPG格式表现，也可以用PNG格式表现。
- State Transfer：**状态转换**
   - 访问一个网站，就代表了客户端和服务器的一个互动过程。会涉及到数据和状态的变化。
### Restful
其中ful代表形容词，代表满足REST原则的。
### RESTful API
RESTful API代表符合REST规范的Web API。
## **1.3REST架构限制条件**
[Roy Thomas Fielding](https://zh.wikipedia.org/w/index.php?title=Roy_Thomas_Fielding&action=edit&redlink=1)的博士在论文中提出REST架构应满足以下6个原则：

1. 客户端-服务端（Client-Server）
   - 通过客户端往服务端发送请求
   - 客户端和服务端的分离可以更好的实现跨多平台的应用
2. 无状态（Stateless）
   - 服务器不保存客户端的信息（请求，无须保持 session）
   - 客户端保存状态信息，每次请求携带所有必须的状态信息（如：请求的数据、头部信息、请求的返回等），服务器端根据这些状态信息来处理请求。
   - 无状态对于服务端的弹性扩容很重要
   - _（服务器可以将会话状态信息传递给其他服务，比如数据库服务，这样可以保持一段时间的状态信息，从而实现认证功能。）_
3. 可缓存（Cacheability）
   - 服务端需回复是否可以缓存
   - 管理良好的缓存机制可以减少客户端-服务器之间的交互。（_甚至完全避免客户端-服务器交互，这进一步提了高性能和可扩展性，并预防客户端在将来进行请求的时候得到陈旧的或者不恰当的数据。_）
4. 统一接口（Uniform Interface）
   - 是 RESTful 系统设计的基本出发点。通过一定的原则设计接口，可以降低耦合性，简化系统架构（可以让所有模块各自独立的进行改进。）
5. 分层系统（Layered System）
   - 客户端一般不知道是否直接连接到了最终的服务器，或者是路径上的中间服务器。
   - 分层允许我们灵活的部署服务端项目，例如中间服务器可以通过负载均衡和共享缓存的机制提高系统的可扩展性，这样可也便于安全策略的部署
6. 按需代码（Code-On-Demand，可选）
   - 服务器可以通过发送可执行代码给客户端的方式，临时性的扩展功能或者定制功能。（例如Java Applet、Flash或JavaScript。）
# 2.为什么需要Restful API？
随着安卓、IOS、小程序等形式的客户端层出不穷，客户端的种类出现多元化，**而客户端和服务端需要接口进行通信**，但接口的**规范性**就成了一个问题：
![](https://cdn.nlark.com/yuque/0/2022/png/26213287/1650763588982-bb4dddbb-4041-4927-b123-f96b9a00c8fd.png#clientId=u44902f92-fbdb-4&from=paste&id=u75f96e2a&originHeight=782&originWidth=1646&originalType=url&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=ufef987aa-30b2-4136-8318-ed5e461b9fe&title=)
所以定义一套**结构清晰、符合标准、易于理解、扩展方便**，让大部分人都能够理解和接受的**接口风格**就显得越来越重要，而RESTful风格的接口刚好有以上特点，就逐渐流行起来。
![](https://cdn.nlark.com/yuque/0/2022/png/26213287/1650763588975-fc6f3af9-8d89-4040-9e4c-94251e4b53ad.png#clientId=u44902f92-fbdb-4&from=paste&id=u243e009e&originHeight=698&originWidth=1560&originalType=url&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=u0c7cb9fa-3436-437a-b413-a0e6ef46c09&title=)
# 3.Restful API怎么用？
## RESTful API设计原则
RESTful API 的核心是**规范**。不同公司、不同团队、不同项目可能采取不同的 REST 设计原则，以下所列的是大家比较**公认**的一些原则。
### 1.请求设计
客户端可以向服务端发送携带数据的请求、服务端会返回适当的响应，构造一个请求可能需要：

1. **端点（Endpoint）**：它是 REST 服务器监听的 URL 地址。
2. **请求方法（Method）**：REST 为不同的请求类型实现了许多“方法”，以下是最常用的：-**GET**：从服务器获取资源。-**POST**：在服务器上创建资源。-**PUT**：更新（全部更新/替换）服务器上的现有资源。需传递所有属性。-**PATCH**：部分更新服务器上的现有资源。传递需更新的（部分）属性即可。-**DELETE**：删除服务器上现有的资源。
3. **头部信息（Headers）**：用于客户端和服务端通讯的额外信息（REST 是无状态的）。常见的头部信息如下：**请求头（Request）**：-_host_：客户端的 IP 地址（或请求的源地址）-_accept-language_：客户端接受的语言类型-_user-agent_：客户端的详细信息，如操作系统和浏览器类型**响应头（Response）**：-_status_：请求的状态或 HTTP 状态码-_content-type_：服务器返回的资源的类型-_set-cookie_：服务器设置的 cookies
4. **请求数据（Data）**：（也称为请求体或消息）包含了将要发送给服务器的数据
### 2.URI 设计
资源都是使用 URI 标识的，我们应该按照一定的规范来设计 URI，通过规范化可以使我们的 API 接口更加易读、易用。
以下是 URI 设计时，应该遵循的一些规范：

- URL 被视为“资源”，资源名使用名词而不是动词（遵循可寻址性原则，具有自描述性，需要在形式上给人以直觉上的关联）
   - 传统API设计：（把操作数据这类动词放在url里面）
      - 添加图书 ：/book/add
      - 查找某一本书 ：/book/get?id=123
      - 查找某个作者的书籍 ：/book/getByAuthor?author=1&page=1
   - Restful API设计：（把动词都放在method 请求方法里面）
      - 添加图书 ：POST /books
      - 查找某一本书 ：GET /books/123
      - 查找某个作者的书籍 ：GET /author/1/book?page=1
- 名词用复数表示。
   - 因为所用的名词往往与数据库的表格名对应。一般来说，数据库中的表都是同种记录的"**集合**"（collection），所以API中的名词也应该使用复数。
   - 资源分为 Collection 和 Member 两种。
      - Collection：一堆资源的集合。
         - 例如我们系统里有很多用户（User）, 这些用户的集合就是 Collection。Collection 的 URI 标识应该是 域名/资源名复数, 例如https:// iam.api.marmotedu.com/users。
      - Member：单个特定资源。
         - 例如系统中特定名字的用户，就是 Collection 里的一个 Member。Member 的 URI 标识应该是 域名/资源名复数/资源名称, 例如https:// iam.api.marmotedu/users/admin。
- URI 结尾不应包含/。
- URI 中不能出现下划线 _，必须用中杠线 -代替（这里有些人推荐用 _，有些人推荐用 -，统一使用一种格式即可，推荐用 - ）。
- URI 路径用小写，不要用大写。
- 避免层级过深的 URI。超过 2 层的资源嵌套会很乱，建议将其他资源转化为?参数，比如：请求某个学校里某个班级里的学生
   -  # 不推荐
 /schools/qinghua/classes/rooma/students 
 # 推荐
 /students?school=qinghua&class=rooma 

这里有个地方需要注意：在实际的 API 开发中，可能会发现有些操作不能很好地映射为一个 REST 资源，这时候，你可以参考下面的做法：

- 将一个操作变成**资源的一个属性**，比如想在系统中暂时禁用某个用户，可以这么设计 URI：/users/zhangsan?active=false。
- 将操作当作是一个资源的嵌套资源，比如一个 GitHub 的加星/去星操作：
   -  PUT /gists/:id/star # github star action
 DELETE /gists/:id/star # github unstar action
- 如果以上都不能解决问题，有时可以打破这类规范。比如登录操作，登录不属于任何一个资源，URI 可以设计为：/login。
- 在设计 URI 时，如果你遇到一些不确定的地方，推荐参考 [GitHub 标准 RESTful API](https://docs.github.com/cn/rest)。
### 3.REST 资源操作映射为 HTTP 方法
REST 风格虽然适用于很多传输协议，但在实际开发中， HTTP 协议已经成了实现 RESTful API 事实上的标准（虽然REST本身受Web技术的影响很深， 但是理论上REST架构风格并不是绑定在HTTP上）。
基本上 RESTful API 所有的行为都应该是由客户端通过HTTP 协议的4个动词，对服务器端资源进行操作，实现“表现层状态转化”。
REST 架构对资源的操作包括获取、创建、修改和删除，这些操作对应 HTTP 协议提供的 GET、POST、PUT 和 DELETE 方法。
形成的规范如下表所示：（在资源集合下，x代表x；在单个资源下，x代表x。）
![image.png](https://cdn.nlark.com/yuque/0/2022/png/26213287/1650763589685-b21f975e-c215-4595-ac53-26df670c0f08.png#clientId=u44902f92-fbdb-4&from=paste&id=u9f0dffae&name=image.png&originHeight=698&originWidth=1524&originalType=url&ratio=1&rotation=0&showTitle=false&size=139233&status=done&style=none&taskId=ucfadfd6b-bbb0-4aa6-a73b-ca4969060d5&title=)
例：（GET /users 代表x）
![image.png](https://cdn.nlark.com/yuque/0/2022/png/26213287/1650763589534-ca610f38-fcd7-4338-abd0-769f2bbf75b7.png#clientId=u44902f92-fbdb-4&from=paste&id=ueb81fec8&name=image.png&originHeight=582&originWidth=1754&originalType=url&ratio=1&rotation=0&showTitle=false&size=120270&status=done&style=none&taskId=u83403d25-915e-446c-827a-5f67b045fbb&title=)
对资源的操作应该满足**安全性**和**幂等性**：

- 安全性：不会改变资源状态，可以理解为只读的。
- 幂等性：执行 1 次和执行 N 次，对资源状态改变的效果是等价的。

使用不同 HTTP 方法时，资源操作的安全性和幂等性对照见下表：
![image.png](https://cdn.nlark.com/yuque/0/2022/png/26213287/1650763589224-e96b4072-0731-4371-a9aa-70bdae7261db.png#clientId=u44902f92-fbdb-4&from=paste&id=u4a541cac&name=image.png&originHeight=448&originWidth=1434&originalType=url&ratio=1&rotation=0&showTitle=false&size=38498&status=done&style=none&taskId=ua1a1dbf2-9b16-494e-aaa8-9608eb66e80&title=)

- 安全性
   - 只有GET是只读的，POST、PUT、DELETE都可能改变资源状态。所以GET是具有安全性，POST、PUT、DELETE不具有安全性。
- 幂等性
   - GET对资源查询多次，结果都是一样的，是幂等操作；
   - POST不是幂等操作，一次请求添加一份新资源，二次请求则添加了两份新资源，多次请求会产生不同的结果，因此POST不是幂等操作；
   - PUT将A修改为B，它第一次请求时值变为了B，再进行多次此操作，最终的结果还是B，与一次执行的结果是一样的，所以PUT是幂等操作；
   - DELETE第一次将资源删除后，后面多次进行此删除请求，最终结果是一样的，将资源删除掉了；

下面来看一个幂等性的例子：
一个为员工涨薪的接口，本次请求发送后为 1 号员工涨薪 500 元。
 PUT https://edu.lagou.com/employee/salary
 {"id" : "1,"incr_salary":500}
**【反面典型 】**如果**没有考虑幂等特性**，可能会这么写，伪代码如下：
 //查询1号员工数据
 Employee employee = employeeService.selectById(1);
 //更新工资为原工资+500
 employee.setSalary(employee.getSalary() + incrSalary);
 //执行更新语句
 employeeService.update(employee)
对于这段代码，单独执行没有任何问题。
但是在分布式环境下，为了保证消息的高可靠性，往往客户端会采用重试或消息补偿的形式重复发送同一个请求。
在这种情况下，这段代码就会出现问题：因为每一个重复请求被发送到服务器都会让该员工工资加 500，最终该员工工资会大于实际应收工资。这样就不符合PUT是幂等的特性。
那如何解决呢？有一种**乐观锁设计**，在员工表额外增加一个 version 的字段，代表当前数据的版本，任何对该数据修改操作都会让 version 字段值 +1，这个 version 的数值要求附加在请求中，如下所示：
 PUT https://edu.lagou.com/employee/salary
 {"id" : "1,"incr_salary":500 ,  "version":1}
执行更新操作前，1 号员工原始数据如下：

| **id** | **salary** | **version** |
| --- | --- | --- |
| 1 | 3000 | 1 |

而服务器端代码也作出如下调整，SQL 语句要增加版本号的比对。
```
 //查询1号员工数据
 Employee employee = employeeService.selectById(1);
 //更新工资为原工资+500
 employee.setSalary(employee.getSalary() + incrSalary);
 //update执行成功，版本号+1
 employee.setVersion(employee.getVersion() + 1));
 //执行更新语句
 employeeService.update(employee)
```
注意：此时 update 方法，除了 id 条件外，还要增加 version 的判断，如下所示。
 update employee set salary = 3500,version=2 where id = 1 and version=1
当执行成功后，1 号员工原始数据将工资更新为 3500，版本为 2。
那这种设计如何保证幂等呢？假设客户端再次发送重复的请求：
 PUT https://edu.lagou.com/employee/salary
 {"id" : "1,"incr_salary":500 ,  "version":1}
后台按逻辑仍会执行下面的 update 语句：
 update employee set salary = 3500,version=2 where id = 1 and version=1
此时，因为数据表中 version 字段已经更新为 2，where 筛选条件将无法得到任何数据。自然就不会产生实质的更新操作，我们幂等性的初衷就已经达到了。
以上介绍的是实现幂等性方案中 **MVCC 多版本并发控制方案**。**除此以外**，保证幂等性还可以采用**幂等表、分布式锁、状态机**等实现方式。
在使用 HTTP 方法的时候，需要注意：

- GET 返回的结果，要尽量可用于 PUT、POST 操作中。
   - 例如，用 GET 方法获得了一个 user 的信息，调用者修改 user 的信息，然后将此结果再用 PUT 方法更新。这要求 GET、PUT、POST 操作的资源属性是一致的。

在设计 API 时，经常会有批量删除的需求，需要在请求中携带多个需要删除的资源名，但是 HTTP 的 DELETE 方法不能携带多个资源名，这时候可以通过下面三种方式来解决：

1. 发起多个 DELETE 请求。
2. 操作路径中带多个 id，id 之间用分隔符分隔, 例如：DELETE /users?ids=1,2,3 。
3. 直接使用 POST 方式来批量删除，在body 中传入需要删除的资源列表。

其中，第二种是最推荐的方式，因为使用了匹配的 DELETE 动词，并且不需要发送多次 DELETE 请求。
这三种方式都有各自的使用场景，你可以根据需要自行选择。如果选择了某一种方式，那么整个项目都需要统一用这种方式。
### 4.统一的返回格式
接口返回最常用的数据格式是JSON。由于JSON能直接被JavaScript读取，所以，以JSON格式编写的REST风格的API具有简单、易读、易用的特点。
一般来说，一个系统的 RESTful API 会向外界开放多个资源的接口，接口的返回格式需要注意以下几点：

- 每个接口的返回格式要保持一致。
   - 不然客户端代码要适配不同接口的返回格式，会大大增加学习和使用成本。
- 要包含 code、message 两项，分别对应了服务器处理结果与返回的消息内容。
- data 属性是可选项，包含从响应返回的额外数据。
   - 如：查询结果、新增或更新后的数据。
- 遵循统一的 code、message 命名标准。
   - 例如：code 以 1xxx 开头代表参数异常，2xxx 开头代表数据库处理异常。不同的公司有不同的命名规则，一定要提前定义好并要求开发团队严格按语义使用编码
- RESTful 接口要求返回的是 JSON 或者 XML 数据，绝不可以包含任何与具体展现相关的内容。

返回的格式没有强制的标准，可以根据实际的业务需要返回不同的格式。
**【反面典型 】**例如，要查询 10 号员工数据。
 GET http(s)://edu.com/employee/10
 {
     "code" : "0" ,
     "message" : "success" ,
     "data" : "<h1>员工姓名:张三</h1>..."
 }
在上面的 JSON 响应中，data 返回了与具体展现相关的内容，会导致不好扩展等问题。
改为下面的样式是较好的数据结构，最终数据如何展现将由客户端 HTML、APP 进行渲染。
 GET http(s)://edu.com/employee/10
 {
     "code" : "0" ,         //--->服务器处理结果
     "message" : "success" ,//--->返回的消息内容
     "data" : {             //--->返回的数据
         "name":"张三",
         "age" : 36
     }
 }
### 5.API 版本管理
随着时间的推移、需求的变更，一个 API 往往满足不了现有的需求，这时候就需要对 API 进行修改。对 API 进行修改时，不能影响**其他调用系统**的正常使用，这就要求 API 变更做到**向下兼容**，也就是**新老版本共存**。
但在实际场景中，很可能会出现同一个 API 无法向下兼容的情况。这时候最好的解决办法是从一开始就引入 API 版本机制，当不能向下兼容时，就引入一个**新的版本，老的版本则保留原样**。这样既能保证服务的可用性和安全性，同时也能满足新需求。
API 版本有不同的标识方法，在 RESTful API 开发中，通常将版本标识放在如下 3 个位置：

- URL 中，比如/v1/users。
   - 这样做的好处是直观，GitHub、Kubernetes、Etcd 等很多优秀的 API 均采用这种方式。
- HTTP Header 中，比如Accept: vnd.example-com.foo+json; version=1.0。
- Form 参数中，比如/users?version=v1。

这里要注意，有些开发人员不建议将版本放在 URL 中，因为他们觉得不同的版本可以理解成 同一种资源的不同表现形式，所以应该采用同一个 URI。
对于这一点，没有严格的标准，根据项目实际需要选择一种方式即可。
### 6.API 命名
API 通常的命名方式有三种，分别是驼峰命名法 (serverAddress)、蛇形命名法 (server_address) 和脊柱命名法 (server-address)。
驼峰命名法和蛇形命名法都需要切换输入法，会增加操作的复杂性，也容易出错，所以一般建议用脊柱命名法。GitHub API 用的就是脊柱命名法，例如 [selected-actions](https://docs.github.com/en/rest/reference/actions#get-allowed-actions-for-an-organization)。
### 7.统一分页 / 过滤 / 排序 / 搜索功能
REST 资源的查询接口，通常情况下都需要实现分页、过滤、排序、搜索功能，因为这些功能是每个 REST 资源都可能会用到的，所以可以实现为一个公共的 API 组件。
下面是一些常见的参数：

- 分页：
   - 在列出一个 Collection 下所有的 Member 时，应该提供分页功能，例如/users?offset=0&limit=20
      - limit，指定返回记录的数量；
      - offset，指定返回记录的开始位置
   - 引入分页功能可以减少 API 响应的延时，同时可以避免返回太多条目，导致服务器 / 客户端响应特别慢，（甚至导致服务器 / 客户端 crash 的情况）。
- 过滤：
   - 如果用户不需要一个资源的全部状态属性，可以在 URI 参数里指定返回哪些属性，例如/users?fields=email,username,address。
- 排序：
   - 用户很多时候会根据创建时间或者其他因素，列出一个 Collection 中前 100 个 Member，这时可以在 URI 参数中指明排序参数，例如/users?sort=age,desc。
- 搜索：
   - 当一个资源的 Member 太多时，用户可能想通过搜索，快速找到所需要的 Member，或着想搜下有没有名字为 xxx 的某类资源，这时候就需要提供搜索功能。搜索建议按模糊匹配来搜索。
### 8.域名
API 的域名设置主要有两种方式：

- [https://marmotedu.com/api](https://marmotedu.com/api) （域名/api ），这种方式适合 API 将来**不会**有进一步扩展的情况，比如刚开始 marmotedu.com 域名下只有一套 API 系统，未来也只有这一套 API 系统。
- [https://iam.api.marmotedu.com](https://iam.api.marmotedu.com) （api在域名中），如果 marmotedu.com 域名下未来会新增另一个系统 API，这时候最好的方式是每个系统的 API 拥有专有的 API 域名，比如：storage.api.marmotedu.com，network.api.marmotedu.com。腾讯云的域名就是采用这种方式。
### 9.状态码
这部分和HTTP部分相似，就不赘述了。
不同的公司有不同的命名规则。
#### 状态码必须精确
客户端的每一次请求，服务器都必须给出回应。回应包括 HTTP 状态码和数据两部分。
HTTP 状态码就是一个三位数，分成五个类别。

- 1xx：相关信息
- 2xx：操作成功
- 3xx：重定向
- 4xx：客户端错误
- 5xx：服务器错误

这五大类总共包含[100多种](https://en.wikipedia.org/wiki/List_of_HTTP_status_codes)状态码，覆盖了绝大部分可能遇到的情况。每一种状态码都有标准的（或者约定的）解释，客户端只需查看状态码，就可以判断出发生了什么情况，所以服务器应该返回尽可能精确的状态码。
下面介绍其他四类状态码的精确含义：
**2xx 状态码**
200状态码表示操作成功，但是不同的方法可以返回更精确的状态码。

- GET: 200 OK
- POST: 201 Created
- PUT: 200 OK
- DELETE: 204 No Content

上面代码中，POST返回201状态码，表示生成了新的资源；DELETE返回204状态码，表示资源已经不存在。
此外，202 Accepted状态码表示服务器已经收到请求，但还未进行处理，会在未来再处理，通常用于异步操作。下面是一个例子。
 HTTP/1.1 202 Accepted
 
 {
 "task": {
  "href": "/api/company/job-management/jobs/2130040",
  "id": "2130040"
 }
 }
**3xx 状态码**
API 用不到301状态码（永久重定向）和302状态码（暂时重定向，307也是这个含义），因为它们可以由应用级别返回，浏览器会直接跳转，API 级别可以不考虑这两种情况。
API 用到的3xx状态码，主要是303 See Other，表示参考另一个 URL。它与302和307的含义一样，也是"暂时重定向"，区别在于302和307用于GET请求，而303用于POST、PUT和DELETE请求。收到303以后，浏览器不会自动跳转，而会让用户自己决定下一步怎么办。下面是一个例子。
 HTTP/1.1 303 See Other
 Location: /api/orders/12345
**4xx 状态码**
4xx状态码表示客户端错误，主要有下面几种。
400 Bad Request：服务器不理解客户端的请求，未做任何处理。
401 Unauthorized：用户未提供身份验证凭据，或者没有通过身份验证。
403 Forbidden：用户通过了身份验证，但是不具有访问资源所需的权限。
404 Not Found：所请求的资源不存在，或不可用。
405 Method Not Allowed：用户已经通过身份验证，但是所用的 HTTP 方法不在他的权限之内。
410 Gone：所请求的资源已从这个地址转移，不再可用。
415 Unsupported Media Type：客户端要求的返回格式不支持。比如，API 只能返回 JSON 格式，但是客户端要求返回 XML 格式。
422 Unprocessable Entity ：客户端上传的附件无法处理，导致请求失败。
429 Too Many Requests：客户端的请求次数超过限额。
**5xx 状态码**
5xx状态码表示服务端错误。一般来说，API 不会向用户透露服务器的详细信息，所以只要两个状态码就够了。
500 Internal Server Error：客户端请求有效，服务器处理时发生了意外。
503 Service Unavailable：服务器无法处理请求，一般用于网站维护状态。
#### 状态码典型用法：
GET

- 200（OK） - 表示已在响应中发出
- 204（无内容） - 资源有空表示
- 301（Moved Permanently） - 资源的URI已被更新
- 303（See Other） - 其他（如，负载均衡）
- 304（not modified）- 资源未更改（缓存）
- 400 （bad request）- 指代坏请求（如，参数错误）
- 404 （not found）- 资源不存在
- 406 （not acceptable）- 服务端不支持所需表示
- 500 （internal server error）- 通用错误响应
- 503 （Service Unavailable）- 服务端当前无法处理请求

POST

- 200（OK）- 如果现有资源已被更改
- 201（created）- 如果新资源被创建
- 202（accepted）- 已接受处理请求但尚未完成（异步处理）
- 301（Moved Permanently）- 资源的URI被更新
- 303（See Other）- 其他（如，负载均衡）
- 400（bad request）- 指代坏请求
- 404 （not found）- 资源不存在
- 406 （not acceptable）- 服务端不支持所需表示
- 409 （conflict）- 通用冲突
- 412 （Precondition Failed）- 前置条件失败（如执行条件更新时的冲突）
- 415 （unsupported media type）- 接受到的表示不受支持
- 500 （internal server error）- 通用错误响应
- 503 （Service Unavailable）- 服务当前无法处理请求

PUT

- 200 （OK）- 如果已存在资源被更改
- 201 （created）- 如果新资源被创建
- 301（Moved Permanently）- 资源的URI已更改
- 303 （See Other）- 其他（如，负载均衡）
- 400 （bad request）- 指代坏请求
- 404 （not found）- 资源不存在
- 406 （not acceptable）- 服务端不支持所需表示
- 409 （conflict）- 通用冲突
- 412 （Precondition Failed）- 前置条件失败（如执行条件更新时的冲突）
- 415 （unsupported media type）- 接受到的表示不受支持
- 500 （internal server error）- 通用错误响应
- 503 （Service Unavailable）- 服务当前无法处理请求

DELETE

- 200 （OK）- 资源已被删除
- 301 （Moved Permanently）- 资源的URI已更改
- 303 （See Other）- 其他，如负载均衡
- 400 （bad request）- 指代坏请求
- 404 （not found）- 资源不存在
- 409 （conflict）- 通用冲突
- 500 （internal server error）- 通用错误响应
- 503 （Service Unavailable）- 服务端当前无法处理请求
# 4.与其他解决方案对比
这部分我不太了解，是直接复制网上的资料，大家有了解的可以帮忙补充下
确定使用哪种 API 风格，需要根据项目需求，结合 API 风格的特点，这对以后的编码实现、通信方式和通信效率都有很大的影响。
## 4.1除REST外其它解决方案

- [远程过程调用](https://zh.wikipedia.org/wiki/%E8%BF%9C%E7%A8%8B%E8%BF%87%E7%A8%8B%E8%B0%83%E7%94%A8)（RPC）-来自：[维基百科](https://zh.wikipedia.org/wiki/%E8%A1%A8%E7%8E%B0%E5%B1%82%E7%8A%B6%E6%80%81%E8%BD%AC%E6%8D%A2)
- [服务导向架构](https://zh.wikipedia.org/wiki/%E6%9C%8D%E5%8B%99%E5%B0%8E%E5%90%91%E6%9E%B6%E6%A7%8B)（SOA）-来自：[维基百科](https://zh.wikipedia.org/wiki/%E8%A1%A8%E7%8E%B0%E5%B1%82%E7%8A%B6%E6%80%81%E8%BD%AC%E6%8D%A2)
- GraphQL（一种用于 API 的查询语言） -来自[freeCodeCamp](https://chinese.freecodecamp.org/news/rest-api-tutorial-rest-client-rest-service-and-api-calls-explained-with-code-examples/)
- JSON-Pure -来自[freeCodeCamp](https://chinese.freecodecamp.org/news/rest-api-tutorial-rest-client-rest-service-and-api-calls-explained-with-code-examples/)
- oData（开放数据协议） -来自[freeCodeCamp](https://chinese.freecodecamp.org/news/rest-api-tutorial-rest-client-rest-service-and-api-calls-explained-with-code-examples/)
## 4.2 RPC vs REST
来自：[微服务架构核心 20 讲-杨波](https://time.geekbang.org/course/detail/100003901-2274)
![image.png](https://cdn.nlark.com/yuque/0/2022/png/26213287/1650763613002-f24349d7-78fc-4349-88f7-eae8018b9a44.png#clientId=u44902f92-fbdb-4&from=paste&height=407&id=u66f6fcb4&name=image.png&originHeight=814&originWidth=1580&originalType=binary&ratio=1&rotation=0&showTitle=false&size=1122293&status=done&style=none&taskId=uaac95606-8d0e-4406-83ea-2368c533c78&title=&width=790)
和REST相关的内容有：

- 耦合性：客户端和服务端没有强的消息耦合
- 消息协议：一般消息协议是文本的，如XML、JSON。开发者可读，但大小一般比二进制大 
- 通讯协议：一般采用HTTP/HTTP2进行通信
- 性能：由于消息协议是基于文本协议和通信协议的原因，REST性能一般低于RPC，但还需看实际场景
- 接口契约IDL：swagger可以对接口进行契约规范
- 客户端：由于REST本身是松散的机制，一般HTTP客户端都可调用Restful API（不一定要强的生成客户端）。用接口定义契约如Swagger也可以自动生成强类型客户端，支持多语言的
- 开发者友好：由于消息协议是基于文本协议，对开发者调试较方便， 在浏览器中直接就可以调用REST接口
- 对外开放：可以直接对外开放，省掉了中间的转换
## 4.3 REST总结
### 优点
来自：[维基百科](https://zh.wikipedia.org/wiki/%E8%A1%A8%E7%8E%B0%E5%B1%82%E7%8A%B6%E6%80%81%E8%BD%AC%E6%8D%A2)

- 简洁：与复杂的[SOAP](https://zh.wikipedia.org/wiki/SOAP)和[XML-RPC](https://zh.wikipedia.org/wiki/XML-RPC)相比更加简洁
- 低耦合、轻量、自解释
- 无状态
- 提高开发效率
   - **前后端分离**：前端拿到数据只负责展示和渲染，不对数据做任何处理。后端处理数据并以JSON格式传输出去，定义这样一套统一的接口，你完全不用考虑用户使用什么系统，无论在web，ios，android三端都可以用相同的API接口
- 不用关心接口实现细节
- 相对更规范，更标准，更通用
- 可更高效利用缓存来提高响应速度
- 可提高服务器的扩展性：通讯本身的无状态性可以让不同的服务器的处理一系列请求中的不同请求
- 浏览器即可作为客户端，简化软件需求
- 相对于其他叠加在[HTTP协议](https://zh.wikipedia.org/wiki/%E8%B6%85%E6%96%87%E6%9C%AC%E4%BC%A0%E8%BE%93%E5%8D%8F%E8%AE%AE)之上的机制，REST的软件依赖性更小
- 不需要额外的资源发现机制
- 在软件技术演进中的长期的兼容性更好
### 缺点

- 性能不如 RPC 高
- 多端 (多次数据交互)
   - 当要获取多个资源时必须请求多个不同的 URL，进而带来多次数据交互。
   - 随着应用变得越来越复杂，管理这些 API 也变得更加困难。
# 参考链接：

1. [Go 语言项目开发实战-API 风格（上）：如何设计RESTful API？-极客时间-孔令飞](https://time.geekbang.org/column/article/386970)
2. [RESTful API 设计指南-阮一峰](https://www.ruanyifeng.com/blog/2014/05/restful_api.html)
3. [RESTful API 中文网](http://restful.p2hp.com/tech/rest-api-design-tutorial-with-example)
4. [维基百科](https://zh.wikipedia.org/wiki/%E8%A1%A8%E7%8E%B0%E5%B1%82%E7%8A%B6%E6%80%81%E8%BD%AC%E6%8D%A2)
5. [怎样用通俗的语言解释REST，以及RESTful？-zhihu](https://www.zhihu.com/question/28557115/answer/48094438?utm_source=wechat_session&utm_medium=social&utm_oi=38249267462144&utm_content=group2_Answer&utm_campaign=shareopn)
6. [restful是什么，restful的api协议是什么-zhihu](https://www.zhihu.com/zvideo/1406988851005452288) 同 [RESTful接口设计，不止命名规范那么简单-拉钩教育](https://kaiwu.lagou.com/course/courseInfo.htm?courseId=1130&sid=20-h5Url-0&lgec_type=website&lgec_sign=56C78768E1A134C49750D2797FB14316&buyFrom=1&pageId=1pz4#/detail/pc?id=8452)
7. [GitHub 标准 RESTful API](https://docs.github.com/cn/rest)
8. [RESTful 架构详解-runoob](https://www.runoob.com/w3cnote/restful-architecture.html)
9. [REST API 教程：REST 客户端，REST 服务及 API 调用（含代码示例）-freeCodeCamp](https://chinese.freecodecamp.org/news/rest-api-tutorial-rest-client-rest-service-and-api-calls-explained-with-code-examples/)
10. [微服务架构核心 20 讲-杨波](https://time.geekbang.org/course/detail/100003901-2274)

实践中常见的问题：

- 客户端不一定都支持这些HTTP方法吧?

的确有这种情况，特别是一些比较古老的基于浏览器的客户端，只能支持GET和POST两种方法。
在实践上，客户端和服务端都可能需要做一些妥协。例如rails框架就支持通过隐藏参数_method=DELETE来传递真实的请求方法， 而像Backbone这样的客户端MVC框架则允许传递_method传输和设置X-HTTP-Method-Override头来规避这个问题。

- 统一接口是否意味着不能扩展带特殊语义的方法?

统一接口并不阻止你扩展方法，只要方法对资源的操作有着具体的、可识别的语义即可，并能够保持整个接口的统一性。
像WebDAV就对HTTP方法进行了扩展，增加了LOCK、UPLOCK等方法。而github的API则支持使用PATCH方法来进行issue的更新，例如:
 PATCH /repos/:owner/:repo/issues/:number
不过，需要注意的是，像PATCH这种不是HTTP标准方法的，服务端需要考虑客户端是否能够支持的问题。

- RESTful API和http一样么？区别是？

不一样
REST通过HTTP实现，把用户的需求抽象成对资源的操作，用户必须通过HTTP协议的GET、HEAD、POST、PUT、DELETE、TRACE、OPTIONS七种基本操作去和服务器交互。

