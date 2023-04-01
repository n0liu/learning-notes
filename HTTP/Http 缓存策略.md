## 背景与定义
### 1.背景
> 为什么Web应用需要使用http缓存策略

一个Web应用在生产环境中，往往经常会被用户访问很多次，现代计算机的发展水平，网页页面加载和渲染的速度是非常快速的，可以做到毫秒级别。然而在页面加载和渲染整个过程中，比较慢的环节就是网络请求。考虑到用户的使用体验，我们期望应用的加载速度越快越好，因此在做页面性能优化的时候，我们就要去针对那个最大的瓶颈入手——网络请求。而且由于网络环境具有不稳定性，会加剧我们的网络请求以及页面加载的不稳定性。因此更加提升了我们优化网络请求的必要性。

为了让网络请求更快一些，我们就要尽量减少我们网络请求资源的“体积”和“数量”，基于这个背景，我们需要使用缓存策略。而Http协议也为我们提供了非常强大的缓存机制。
### 2.定义
> 什么是浏览器缓存

浏览器缓存是浏览器在本地磁盘对用户最近请求过的特定资源进行存储，当访问者再次访问同一页面时，浏览器就可以直接从本地磁盘加载可以多次使用的特定资源。用来减少发送不必要的网络请求，加块页面的加载速度，提升用户的使用体验。
## 强制缓存和协商缓存
### 1.强制缓存
![图片1.png](https://cdn.nlark.com/yuque/0/2022/png/21814148/1650191055530-e9f72aac-cc3e-4b2f-9a74-779083e0ac45.png#clientId=ucd45c617-c8fa-4&from=ui&id=u63ef1bd8&name=%E5%9B%BE%E7%89%871.png&originHeight=554&originWidth=768&originalType=binary&ratio=1&rotation=0&showTitle=false&size=108390&status=done&style=none&taskId=u728ee179-71b6-44d9-bc21-167cf2da200&title=)
初次请求，如果服务端感觉这个资源可以被缓存的话（通常是一些静态资源，如js、css、图片等），它就会在 response headers 中加一个Cache-Control，如果服务端感觉这个资源，没法被缓存，或者说不适合被缓存，它就不会加这个Cache-Control，也就是说，Cache-Control是在 response headers中由服务端返回的。
![图片5.png](https://cdn.nlark.com/yuque/0/2022/png/21814148/1650195962871-0f3bd219-430e-43cf-b30e-779e765ae8b3.png#clientId=u81ddd212-b674-4&from=ui&id=ueed1f9dd&name=%E5%9B%BE%E7%89%875.png&originHeight=420&originWidth=676&originalType=binary&ratio=1&rotation=0&showTitle=false&size=41666&status=done&style=none&taskId=uacb8c2a1-b568-4358-85a0-264440f7f0b&title=)
max-age ：以秒级别的缓存最长的过期时间；

no-cache：不用强制缓存（本地缓存）；

no-store：不用强制缓存，也不用协商缓存，就直接让服务端简单粗暴地把资源再重新返给浏览器客户端

private：针对最终用户做一个缓存

public：允许中间的一些路由或者中间一些代理也可以做缓存

expires

例如Cache-Control: max-age=31536000（单位是秒）这里就代表一年的时间。

![图片2.png](https://cdn.nlark.com/yuque/0/2022/png/21814148/1650194866150-e1f75825-d3e3-44f5-8e22-0f9d5fdf20ff.png#clientId=u81ddd212-b674-4&from=ui&id=u77b5fe1f&name=%E5%9B%BE%E7%89%872.png&originHeight=472&originWidth=800&originalType=binary&ratio=1&rotation=0&showTitle=false&size=202226&status=done&style=none&taskId=u2927a808-0a6e-4734-b659-f753f62621c&title=)
这里举百度某个页面的一个例子，max-age=5184000，单位是秒 。缓存挺长一段时间。


![图片3.png](https://cdn.nlark.com/yuque/0/2022/png/21814148/1650194959769-a0dee231-f9ff-4f2f-a468-6ee071d781ba.png#clientId=u81ddd212-b674-4&from=ui&id=u7bebf8a9&name=%E5%9B%BE%E7%89%873.png&originHeight=550&originWidth=693&originalType=binary&ratio=1&rotation=0&showTitle=false&size=116131&status=done&style=none&taskId=ubcd07ee6-346a-4ec9-b042-6772b11fb85&title=)
如果客户端再次请求，之前有Cache-Control，客户端会把这个资源给缓存下来。再次请求的时候，它只要判断这个Cache-Control这个时间还有效，没有过期，然后浏览器就会在本地缓存里面去找这个资源，他就不会到服务端，不经过网络，然后直接返回这个资源。这样就会更快一些，因为读取本地缓存是一个非常快的一个过程。

        
![图片4.png](https://cdn.nlark.com/yuque/0/2022/png/21814148/1650195378483-7d3c542e-00df-49fd-a1ac-6f55cb45b6ee.png#clientId=u81ddd212-b674-4&from=ui&id=u2faa2404&name=%E5%9B%BE%E7%89%874.png&originHeight=316&originWidth=933&originalType=binary&ratio=1&rotation=0&showTitle=false&size=84422&status=done&style=none&taskId=u1ccfd950-7e0a-4bec-8d44-2afd981c7d5&title=)

 这里是一个例子，它使我们达到了要加快访问速度的一个目的。前提是你之前有过初次请求并且服务端已经设置了Cache-Control，然后到浏览器，浏览器会自动地根据Cache-Control，来把这个资源存下来。


如果有一天，缓存失效了，也就是说浏览器判断之前的Cache-Control的这个max-age的时间和现在对不上了，缓存已经失效了，已经超过最大的一个时间，这个时候浏览器就会再次去请求服务端，再次请求服务端，服务端会重新返回这个资源和 Cache-Control，又去设置了一个新的过期时间 max-age。如果再次请求，就又会执行一遍刚刚的逻辑。

这就是http缓存策略中的强制缓存。

### 2.协商缓存
协商缓存是一个服务端缓存策略，也就是，服务端来判断这个资源是不是可以使用缓存。

如果和本地缓存的资源一致，服务端返回304，命中缓存；否则返回200和最新的资源。
![图片7.png](https://cdn.nlark.com/yuque/0/2022/png/21814148/1650196961356-c3c79f8e-0a80-4384-bae9-74661d78ce19.png#clientId=u81ddd212-b674-4&from=ui&id=ubcbc78df&name=%E5%9B%BE%E7%89%877.png&originHeight=546&originWidth=732&originalType=binary&ratio=1&rotation=0&showTitle=false&size=126550&status=done&style=none&taskId=uc0ddc555-ec7b-4d33-9256-f06bc4db13b&title=)

这里因为资源标识比较短，体积比较小，我们带上之后他可以很快地到达我们这个服务端。

这里资源标识，首先它是在response headers里面的，因为它是服务端返回的，有两种：

Last-Modified：资源的最后修改时间

Etag：资源的唯一标识（服务端可以根据资源的文件内容生成它唯一的一个标识，通常是一个字符串，类似于人的指纹）
![图片8.png](https://cdn.nlark.com/yuque/0/2022/png/21814148/1650197574974-094e1803-7926-4f28-9e5e-8b17820963ca.png#clientId=u81ddd212-b674-4&from=ui&id=u097abad6&name=%E5%9B%BE%E7%89%878.png&originHeight=558&originWidth=834&originalType=binary&ratio=1&rotation=0&showTitle=false&size=131692&status=done&style=none&taskId=u00bbc7c9-d8cd-4aa7-b3a0-7828f260ed4&title=)
if-modified-since：它的值就是Last-Modified，就是这个资源的最后修改时间

初次请求到服务端，服务端感觉这个资源可以被缓存，然后就返回资源，然后这个Last-Modified（资源的最后修改时间），然后到浏览器，浏览器接收到资源之后，就可以把资源先缓存起来，因为将来它可能会命中缓存。
如果是一样那就证明我之前在返回这个last-modified的之后，我服务端的资源还没有改过。如果是在这种情况下，服务端会返回一个304，告诉浏览器说，我们这个资源从上次返回到现在都没有改动过，你可以继续用缓存，这个时候这次返回，体积就非常小，因为它只返回了304的一个状态码，效率非常高。

如果有一种情况说，我们上次返回资源之后，我们的这个资源被修改了，这个之前的if-modified-since的时间就不是最新的了，服务端就知道你请求的资源已经被改过了，这个时候我就可以返回一个新的last-modified，而不是304了，所以说我们就返回一个200和新的资源以及last-modified。if-modified-since带的永远是最近一次返回的last-modified的返回的那个时间。然后服务端根据这个if-modified-since带来的这个时间和我这个资源最后修改时间做一个协商做一个对比，然后看看能不能返回一个304，如果说资源被改了，那我们哪怕慢一点我们也不能返回一个错误的信息。我就直接返回200,资源，新的last-modified，力求下次能命中缓存。
![图片9.png](https://cdn.nlark.com/yuque/0/2022/png/21814148/1650197955028-0c4ce948-1917-451b-a663-0a699abcd657.png#clientId=u81ddd212-b674-4&from=ui&id=uf19c450c&name=%E5%9B%BE%E7%89%879.png&originHeight=558&originWidth=863&originalType=binary&ratio=1&rotation=0&showTitle=false&size=122146&status=done&style=none&taskId=u358851eb-ea9d-4192-aef3-dbf0d9f9b1f&title=)
if-none-match：它的值就是Etag，就是这个资源的唯一标识。

Etag是一样的，具体过程类比last-modified。只不过etag是拿这个资源算一个类似于指纹一样的字符串（唯一的）来做对比，做协商。最后的结果呢就是如果命中成功，我们就返回一个304，否则就返回200，新的资源，新的etag。
![图片10.png](https://cdn.nlark.com/yuque/0/2022/png/21814148/1650198042414-98464e2b-49b9-4be5-a147-c03b45bc3014.png#clientId=u81ddd212-b674-4&from=ui&id=uea2c92d9&name=%E5%9B%BE%E7%89%8710.png&originHeight=439&originWidth=1061&originalType=binary&ratio=1&rotation=0&showTitle=false&size=217145&status=done&style=none&taskId=u9463bf09-d7c4-4416-b940-f0396bd33e6&title=)
![图片11.png](https://cdn.nlark.com/yuque/0/2022/png/21814148/1650198109932-36a26fe2-8525-43ff-b5b6-818799d94914.png#clientId=u81ddd212-b674-4&from=ui&id=ud26d1fba&name=%E5%9B%BE%E7%89%8711.png&originHeight=513&originWidth=738&originalType=binary&ratio=1&rotation=0&showTitle=false&size=162818&status=done&style=none&taskId=u258697ad-1a87-4318-bbb5-7e8a236d758&title=)
没有返回新的资源，只是返回一个304 , 这个size是非常小的。0.6k和5.6kb相比中间相差还是非常大的。所以说，命中缓存是一个非常高效非常快速的一个方式。

共存的话，会优先使用etag，原因是last-modified只能精确到秒级，秒级对于计算机来说他还是比较宽泛的一个时间段。码农角度来看计算机我们所有的程序执行是以毫秒为单位的。甚至是在毫秒以内，所以说秒级还是比较宽泛的概念，如果资源被重复生成，而内容不变，这个etag会更精准一些。

![图片12.png](https://cdn.nlark.com/yuque/0/2022/png/21814148/1650198322725-9e7e9963-1120-42d4-89d1-6a18bd535bfb.png#clientId=u81ddd212-b674-4&from=ui&id=u476fccef&name=%E5%9B%BE%E7%89%8712.png&originHeight=554&originWidth=725&originalType=binary&ratio=1&rotation=0&showTitle=false&size=110891&status=done&style=none&taskId=u881384c6-a039-419d-8ba3-f7893b781e9&title=)
最后我们拿一个统一的图做一个例子。

首先发送请求，有缓存，也就是我们命中这个cache-control也就是强制缓存，这是客户端，然后缓存是否过期，也就是说我们cache-control里面有个max-age，也就是最大缓存时间，如果缓存没有过期的话就读取缓存，也就是强制缓存，然后页面呈现，这个就是我们讲的这个cache-control的这个强制缓存。
如果max-age过期了，那就看一下有没有etag 和last-modified，如果没有etag和last-modified，那我们没法进行我们的协商缓存，那就向http发送请求，然后服务器返回资源，然后页面呈现。

如果说有etag和last-modified，我们向服务器发送请求的时候就需要带上if-none-match和这个if-modified-since，这两个值分别是这个etag的值和last-modified这个值，让服务端去判断去协商，服务端判断这个缓存是不是可用，是服务器根据if-none-match和if-modified-since去做对比，如果是缓存可用的话，就返回304，返回304然后客户端可以读取本地缓存，然后就页面呈现，这个就是协商缓存，如果这个地方判断过期了，缓存不可用，那就是返回状态码200，直接返回资源，然后页面呈现。

以上就是Http缓存策略。

## 浏览器的三种刷新操作
![图片13.png](https://cdn.nlark.com/yuque/0/2022/png/21814148/1650207322551-3e6db248-73a9-40fd-ba3d-06f18e0fa119.png#clientId=u41c7b69f-f882-4&from=ui&id=u9480bdf6&name=%E5%9B%BE%E7%89%8713.png&originHeight=412&originWidth=859&originalType=binary&ratio=1&rotation=0&showTitle=false&size=87526&status=done&style=none&taskId=uf0ac1163-1325-4a1c-900d-f72db7f96f4&title=)
![图片14.png](https://cdn.nlark.com/yuque/0/2022/png/21814148/1650207465360-f4a89fd6-90a5-4904-b0b8-5de2fdc9896b.png#clientId=u41c7b69f-f882-4&from=ui&id=ub80543a6&name=%E5%9B%BE%E7%89%8714.png&originHeight=410&originWidth=849&originalType=binary&ratio=1&rotation=0&showTitle=false&size=126026&status=done&style=none&taskId=udfef04b4-1428-428e-8031-eede28b53a0&title=)
这三种操作对于缓存是有一定影响的：

如果手动点击刷新按钮，这个时候强制缓存就会失效，Cache-control就会失效。但是把所有的请求发给服务端，服务端协商缓存还是有效的。

强制缓存和协商缓存这两个策略，一是在客户端，一个是在服务端。

手动刷新的时候，强制缓存失效，这个时候我们还有一个兜底的方案， 就是我们在服务端可以做一个协商缓存，这样也会让我们的页面加载速度更快一些。

如果是强制刷新的话，也就是我们按住 Ctrl + F5 的话，那我们的强制缓存和协商缓存就全部都失效。因为如果我们要强制刷新，服务端肯定得把所有资源都全部返回，不管加载多慢，也要返回给我们最新的结果，所以说这两个全部失效。那就所有的请求全部都返回200，返回最新的资源。


