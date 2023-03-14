# 有关布局的一些基本概念
## 标准盒模型
> **盒子模型**：每个元素，都会形成一个矩形块，主要包括四部分：margin(外边距)+border(边框)+padding(内边距)+content(内容)

![](https://cdn.nlark.com/yuque/0/2022/jpeg/21490942/1648358478553-d5ccda7e-d981-480b-bc35-153c141e71a8.jpeg#clientId=u5eea1180-31f8-4&from=paste&id=ue1270065&originHeight=446&originWidth=732&originalType=url&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=u46e8fdeb-c35b-4264-8af8-2d68b493780&title=)
### 块级盒子（Block box） 和 内联盒子（Inline box）
> 在 CSS 中我们广泛地使用两种“盒子” —— **块级盒子** (**block box**) 和 **内联盒子** (**inline box**)**。**这两种盒子会在**页面流**（page flow）和**元素之间的关系**方面表现出不同的行为:

#### 
#### 块级盒子
> 一个被定义成块级的（block）盒子会表现出以下行为:
> - 盒子会在内联的方向上扩展并占据父容器在该方向上的所有可用空间，在绝大数情况下意味着盒子会和父容器一样宽
> - 每个盒子都会换行
> - [width](https://developer.mozilla.org/zh-CN/docs/Web/CSS/width) 和 [height](https://developer.mozilla.org/zh-CN/docs/Web/CSS/height) 属性可以发挥作用
> - 内边距（padding）, 外边距（margin） 和 边框（border） 会将其他元素从当前盒子周围“推开”
> 
> 除非特殊指定，诸如标题(<h1>等)和段落(<p>)默认情况下都是块级的盒子。

#### 
#### 内联盒子
> 如果一个盒子对外显示为 inline，那么他的行为如下:
> - 盒子不会产生换行。
> -  [width](https://developer.mozilla.org/zh-CN/docs/Web/CSS/width) 和 [height](https://developer.mozilla.org/zh-CN/docs/Web/CSS/height) 属性将不起作用。
> - 垂直方向的内边距、外边距以及边框会被应用但是不会把其他处于 inline 状态的盒子推开。
> - 水平方向的内边距、外边距以及边框会被应用且会把其他处于 inline 状态的盒子推开。


### CSS3设定盒子模型种类
![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648358802143-6b22d046-6058-4428-85d7-311b9e0241a2.png#clientId=u5eea1180-31f8-4&from=paste&id=u4c8f2b62&name=image.png&originHeight=507&originWidth=761&originalType=url&ratio=1&rotation=0&showTitle=false&size=292959&status=done&style=none&taskId=u279fd726-04a8-4d18-89f6-a85e6665922&title=)
> box-sizing 属性允许您以特定的方式定义匹配某个区域的特定元素。
> box-sizing: content-box;  //宽度和高度分别应用到元素的内容框。在宽度和高度之外绘制元素的内边距和边框。
>  box-sizing: border-box;  //为元素设定的宽度和高度决定了元素的边框盒。就是说，为元素指定的任何内边距和边框都将在已设定的宽度和高度内进行绘制。通过从已设定的宽度和高度分别减去边框和内边距才能得到内容的宽度和高度。 
> box-sizing: inherit;// 规定应从父元素继承 box-sizing 属性的值。 即box-sizing属性可以指定盒子模型种类，content-box指定盒子模型为W3C（标准盒模型），border-box为IE盒子模型。


## 标准文档流 （Normal Flow）
> 标准文档流(normal flow)是指在不对页面进行任何布局控制时，浏览器默认的HTML布局方式。
> 标准文档流在mdn上被译为正常布局流。

```html
<p>I love my cat.</p>

<ul>
  <li>Buy cat food</li>
  <li>Exercise</li>
  <li>Cheer up friend</li>
</ul>

<p>The end!</p>
```
浏览器渲染结果
![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648355098743-5a2c40f3-1b1d-4671-b615-a1fbfe839ed7.png#clientId=u5eea1180-31f8-4&from=paste&height=202&id=uf2723a35&name=image.png&originHeight=202&originWidth=774&originalType=binary&ratio=1&rotation=0&showTitle=false&size=7655&status=done&style=none&taskId=u85c25c8a-69fd-4da5-9322-886121e00ab&title=&width=774)
> 出现在另一个元素下面的元素被描述为**块**元素，与出现在另一个元素旁边的**内联元素**不同，内联元素就像段落中的单个单词一样。

标准文档流基本按块级元素从上到下，行内元素从左到右进行渲染。元素在CSS属性的影响下可以脱离标准文档流，或在不脱离标准文档流的情况下布局样式发生变化；
## 浮动
> CSS属性：float；

应用CSS中的浮动将覆盖默认的布局行为；
浮动常常被应用于布局实现，但浮动属性最早是为了实现文字环绕效果而设计的；
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <style>
        .border {
            border: solid 1px;
        }
        .green {
            background-color: lightgreen;
        }
        .red {
            background-color: lightcoral;
        }
        .float-left {
            float: left;
        }
        .box-100 {
            width: 100px;
            height: 100px;
        }
        .box-200 {
            width: 200px;
            height: 200px;
            margin: 200px;
        }
    </style>
</head>
<body>
    <div class="box-200">
        <div class="float-left box-100 green border">float: left</div>
        <div class="red border">这段文字用于演示文字环绕。这段文字用于演示文字环绕。这段文字用于演示文字环绕。这段文字用于演示文字环绕。</div>
    </div>
</body>
</html>
```
浏览器渲染结果
![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648357992928-cfc569b2-497d-4ed5-9b9a-f9d9f59137b2.png#clientId=u5eea1180-31f8-4&from=paste&height=155&id=uc7b09f6c&name=image.png&originHeight=155&originWidth=215&originalType=binary&ratio=1&rotation=0&showTitle=false&size=7746&status=done&style=none&taskId=uf40178c5-5276-4dfa-a75e-9fda8e0aac5&title=&width=215)
### 浮动元素是如何定位的
> 正如我们前面提到的那样，当一个元素浮动之后，它会被移出正常的文档流，然后向左或者向右平移，一直平移直到碰到了所处的容器的边框，或者碰到另外一个浮动的元素。


### 清除浮动
#### 使用 clear
> 使用 clear元素浮动之后，周围的元素会重新排列，为了避免这种情况，使用 clear 属性。 
> clear 属性指定元素两侧不能出现浮动元素。
> 可以在父元素配合伪类使用，解决子元素浮动后父级坍塌问题，需注意伪类元素是行内元素；

#### 父级添加overflow属性
> 通过触发BFC方式，实现清除浮动


## 定位
> 定位(positioning)能够让我们把一个元素从它原本在正常布局流(normal flow)中应该在的位置移动到另一个位置。定位(positioning)并不是一种用来给你做主要页面布局的方式，它更像是让你去管理和微调页面中的一个特殊项的位置。
> 有五种主要的定位类型需要我们了解：
> - **静态定位(Static positioning)**是每个元素默认的属性——它表示“将元素放在文档布局流的默认位置——没有什么特殊的地方”。
> - **相对定位(Relative positioning)**允许我们相对于元素在正常的文档流中的位置移动它——包括将两个元素叠放在页面上。这对于微调和精准设计(design pinpointing)非常有用。
> - **绝对定位(Absolute positioning)**将元素完全从页面的正常布局流(normal layout flow)中移出，类似将它单独放在一个图层中。我们可以将元素相对于页面的 <html> 元素边缘固定，或者相对于该元素的_最近被定位祖先元素(nearest positioned ancestor element)_。绝对定位在创建复杂布局效果时非常有用，例如通过标签显示和隐藏的内容面板或者通过按钮控制滑动到屏幕中的信息面板。
> - **固定定位(Fixed positioning)**与绝对定位非常类似，但是它是将一个元素相对浏览器视口固定，而不是相对另外一个元素。 这在创建类似在整个页面滚动过程中总是处于屏幕的某个位置的导航菜单时非常有用。
> - **粘性定位(Sticky positioning)**是一种新的定位方式，它会让元素先保持和position: static一样的定位，当它的相对视口位置(offset from the viewport)达到某一个预设值时，他就会像position: fixed一样定位。

### 固定定位
> 固定定位(fixed positioning)同绝对定位(absolute positioning)一样，将元素从文档流(document flow)当中移出了。但是，定位的坐标不会应用于"容器"边框来计算元素的位置，而是会应用于视口(viewport)边框。利用这一特性，我们可以轻松搞出一个固定位置的菜单，而不受底下的页面滚动的影响。

### 粘性定位
> 粘性定位(sticky positioning)是最后一种我们能够使用的定位方式。它将默认的静态定位(static positioning)和固定定位(fixed positioning)相混合。当一个元素被指定了position: sticky时，它会在正常布局流中滚动，直到它出现在了我们给它设定的相对于容器的位置，这时候它就会停止随滚动移动，就像它被应用了position: fixed一样。

## BFC 块级格式上下文
> Formatting context 是 W3C CSS2.1 规范中的一个概念。它是页面中的一块渲染区域，并且有一套渲染规则，它决定了其子元素将如何定位，以及和其他元素的关系和相互作用。最常见的 Formatting context 有 Block fomatting context (简称BFC)和 Inline formatting context (简称IFC)。

### BFC的特点

1. BFC就是页面上的一个隔离的独立容器，容器里面的子元素不会影响到外面的元素，反之也如此。
2. 计算BFC的高度时，浮动元素也参与计算（故也可以达到所谓清除浮动的效果，只要将包裹层转变为BFC）。
### 下列方式会创建块格式化上下文：
> - 根元素（<html>）
> - 浮动元素（元素的 float 不是 none）
> - 绝对定位元素（元素的 position 为 absolute 或 fixed）
> - 行内块元素（元素的 display 为 inline-block）
> - 表格单元格（元素的 display 为 table-cell，HTML表格单元格默认为该值）
> - 表格标题（元素的 display 为 table-caption，HTML表格标题默认为该值）
> - 匿名表格单元格元素（元素的 display 为 table、table-row、 table-row-group、table-header-group、table-footer-group（分别是HTML table、row、tbody、thead、tfoot 的默认属性）或 inline-table）
> - overflow 计算值(Computed)不为 visible 的块元素
> - display 值为 flow-root 的元素
> - contain 值为 layout、content 或 paint 的元素
> - 弹性元素（display 为 flex 或 inline-flex 元素的直接子元素）
> - 网格元素（display 为 grid 或 inline-grid 元素的直接子元素）
> - 多列容器（元素的 column-count 或 column-width (en-US) 不为 auto，包括 column-count 为 1）
> - column-span 为 all 的元素始终会创建一个新的BFC，即使该元素没有包裹在一个多列容器中（标准变更，Chrome bug）。

### BFC的作用

1. 利用BFC避免margin重叠。
2. 清除浮动
3. 用于布局实现
## IFC内敛格式化上下文
> Inline Formatting Context 内敛格式化上下文。
> IFC的line box（线框高度由其包含行内元素中最高的实际高度计算而来（不受到竖直方向的padding/margin影响）

### 作用
> 水平居中：当一个块要在环境中水平居中时候，设置其为inline-block则会在外层产生IFC，通过text-align:center则可以使其水平居中。
> 
> 垂直居中：创建一个IFC，用其中一个元素撑开父元素的高度，然后设置其vertical-align:middle,其他行内元素则可以在此父元素下垂直居中。

# 弹性盒子（Flexbox）
## 基本概念
> Flexbox 是CSS 弹性盒子布局模块（Flexible Box Layout Module）的缩写，它被专门设计出来用于创建横向或是纵向的一维页面布局。要使用flexbox，你只需要在想要进行flex布局的父元素上应用display: flex ，所有直接子元素都将会按照flex进行布局。
> 
> 采用 Flex 布局的元素，称为 Flex 容器（flex container），简称"容器"。它的所有子元素自动成为容器成员，称为 Flex 项目（flex item），简称"项目"。

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648364289702-cae2d222-b060-4957-b9c7-d6036218dcb9.png#clientId=u5eea1180-31f8-4&from=paste&id=ue14c3710&name=image.png&originHeight=333&originWidth=563&originalType=url&ratio=1&rotation=0&showTitle=false&size=30854&status=done&style=none&taskId=u158b4d0a-7414-45f6-a37d-611a1c0d333&title=)
> 容器默认存在两根轴：水平的主轴（main axis）和垂直的交叉轴（cross axis）。主轴的开始位置（与边框的交叉点）叫做main start，结束位置叫做main end；交叉轴的开始位置叫做cross start，结束位置叫做cross end。 项目默认沿主轴排列。单个项目占据的主轴空间叫做main size，占据的交叉轴空间叫做cross size。

## 容器的属性
> - flex-direction：决定主轴的方向。
> - flex-wrap：如果一条轴线排不下，如何换行。
> - flex-flow：flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap。
> - justify-content：定义了项目在主轴上的对齐方式。
> - align-items：定义项目在交叉轴上如何对齐。
> - align-content：定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。

#### 
### flex-direction属性
> - row（默认值）：主轴为水平方向，起点在左端。
> - row-reverse：主轴为水平方向，起点在右端。
> - column：主轴为垂直方向，起点在上沿。
> - column-reverse：主轴为垂直方向，起点在下沿。

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648364965275-9e07af7a-6d73-4633-b197-a8132bc84a74.png#clientId=u5eea1180-31f8-4&from=paste&id=u515a7ecf&name=image.png&originHeight=203&originWidth=796&originalType=url&ratio=1&rotation=0&showTitle=false&size=7519&status=done&style=none&taskId=u503a40a7-f674-41f7-b876-714047a0d56&title=)
### flex-wrap属性
> - nowrap（默认）：不换行。
> - wrap：换行，第一行在上方。
> - wrap-reverse：换行，第一行在下方。

#### nowrap
![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648365104077-4b0b0c9b-a1ea-40cc-b46a-1cb33ef5241c.png#clientId=u5eea1180-31f8-4&from=paste&id=ud341d01a&name=image.png&originHeight=145&originWidth=700&originalType=url&ratio=1&rotation=0&showTitle=false&size=77009&status=done&style=none&taskId=ud9af9cf3-2854-4d16-a492-96b33942dce&title=)
#### wrap
![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648365140902-73a0aa3f-ff76-48b6-b0df-a6eb1da66480.png#clientId=u5eea1180-31f8-4&from=paste&id=u34485943&name=image.png&originHeight=177&originWidth=700&originalType=url&ratio=1&rotation=0&showTitle=false&size=103849&status=done&style=none&taskId=ub07d66f5-2b54-488f-a0ea-040fe2ef450&title=)
#### wrap-reverse
![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648365158770-f34456be-58b2-44a1-97c7-17c5ab947b8c.png#clientId=u5eea1180-31f8-4&from=paste&id=u08004e88&name=image.png&originHeight=177&originWidth=700&originalType=url&ratio=1&rotation=0&showTitle=false&size=99308&status=done&style=none&taskId=u23cd880a-0455-4dc9-b6f9-54aec9f39b9&title=)
### flex-flow属性
> flex-flow属性是flex-direction属性和flex-wrap属性的简写形式，默认值为row nowrap。

### justify-content属性
> 它可能取5个值，具体对齐方式与轴的方向有关。下面假设主轴为从左到右。它可能取5个值，具体对齐方式与轴的方向有关。下面假设主轴为从左到右。
> - flex-start（默认值）：左对齐 
> - flex-end：右对齐 
> - center： 居中 
> - space-between：两端对齐，项目之间的间隔都相等。 
> - space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648365347793-0abca85c-d3ad-4d1d-a992-edf3665d26e5.png#clientId=u5eea1180-31f8-4&from=paste&id=u8582ab1c&name=image.png&originHeight=763&originWidth=637&originalType=url&ratio=1&rotation=0&showTitle=false&size=29479&status=done&style=none&taskId=ub4e38ad0-f963-4f87-9bf4-1c6d540fd94&title=)
### align-content属性
> - flex-start：与交叉轴的起点对齐。
> - flex-end：与交叉轴的终点对齐。
> - center：与交叉轴的中点对齐。
> - space-between：与交叉轴两端对齐，轴线之间的间隔平均分布。
> - space-around：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
> - stretch（默认值）：轴线占满整个交叉轴。

### ![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648365483106-d59c600c-cb8d-4fbf-a9f5-26c6cc9e0b7a.png#clientId=u5eea1180-31f8-4&from=paste&id=u9c85295a&name=image.png&originHeight=786&originWidth=620&originalType=url&ratio=1&rotation=0&showTitle=false&size=32854&status=done&style=none&taskId=u24e28721-ee7d-4276-ae40-5c0879d2c0f&title=)
## 项目的属性
> 以下6个属性设置在项目上。
> - order
> - flex-grow
> - flex-shrink
> - flex-basis
> - flex
> - align-self

### order属性
> order属性定义项目的排列顺序。数值越小，排列越靠前，默认为0。

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648366390018-0a64d8bc-3381-466d-97d5-68cf75947c16.png#clientId=u5eea1180-31f8-4&from=paste&id=u22dedd1f&name=image.png&originHeight=480&originWidth=751&originalType=url&ratio=1&rotation=0&showTitle=false&size=16154&status=done&style=none&taskId=u89f3c765-643c-46b3-95d3-83621a7c73c&title=)
### flex-grow属性
> flex-grow属性定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大。
> 如果所有项目的flex-grow属性都为1，则它们将等分剩余空间（如果有的话）。
> 如果一个项目的flex-grow属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍。

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648366439485-ca818624-719d-4bfb-a0fc-c43f5b107d79.png#clientId=u5eea1180-31f8-4&from=paste&id=u75dad3ec&name=image.png&originHeight=211&originWidth=802&originalType=url&ratio=1&rotation=0&showTitle=false&size=7337&status=done&style=none&taskId=u71f14c1a-46c0-4094-a660-0f0828a2443&title=)
### flex-shrink属性
> flex-shrink属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。
> 如果所有项目的flex-shrink属性都为1，当空间不足时，都将等比例缩小。如果一个项目的flex-shrink属性为0，其他项目都为1，则空间不足时，前者不缩小。负值对该属性无效。

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648366472464-c77e84a4-dcb1-4f2f-a885-cc875f0a23a2.png#clientId=u5eea1180-31f8-4&from=paste&id=u2d59bd9f&name=image.png&originHeight=145&originWidth=700&originalType=url&ratio=1&rotation=0&showTitle=false&size=77486&status=done&style=none&taskId=uab8843b7-0fbe-4caf-a8ea-847fff09e85&title=)
### flex-basis属性
> flex-basis属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为auto，即项目的本来大小。
> 它可以设为跟width或height属性一样的值（比如350px），则项目将占据固定空间。

### flex属性
> flex属性是flex-grow, flex-shrink 和 flex-basis的简写，默认值为0 1 auto。后两个属性可选
> 该属性有两个快捷值：auto (1 1 auto) 和 none (0 0 auto)。
>  建议优先使用这个属性，而不是单独写三个分离的属性，因为浏览器会推算相关值。

### align-self属性
> align-self属性允许单个项目有与其他项目不一样的对齐方式，可覆盖align-items属性。默认值为auto，表示继承父元素的align-items属性，如果没有父元素，则等同于stretch。
> 该属性可能取6个值，除了auto，其他都与align-items属性完全一致。

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648366736030-8e5bac00-41ef-40fd-85bb-ade41d8fbb5e.png#clientId=u5eea1180-31f8-4&from=paste&id=u9b0b2a53&name=image.png&originHeight=390&originWidth=743&originalType=url&ratio=1&rotation=0&showTitle=false&size=18468&status=done&style=none&taskId=ua4d849e1-6a4a-4af0-9a76-e5f057b58c2&title=)
# Grid布局
## 基本概念
> 网格是一组相交的水平线和垂直线，它定义了网格的列和行。
>  CSS 提供了一个基于网格的布局系统，带有行和列，可以让我们更轻松地设计网页，而无需使用浮动和定位。
> 它将网页划分成一个个网格，可以任意组合不同的网格，做出各种各样的布局。
> Flex 布局是轴线布局，只能指定"项目"针对轴线的位置，可以看作是一维布局。Grid 布局则是将容器划分成"行"和"列"，产生单元格，然后指定"项目所在"的单元格，可以看作是二维布局。
> 下图这样的布局，就很适合用Grid网格布局实现。

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648375906113-ef9f44d5-ebc9-4446-b157-f8e09c10c286.png#clientId=u5eea1180-31f8-4&from=paste&id=u96a176dc&name=image.png&originHeight=357&originWidth=792&originalType=url&ratio=1&rotation=0&showTitle=false&size=10053&status=done&style=none&taskId=u828d4745-d51b-4dd7-99c6-5e7122a90a4&title=)
### 容器和项目
> 采用网格布局的区域，称为"容器"（container）。容器内部采用网格定位的子元素，称为"项目"（item）。
> 注意：项目只能是容器的顶层子元素，不包含项目的子元素。Grid 布局只对项目生效。

### 行和列
> 容器里面的水平区域称为"行"（row），垂直区域称为"列"（column）。

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648376186688-0d223442-5ce7-461e-ab18-e5111b1d719e.png#clientId=u5eea1180-31f8-4&from=paste&id=uc183dbcd&name=image.png&originHeight=372&originWidth=564&originalType=url&ratio=1&rotation=0&showTitle=false&size=12700&status=done&style=none&taskId=u4460c76f-e2c6-4e09-a85b-3d28f6139fa&title=)
> 上图中，水平的深色区域就是"行"，垂直的深色区域就是"列"。

### 单元格
> 行和列的交叉区域，称为"单元格"（cell）。 正常情况下，n行和m列会产生n x m个单元格。比如，3行3列会产生9个单元格。

### 网格线
> 划分网格的线，称为"网格线"（grid line）。水平网格线划分出行，垂直网格线划分出列。 正常情况下，n行有n + 1根水平网格线，m列有m + 1根垂直网格线，比如三行就有四根水平网格线。

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648376251578-e1b4adde-35e9-4c0c-bd6d-9b81878a451f.png#clientId=u5eea1180-31f8-4&from=paste&id=ubb7bb66f&name=image.png&originHeight=462&originWidth=500&originalType=url&ratio=1&rotation=0&showTitle=false&size=41284&status=done&style=none&taskId=u880e9b79-3788-4013-b1a5-c7d52b53047&title=)
> 上图是一个 4 x 4 的网格，共有5根水平网格线和5根垂直网格线。

## 容器属性
> Grid 布局的属性分成两类。一类定义在容器上面，称为容器属性；另一类定义在项目上面，称为项目属性。这部分先介绍容器属性。

### display 属性
> display: grid指定一个容器采用网格布局。

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648376410480-cfde454c-2faf-4bad-9ac7-eca3e0c32ebc.png#clientId=u5eea1180-31f8-4&from=paste&id=ub9e7cf6c&name=image.png&originHeight=311&originWidth=209&originalType=url&ratio=1&rotation=0&showTitle=false&size=12451&status=done&style=none&taskId=ud5661997-5c7f-47a2-8ffc-04c9d79ce8a&title=)
> 默认情况下，容器元素都是块级元素，但也可以设成行内元素。
> display：inline-grid；

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648376441229-62909497-6b9e-4d14-a032-3dadc657e86b.png#clientId=u5eea1180-31f8-4&from=paste&id=u03fd03e9&name=image.png&originHeight=212&originWidth=341&originalType=url&ratio=1&rotation=0&showTitle=false&size=12941&status=done&style=none&taskId=u3253b5e0-a2c3-4031-b0c9-c81ecb445d7&title=)
> 注意，设为网格布局以后，容器子元素（项目）的float、display: inline-block、display: table-cell、vertical-align和column-*等设置都将失效。

### grid-template-columns 属性 / grid-template-rows 属性
> 容器指定了网格布局以后，接着就要划分行和列。grid-template-columns属性定义每一列的列宽，grid-template-rows属性定义每一行的行高。

```css
.container {
  display: grid;
  grid-template-columns: 100px 100px 100px;
  grid-template-rows: 100px 100px 100px;
}
```
> 上面代码指定了一个三行三列的网格，列宽和行高都是100px。

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648376557003-cb378efe-1f19-4c8c-ac2e-62c298dd99f8.png#clientId=u5eea1180-31f8-4&from=paste&id=u1b7adc09&name=image.png&originHeight=402&originWidth=390&originalType=url&ratio=1&rotation=0&showTitle=false&size=19664&status=done&style=none&taskId=u86709f38-b4d9-4ebd-9ca3-38dfcb5aa72&title=)
#### 百分比
> 除了使用绝对单位，也可以使用百分比。

```css
.container {
  display: grid;
  grid-template-columns: 33.33% 33.33% 33.33%;
  grid-template-rows: 33.33% 33.33% 33.33%;
}
```
#### repeat()
> repeat()接受两个参数，第一个参数是重复的次数（上例是3），第二个参数是所要重复的值。
> 可以使用repeat()函数，简化重复的值。上面的代码用repeat()改写如下。

```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 33.33%);
  grid-template-rows: repeat(3, 33.33%);
}
```
> repeat()也可以重复某种模式

```css
grid-template-columns: repeat(2, 100px 20px 80px);
```
> 上面代码定义了6列，第一列和第四列的宽度为100px，第二列和第五列为20px，第三列和第六列为80px。

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648376838255-4b9cb680-0f88-43c2-8b0b-576117106a72.png#clientId=u5eea1180-31f8-4&from=paste&id=u0ff64d0b&name=image.png&originHeight=276&originWidth=521&originalType=url&ratio=1&rotation=0&showTitle=false&size=18003&status=done&style=none&taskId=u74c38db1-d682-484d-a148-6f0ccc831d2&title=)
#### auto-fill 关键字
> 有时，单元格的大小是固定的，但是容器的大小不确定。如果希望每一行（或每一列）容纳尽可能多的单元格，这时可以使用auto-fill关键字表示自动填充。

```css
.container {
  display: grid;
  grid-template-columns: repeat(auto-fill, 100px);
}
```
> 上面代码表示每列宽度100px，然后自动填充，直到容器不能放置更多的列。

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648377167539-9cddc4e7-fb80-48b0-b3f9-76868ced2d72.png#clientId=u5eea1180-31f8-4&from=paste&id=ub44f940a&name=image.png&originHeight=268&originWidth=647&originalType=url&ratio=1&rotation=0&showTitle=false&size=21447&status=done&style=none&taskId=u112ac4c5-291c-42d5-990b-00b44c0e6c8&title=)
#### fr 关键字
> 表示比例关系，网格布局提供了fr关键字（fraction 的缩写，一小部分的意思）。如果两列的宽度分别为1fr和2fr，就表示后者是前者的两倍。

```css
.container {
  display: grid;
  grid-template-columns: 1fr 1fr;
}
```
> 上面代码表示两个相同宽度的列。

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648377315260-5bf83008-9190-43fc-b913-7e89dff0893e.png#clientId=u5eea1180-31f8-4&from=paste&id=u6bce03d8&name=image.png&originHeight=585&originWidth=471&originalType=url&ratio=1&rotation=0&showTitle=false&size=24430&status=done&style=none&taskId=uff8eb6e0-ddff-4069-8bc0-9481797ff52&title=)
> fr可以与绝对长度的单位结合使用，这时会非常方便。

```css
.container {
  display: grid;
  grid-template-columns: 150px 1fr 2fr;
}
```
> 上面代码表示，第一列的宽度为150像素，第二列的宽度是第三列的一半。

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648377362537-60b54dbe-bace-4910-bd5a-0acf6a81c947.png#clientId=u5eea1180-31f8-4&from=paste&id=u2bf29ccf&name=image.png&originHeight=366&originWidth=478&originalType=url&ratio=1&rotation=0&showTitle=false&size=20676&status=done&style=none&taskId=u43c1e15a-3681-497c-8183-627d008cca4&title=)
#### minmax()
> minmax()函数产生一个长度范围，表示长度就在这个范围之中。它接受两个参数，分别为最小值和最大值。

```css
grid-template-columns: 1fr 1fr minmax(100px, 1fr);
```
> 上面代码中，minmax(100px, 1fr)表示列宽不小于100px，不大于1fr。

#### auto 关键字
> auto关键字表示由浏览器自己决定长度。通常就是单元格内的内容长度。

```css
grid-template-columns: 100px auto 100px;
```
> 上面代码中，第二列的宽度，基本上等于该列单元格的最大宽度，除非单元格内容设置了min-width，且这个值大于最大宽度。

#### 网格线的名称
> grid-template-columns属性和grid-template-rows属性里面，还可以使用方括号，指定每一根网格线的名字，方便以后的引用。

```css
.container {
  display: grid;
  grid-template-columns: [c1] 100px [c2] 100px [c3] auto [c4];
  grid-template-rows: [r1] 100px [r2] 100px [r3] auto [r4];
}
```
> 上面代码指定网格布局为3行 x 3列，因此有4根垂直网格线和4根水平网格线。方括号里面依次是这八根线的名字。 网格布局允许同一根线有多个名字，比如[fifth-line row-5]。

### grid-row-gap 属性 / grid-column-gap 属性 / grid-gap 属性
> grid-row-gap属性设置行与行的间隔（行间距），grid-column-gap属性设置列与列的间隔（列间距）。

```css
.container {
  grid-row-gap: 20px;
  grid-column-gap: 20px;
}
```
> 上面代码中，grid-row-gap用于设置行间距，grid-column-gap用于设置列间距。

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648377721434-83fce487-7fdd-4376-992c-bcdda3792042.png#clientId=u5eea1180-31f8-4&from=paste&id=u81de6924&name=image.png&originHeight=443&originWidth=448&originalType=url&ratio=1&rotation=0&showTitle=false&size=22089&status=done&style=none&taskId=u13ab720e-72bd-4e57-bee0-944e23edd33&title=)
> grid-gap属性是grid-column-gap和grid-row-gap的合并简写形式，因此，上面一段 CSS 代码等同于下面的代码。

```css
/* grid-gap: <grid-row-gap> <grid-column-gap>; */
.container {
  grid-gap: 20px 20px;
}
```
> 如果grid-gap省略了第二个值，浏览器认为第二个值等于第一个值。
> 根据最新标准，上面三个属性名的grid-前缀已经删除，grid-column-gap和grid-row-gap写成column-gap和row-gap，grid-gap写成gap。

### grid-template-areas 属性
> 网格布局允许指定"区域"（area），一个区域由单个或多个单元格组成。grid-template-areas属性用于定义区域。

```css
.container {
  display: grid;
  grid-template-columns: 100px 100px 100px;
  grid-template-rows: 100px 100px 100px;
  grid-template-areas: 'a b c'
                       'd e f'
                       'g h i';
}
```
> 上面代码先划分出9个单元格，然后将其定名为a到i的九个区域，分别对应这九个单元格。多个单元格合并成一个区域的写法如下。

```css
grid-template-areas: 'a a a'
                     'b b b'
                     'c c c';
```
> 如果某些区域不需要利用，则使用"点"（.）表示。

```css
grid-template-areas: 'a . c'
                     'd . f'
                     'g . i';
```
> 上面代码中，中间一列为点，表示没有用到该单元格，或者该单元格不属于任何区域。实际效果就是网格布局那一列空缺了，直接可以看到容器的背景。
> 
> 注意，区域的命名会影响到网格线。
> 每个区域的起始网格线，会自动命名为区域名-start，终止网格线自动命名为区域名-end。
> 比如，区域名为header，则起始位置的水平网格线和垂直网格线叫做header-start，终止位置的水平网格线和垂直网格线叫做header-end。

### grid-auto-flow 属性
> 划分网格以后，容器的子元素会按照顺序，自动放置在每一个网格。默认的放置顺序是"先行后列"，即先填满第一行，再开始放入第二行，即下图数字的顺序。

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648378247283-3349d19c-ed7e-46a5-bda2-bfbf13e727bb.png#clientId=u5eea1180-31f8-4&from=paste&id=ufe714494&name=image.png&originHeight=402&originWidth=390&originalType=url&ratio=1&rotation=0&showTitle=false&size=19664&status=done&style=none&taskId=u82eca8fe-de67-42de-a670-3a63f7e1e11&title=)
> 这个顺序由grid-auto-flow属性决定，默认值是row，即"先行后列"。也可以将它设成column，变成"先列后行"。

```css
grid-auto-flow: column;
```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648378275144-2eba7f08-e18b-45bd-b70b-b597756c8a50.png#clientId=u5eea1180-31f8-4&from=paste&id=uf11c7f07&name=image.png&originHeight=395&originWidth=398&originalType=url&ratio=1&rotation=0&showTitle=false&size=20115&status=done&style=none&taskId=ua6d8aafd-c063-4d7b-a556-dd0e9ecf2dd&title=)
> grid-auto-flow属性除了设置成row和column，还可以设成row dense和column dense。这两个值主要用于，某些项目指定位置以后，剩下的项目怎么自动放置。
> 
> 下面的例子让1号项目和2号项目各占据两个单元格，然后在默认的grid-auto-flow: row情况下，会产生下面这样的布局。

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648378305651-0ac21b3a-278e-48e8-818d-609c1f063ff7.png#clientId=u5eea1180-31f8-4&from=paste&id=ub020408b&name=image.png&originHeight=508&originWidth=389&originalType=url&ratio=1&rotation=0&showTitle=false&size=21528&status=done&style=none&taskId=u8a2d9874-4596-40b5-9ee8-3c811a42c48&title=)
> 上图中，1号项目后面的位置是空的，这是因为3号项目默认跟着2号项目，所以会排在2号项目后面。 现在修改设置，设为row dense，表示"先行后列"，并且尽可能紧密填满，尽量不出现空格。

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648378333589-96c0dcda-7bd2-4b4b-9c02-4d54bb2cc7fa.png#clientId=u5eea1180-31f8-4&from=paste&id=u89a3ef30&name=image.png&originHeight=511&originWidth=401&originalType=url&ratio=1&rotation=0&showTitle=false&size=21729&status=done&style=none&taskId=u52384226-86db-45a6-8ac0-ae6d412a7bc&title=)
> 上图会先填满第一行，再填满第二行，所以3号项目就会紧跟在1号项目的后面。8号项目和9号项目就会排到第四行。 如果将设置改为column dense，表示"先列后行"，并且尽量填满空格。

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648378362142-22ce597f-efb5-41a5-bc81-a1d9a0d743c1.png#clientId=u5eea1180-31f8-4&from=paste&id=u4957f479&name=image.png&originHeight=393&originWidth=476&originalType=url&ratio=1&rotation=0&showTitle=false&size=21527&status=done&style=none&taskId=ucd5cb2c7-0855-4983-ba03-6f14c78eb23&title=)
### justify-items 属性 / align-items 属性 / place-items 属性
> justify-items属性设置单元格内容的水平位置（左中右），align-items属性设置单元格内容的垂直位置（上中下）。

```css
.container {
  justify-items: start | end | center | stretch;
  align-items: start | end | center | stretch;
}
```
> 这两个属性的写法完全相同，都可以取下面这些值。
> - start：对齐单元格的起始边缘。
> - end：对齐单元格的结束边缘。
> - center：单元格内部居中。
> - stretch：拉伸，占满单元格的整个宽度（默认值）。

#### justify-items: start;
![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648378633572-633e9336-44b2-4583-ad64-531acbf6ed39.png#clientId=u5eea1180-31f8-4&from=paste&id=ue40af564&name=image.png&originHeight=229&originWidth=579&originalType=url&ratio=1&rotation=0&showTitle=false&size=35062&status=done&style=none&taskId=uf724af7a-d20a-4b44-9f03-88b8bac006d&title=)
#### align-items: start;
![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648378665897-8b37f138-f838-4906-a45c-06959f64406f.png#clientId=u5eea1180-31f8-4&from=paste&id=uf1d673fb&name=image.png&originHeight=226&originWidth=569&originalType=url&ratio=1&rotation=0&showTitle=false&size=30894&status=done&style=none&taskId=u1d933023-1968-4d6c-bcbf-87047ab27bf&title=)
> place-items属性是align-items属性和justify-items属性的合并简写形式。
> place-items: <align-items> <justify-items>;
> 如果省略第二个值，则浏览器认为与第一个值相等。

### justify-content 属性 / align-content 属性 / place-content 属性
> justify-content属性是整个内容区域在容器里面的水平位置（左中右），align-content属性是整个内容区域的垂直位置（上中下）。

```css
.container {
  justify-content: start | end | center | stretch | space-around | space-between | space-evenly;
  align-content: start | end | center | stretch | space-around | space-between | space-evenly;  
}
```
> 这两个属性的写法完全相同，都可以取下面这些值。（下面的图都以justify-content属性为例，align-content属性的图完全一样，只是将水平方向改成垂直方向。）

#### start - 对齐容器的起始边框。
![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648378903027-7590d2c3-8a90-4ede-b6ab-dad957fe2580.png#clientId=u5eea1180-31f8-4&from=paste&id=uf474394e&name=image.png&originHeight=349&originWidth=582&originalType=url&ratio=1&rotation=0&showTitle=false&size=48222&status=done&style=none&taskId=u83a19f87-cac0-4eb9-aaca-06c1d9d1795&title=)
#### end - 对齐容器的结束边框。
![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648378925165-5b537dc3-7b0c-440c-b7e6-f1d8e993f380.png#clientId=u5eea1180-31f8-4&from=paste&id=u8f8ae251&name=image.png&originHeight=334&originWidth=591&originalType=url&ratio=1&rotation=0&showTitle=false&size=48100&status=done&style=none&taskId=u7b4ad016-3f3b-4f03-8056-c13a960c3f6&title=)
#### center - 容器内部居中。
![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648378936620-9f2b4c4c-ce72-4b19-9d38-1c74f00ca670.png#clientId=u5eea1180-31f8-4&from=paste&id=ubfbd07c6&name=image.png&originHeight=331&originWidth=578&originalType=url&ratio=1&rotation=0&showTitle=false&size=47784&status=done&style=none&taskId=u7d1535fb-b8c7-41e8-8a7c-354e4a230ea&title=)
#### stretch - 项目大小没有指定时，拉伸占据整个网格容器。
![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648378948696-f1cdcd20-5da6-45e6-8a52-abcb3c8178e8.png#clientId=u5eea1180-31f8-4&from=paste&id=uc64ba22c&name=image.png&originHeight=343&originWidth=592&originalType=url&ratio=1&rotation=0&showTitle=false&size=49135&status=done&style=none&taskId=u21c3825c-cd7e-45fa-af98-b2e36e7c1b6&title=)
#### space-around - 每个项目两侧的间隔相等。所以，项目之间的间隔比项目与容器边框的间隔大一倍。
![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648378962070-369030be-eb50-4b2a-b469-c4d6e54746b2.png#clientId=u5eea1180-31f8-4&from=paste&id=u310ae960&name=image.png&originHeight=338&originWidth=575&originalType=url&ratio=1&rotation=0&showTitle=false&size=48902&status=done&style=none&taskId=u76f4ba5e-02cd-4852-8aa1-9ebd1cdcf1f&title=)
#### space-between - 项目与项目的间隔相等，项目与容器边框之间没有间隔。
![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648378979279-29c4e437-d599-482e-97d8-e670f399181f.png#clientId=u5eea1180-31f8-4&from=paste&id=u0d48e32e&name=image.png&originHeight=340&originWidth=575&originalType=url&ratio=1&rotation=0&showTitle=false&size=51881&status=done&style=none&taskId=ua0fc2187-7ac6-4496-847a-69d288aaeca&title=)
#### space-evenly - 项目与项目的间隔相等，项目与容器边框之间也是同样长度的间隔。
![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648378990445-636896b8-a152-42db-a325-674e3c186175.png#clientId=u5eea1180-31f8-4&from=paste&id=u6fdcff9a&name=image.png&originHeight=337&originWidth=588&originalType=url&ratio=1&rotation=0&showTitle=false&size=51050&status=done&style=none&taskId=ubf5598b2-34e8-4303-8d26-bec7b29b314&title=)
> place-content属性是align-content属性和justify-content属性的合并简写形式。
> place-content: <align-content> <justify-content>
> 如果省略第二个值，浏览器就会假定第二个值等于第一个值。

### grid-auto-columns 属性 / grid-auto-rows 属性
> 有时候，一些项目的指定位置，在现有网格的外部。比如网格只有3列，但是某一个项目指定在第5行。这时，浏览器会自动生成多余的网格，以便放置项目。
> 
> grid-auto-columns属性和grid-auto-rows属性用来设置，浏览器自动创建的多余网格的列宽和行高。它们的写法与grid-template-columns和grid-template-rows完全相同。如果不指定这两个属性，浏览器完全根据单元格内容的大小，决定新增网格的列宽和行高。
> 
> 下面的例子里面，划分好的网格是3行 x 3列，但是，8号项目指定在第4行，9号项目指定在第5行。

```css
.container {
  display: grid;
  grid-template-columns: 100px 100px 100px;
  grid-template-rows: 100px 100px 100px;
  grid-auto-rows: 50px; 
}
```
> 上面代码指定新增的行高统一为50px（原始的行高为100px）。

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648379169743-7da2ed64-ce9d-44db-9ca3-4ccafc2f5ddc.png#clientId=u5eea1180-31f8-4&from=paste&id=ufbb2666c&name=image.png&originHeight=517&originWidth=389&originalType=url&ratio=1&rotation=0&showTitle=false&size=15840&status=done&style=none&taskId=ue0510091-709b-45b8-98ff-b3b1a2f2363&title=)
### grid-template 属性 / grid 属性
> grid-template属性是grid-template-columns、grid-template-rows和grid-template-areas这三个属性的合并简写形式。
> grid属性是grid-template-rows、grid-template-columns、grid-template-areas、 grid-auto-rows、grid-auto-columns、grid-auto-flow这六个属性的合并简写形式。
> 从易读易写的角度考虑，还是建议不要合并属性，所以这里就不详细介绍这两个属性了。

## 项目属性
> 项目属性定义在项目上面。

### grid-column-start 属性 /  grid-column-end 属性 / grid-row-start 属性 /  grid-row-end 属性
> - grid-column-start属性：左边框所在的垂直网格线
> - grid-column-end属性：右边框所在的垂直网格线
> - grid-row-start属性：上边框所在的水平网格线
> - grid-row-end属性：下边框所在的水平网格线

```css
.item-1 {
  grid-column-start: 2;
  grid-column-end: 4;
}
```
> 上面代码指定，1号项目的左边框是第二根垂直网格线，右边框是第四根垂直网格线。

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648379371202-b4514cd6-a1d5-42c8-a1f5-23a44289c394.png#clientId=u5eea1180-31f8-4&from=paste&id=u89ee45b5&name=image.png&originHeight=508&originWidth=386&originalType=url&ratio=1&rotation=0&showTitle=false&size=21701&status=done&style=none&taskId=u5e15bde3-94d6-46a8-8805-3fa44b124c9&title=)
> 上图中，只指定了1号项目的左右边框，没有指定上下边框，所以会采用默认位置，即上边框是第一根水平网格线，下边框是第二根水平网格线。除了1号项目以外，其他项目都没有指定位置，由浏览器自动布局，这时它们的位置由容器的grid-auto-flow属性决定，这个属性的默认值是row，因此会"先行后列"进行排列。
> 
> 下面的例子是指定四个边框位置的效果。

```css
.item-1 {
  grid-column-start: 1;
  grid-column-end: 3;
  grid-row-start: 2;
  grid-row-end: 4;
}
```
![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648379456181-e529b51e-45db-498e-bee3-f1f2840db064.png#clientId=u5eea1180-31f8-4&from=paste&id=u5b82301f&name=image.png&originHeight=506&originWidth=388&originalType=url&ratio=1&rotation=0&showTitle=false&size=21570&status=done&style=none&taskId=ua1471e5a-3dd6-49d8-88d4-7a0f47230f4&title=)
> 这四个属性的值，除了指定为第几个网格线，还可以指定为网格线的名字。
> 这四个属性的值还可以使用span关键字，表示"跨越"，即左右边框（上下边框）之间跨越多少个网格。

```css
.item-1 {
  grid-column-start: span 2;
}
```
> 上面代码表示，1号项目的左边框距离右边框跨越2个网格。

![image.png](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648379501092-15c9672b-f63f-4a39-b72e-0b6c0b95e6b4.png#clientId=u5eea1180-31f8-4&from=paste&id=u551eb541&name=image.png&originHeight=504&originWidth=396&originalType=url&ratio=1&rotation=0&showTitle=false&size=21483&status=done&style=none&taskId=u259c3126-c3ef-4b28-9c4a-4420420a526&title=)
> 这与下面的代码效果完全一样。

```css
.item-1 { grid-column-end: span 2; }
```
> 使用这四个属性，如果产生了项目的重叠，则使用z-index属性指定项目的重叠顺序。

### grid-column 属性 /  grid-row 属性
> grid-column属性是grid-column-start和grid-column-end的合并简写形式，grid-row属性是grid-row-start属性和grid-row-end的合并简写形式。

```css
.item {
  grid-column: <start-line> / <end-line>;
  grid-row: <start-line> / <end-line>;
}
```
### grid-area 属性
> grid-area属性指定项目放在哪一个区域。
> grid-area属性还可用作grid-row-start、grid-column-start、grid-row-end、grid-column-end的合并简写形式，直接指定项目的位置。

```css
.item {
  grid-area: <row-start> / <column-start> / <row-end> / <column-end>;
}
```
### justify-self 属性 / align-self 属性 / place-self 属性
> justify-self属性设置单元格内容的水平位置（左中右），跟justify-items属性的用法完全一致，但只作用于单个项目。
> align-self属性设置单元格内容的垂直位置（上中下），跟align-items属性的用法完全一致，也是只作用于单个项目。

```css
.item {
  justify-self: start | end | center | stretch;
  align-self: start | end | center | stretch;
}
```
> 这两个属性都可以取下面四个值。
> - start：对齐单元格的起始边缘。
> - end：对齐单元格的结束边缘。
> - center：单元格内部居中。
> - stretch：拉伸，占满单元格的整个宽度（默认值）。
> 
> place-self属性是align-self属性和justify-self属性的合并简写形式。
> place-self: <align-self> <justify-self>;
> 如果省略第二个值，place-self属性会认为这两个值相等。


# 常见布局实现
## 垂直水平居中
### 使用position定位
```html
<div class="center">test</div>
```
```css
  /* 这种通过margin：auto实现居中的方式需要在确定目标元素宽高时才能使用 */
  .center {
    background: red;
    width: 100px;
    height: 100px;
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    margin: auto;
  } 
```
```css
  .center {
    background: red;
    width: 100px;
    height: 100px;
    position: absolute;
    top: 50%;
    left: 50%;
    margin: -50px 0 0 -50px;
  } 
```
```css
  .center {
    color: red;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%,-50%);
  }
```
### 使用flex布局
```html
<div class="wrap">
  <div class="item">test</div>
</div>
```
```css
  .wrap {
    width: 100%;
    height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  .item {
    color: red;
  }
```
### 使用伪类
```html
<div class="wrap">
  <div class="item">test</div>
</div>
```
```css
  .wrap {
    width: 100%;
    height: 100%;
    background-color: #009ef4;
    text-align: center;
    position: absolute;
    top: 0;
    left: 0;
  }

  .wrap:after {
    display: inline-block;
    content: '';
    width: 0;
    height: 100%;
    vertical-align: middle;
  }

  .item {
    color: red;
    display: inline-block;
    vertical-align: middle;
  }
```
### 使用表格
```html
  <div class="wrap">
    <div class="item">
      test
    </div>
  </div>
```
```css
  .wrap {
    width: 100%;
    height: 100vh;
    display: table;
  }

  .item {
    color: #F00;
    display: table-cell;
    vertical-align: middle;
    text-align: center;
  }
```
## 两列布局
### flaot + margin实现
```html
<body>
  <div class="left">定宽</div>
  <div class="right">自适应</div>
</body>
```
```css
.left{
  width: 200px;
  height: 600px;
  background: red;
  float: left;
  display: table;
  text-align: center;
  line-height: 600px;
  color: #fff;
}

.right{
  margin-left: 210px;
  height: 600px;
  background: yellow;
  text-align: center;
  line-height: 600px;
}
```
![](https://cdn.nlark.com/yuque/0/2022/jpeg/21490942/1648381699318-a5bafb08-a742-47e9-bf95-20052715cae7.jpeg#clientId=u5eea1180-31f8-4&from=paste&id=u2cde2880&originHeight=471&originWidth=732&originalType=url&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=uc028cb60-a771-46f3-bc40-6201b4b6ae1&title=)
> 可以使用position实现相似效果。

### grid实现
```css
.wrapper {
  display: grid;
  grid-template-columns: 30% 70%;
}
```
> 上面代码将左边栏设为30%，右边栏设为70%。

## 三列布局
### 左右float，中间margin
```html
<div class="left">左栏</div>
<div class="right">右栏</div>
<div class="middle">中间栏</div>
```
```css
.left{
  width: 200px;height: 300px; background: yellow; float: left;    
}
.right{
  width: 150px; height: 300px; background: green; float: right;
}
.middle{
  height: 300px; background: red; margin-left: 220px; margin-right: 160px;
}
```
![](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648382029240-00f38078-4fbe-459d-b6b5-16acf129b5c0.png#clientId=u5eea1180-31f8-4&from=paste&id=u5cd07040&originHeight=215&originWidth=452&originalType=url&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=uc2dcb61c-8083-4026-990e-f81dc82111f&title=)
> 缺点是：1. 当宽度小于左右两边宽度之和时，右侧栏会被挤下去；2. html的结构不正确

### 左右position，中间margin
```html
<div class="left">左栏</div>
<div class="right">右栏</div>
<div class="middle">中间栏</div>
```
```css
.left{
    background: yellow;
    width: 200px;
    height: 300px;
    position: absolute;
    top: 0;
    left: 0;
}
.middle{
    height: 300px;
    margin: 0 220px;
    background: red;
}
.right{
    height: 300px;
    width: 200px;
    position: absolute;
    top: 0;
    right: 0;
    background: green;
}
```
![](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648382108998-8612da52-477d-4207-aac4-0e2e592b9301.png#clientId=u5eea1180-31f8-4&from=paste&id=u79064438&originHeight=217&originWidth=457&originalType=url&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=uc6c0416d-1d33-450c-9cbb-cfa3322bab2&title=)
> 好处是：html结构正常。
> 缺点时：当父元素有内外边距时，会导致中间栏的位置出现偏差

### flex布局
```html
<div class="left">左栏</div>
<div class="right">右栏</div>
<div class="middle">中间栏</div>
```
```css
.wrapper{
    display: flex;
}
.left{
    width: 200px;
    height: 300px;
    background: green;
}
.middle{
    width: 100%;
    background: red;
    marign: 0 20px;
}
.right{
    width: 200px;
    height: 3000px;
    background: yellow;
}
```
![](https://cdn.nlark.com/yuque/0/2022/png/21490942/1648382208717-4a4c8301-2ce1-4dbf-8356-1ed050fe9261.png#clientId=u5eea1180-31f8-4&from=paste&id=u3ec5e94d&originHeight=215&originWidth=452&originalType=url&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=u8e4b12dc-9b4e-4791-aaa9-63635f4bdad&title=)
> 除了兼容性，一般没有太大的缺陷

### Grid实现
```css
.wrapper {
  display: grid;
  grid-template-columns: 20% 60% 20%;
}
```
> 上面代码将左边栏设为20%，中栏设为60%，右边栏设为70%。

### 圣杯布局 - 常规
> - 两侧定宽，中间自适应
> - 主要内容优先渲染

```html
<div class="container">
    <div class="main">main</div>
    <div class="left">left</div>
    <div class="right">right</div>
</div>
```
```html
.container {
  padding-left: 200px;  /* 预留左侧空间，为.left宽度*/
  padding-right: 300px; /* 预留左侧空间，为.right宽度*/
}
.main {
  float: left;
  width: 100%;
  height: 300px;
  background: #67c23a;
}
.left {
  float: left;
  margin-left: -100%;   /* 移动到左侧，100%是一个父元素宽度，这里也就是.container的宽度 */
  position: relative;   /* 因为.container设置了padding*/
  right: 200px;         /* 所以需要再向左移动自身宽度,left: -200px;也是可以的 */
  width: 200px;
  height: 300px;
  background: #e6a23c;
}
.right {
  float: left;
  margin-right: -300px; /* 移动到右侧，自身宽度*/
  width: 300px;
  height: 300px;
  background: #f56c6c;
}
```
#### 第一步
> 首先设置好.main、.left、.right的宽度并浮动，为左右两列预留出空间。

```css
.container {
  padding-left: 200px;  /* 预留左侧空间，为.left宽度*/
  padding-right: 300px; /* 预留右侧空间，为.right宽度*/
}
.main {
  float: left;
  width: 100%;
  height: 300px;
  background: #67c23a;
}
.left {
  float: left;
  width: 200px;
  height: 300px;
  background: #e6a23c;
}
.right {
  float: left;
  width: 300px;
  height: 300px;
  background: #f56c6c;
}
```
#### 第二步
> 通过负margin、position把<div class="left">left</div>移动到左侧预留位置。

```css
.left {
  float: left;
  margin-left: -100%;   /* 移动到左侧，100%是一个父元素宽度，这里也就是.container的宽度 */
  position: relative;   /* 因为.container设置了padding */
  right: 200px;         /* 所以需要再向左移动自身宽度,left: -200px;也是可以的 */
  width: 200px;
  height: 300px;
  background: #e6a23c;
}
```
#### 第三步
> 通过负margin把<div class="right">right</div>移动到右侧预留位置。

```css
.right {
  float: left;
  margin-right: -300px; /* 移动到右侧，自身宽度*/
  width: 300px;
  height: 300px;
  background: #f56c6c;
}
```
### 圣杯布局 - 利用BFC
```html
    <div class="left">left</div>
    <div class="right">right</div>
    <div class="main">main</div>
```
```css
.main {
  width: auto;
  height: 300px;
  background: #67c23a;
  overflow: hidden;
}

.left {
  float: left;
  width: 200px;
  height: 300px;
  background: #e6a23c;
}

.right {
  float: right;
  width: 300px;
  height: 300px;
  background: #f56c6c;
}
```
## sticky footer
> 如果页面内容不够长的时候，页脚块粘贴在视窗底部；如果内容足够长时，页脚块会被内容向下推送

### 为内容区域添加最小的高度
> 这种方法重要用vh(viewpoint height)来计算整体视窗的高度(1vh等于视窗高度的1%),然后减去底部footer的高度，从而求得内容区域的最小高度。例如我们可以添加如下样式：

```css
.content {
	min-height: calc(100vh-footer高度);
	box-sizing: border-box;
}
```
### 使用flex布局
> 这种方法就是利用flex布局对视窗高度进行分割。footer的flex设为0，这样footer获得其固有的高度;content的flex设为1，这样它会充满除去footer的其他部分。

```css
body {
	display: flex;
  flex-flow: column;
  min-height: 100vh;
}
.content {
	flex: 1;
}
.footer {
	flex: 0;
}
```
