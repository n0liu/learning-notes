css 作用域是全局的，项目越来越大，人越来越多，命名慢慢成为了问题，于是CSS 社区也诞生了相应的模块化解决方案：BEM、Atomic CSS、OOCSS、SMACSS、ITCSS，以及 CSS Modules 和 CSS-in-JS 等。

根据这些 CSS 模块化方案的特点，简单的分为三大类：

1. **CSS 命名方法论**：通过人工的方式来约定命名规则。
2. **CSS Modules**：一个 CSS 文件就是一个独立的模块。
3. **CSS-in-JS**：在 JS 中写 CSS。

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602859/1647589265351-677ebef0-297d-4f36-8a59-2341669ee724.png#clientId=u73e146df-ac9c-4&from=paste&height=507&id=u4ac5186f&name=image.png&originHeight=507&originWidth=732&originalType=binary&ratio=1&rotation=0&showTitle=false&size=57687&status=done&style=none&taskId=uab1caeaa-0afe-42bf-8652-cd724d86aad&title=&width=732)

## 一、BEM
BEM即为块级元素修饰字符（Block Element Modifier），以 .block__element--modifier 形式命名，即 .模块名__元素名--修饰器名 三个部分，用双下划线 __ 来明确区分模块名和元素名，用双横线 -- 来明确区分元素名和修饰器名。
```javascript
<!-- 示例模块 -->
<div class="card">
  <div class="card__head">
    <ul class="card__menu">
      <li class="card__menu-item">menu item 1</li>
      <li class="card__menu-item">menu item 2</li>
      <li class="card__menu-item card__menu-item--active">menu item 3</li>
      <li class="card__menu-item card__menu-item--disable">menu item 4</li>
    </ul>
  </div>
  <div class="card__body"></div>
  <div class="card__foot"></div>
</div>
```
在 BEM 中不建议使用子代选择器，因为每一个类名已经都是全局唯一的了，除非是 block 相互嵌套的场景。
```javascript
.card {}
.card__head {}
.card__menu {}
.card__menu-item {}
.card__menu-item--active {}
.card__menu-item--disable {}
.card__body {}
.card__foot {}
```
使用 Sass/Less/Stylus 的父元素选择器 & 可以更高效的编写 BEM：
```javascript
.card {
  &__head {}
  &__menu {
    &-item {
      &--active {}
      &--disable {}
    }
  }
  &__body {}
  &__foot {}
}
```

## 二、Atomic CSS
原子化 CSS 结构。

优点是可以写基础 视觉功能小的，单用途的 CSS，相当于把每一个单一的作用定义一个Class，确保整个样式表没有一条重复的样式，这样复用性是最高的，代码也最少，但是每个元素就需要一堆的 Class。

这种思路可谓另辟蹊径，独树一帜。当然优缺点都很明显：CSS 代码最小化了，而 HTML 膨胀了；虽然不用考虑命名，但是要记一堆新规则。例如css类名为
mt-1： 对应margin-top: 1px; 
w-200：对应width: 200px;
Bgc(#0280ae.5) H(90px) IbBox W(50%) foo_W(100%)：
	width: 50%;
height: 90px;
background-color: rgba(2,128,174,.5);
更多样式规则可以参考：[https://acss.io/](https://acss.io/)

## 三、CSS module
[CSS Modules](https://link.segmentfault.com/?enc=HQgveA280ddEkV4oH6NGzQ%3D%3D.vE9Um3BECv0Goxxd%2Frt3Rmx0TNvfPZvwlP%2BI4jP5%2FlIN8631084D8bjhajKxTwd3) 是一种模块化工具。
CSS Modules 特性：

- **作用域**：模块中的名称默认都属于本地作用域，定义在 :local 中的名称也属于本地作用域，定义在 :global 中的名称属于全局作用域，全局名称不会被编译成哈希字符串。
- **命名**：对于本地类名称，CSS Modules 建议使用 camelCase 方式来命名，这样会使 JS 文件更干净，即 styles.className。
但是你仍然可以固执己见地使用 styles['class-name']，允许但不提倡。🤪
- **组合**：使用 composes 属性来继承另一个选择器的样式，这与 Sass 的 @extend 规则类似。
- **变量**：使用 @value 来定义变量，不过需要安装 PostCSS 和 [postcss-modules-values](https://link.segmentfault.com/?enc=W2EZndvQ1m6YsQfGEGU8iw%3D%3D.qtYphXVq58ZEVrIE3%2BInwN51xtQRSKriJwtzUsc%2FK1whOli97my%2BnJ6jju5%2FRU5yN%2BoVCeIe58PticT4HeN6dg%3D%3D) 插件。

示例：
### 3.1 webpack中配置css-loader
```javascript
module.exports = {
  entry: __dirname + '/index.js',
  output: {
    publicPath: '/',
    filename: './bundle.js'
  },
  module: {
    loaders: [
      {
        test: /\.jsx?$/,
        exclude: /node_modules/,
        loader: 'babel',
        query: {
          presets: ['es2015', 'stage-0', 'react']
        }
      },
      {
        test: /\.css$/,
        loader: "style-loader!css-loader?modules"
      },
    ]
  }
};
```
上面代码中，关键的一行是style-loader!css-loader?modules，它在css-loader后面加了一个查询参数modules，表示打开 CSS Modules 功能。
css-loader默认的哈希算法是[hash:base64]，这会将.title编译成._3zyde4l1yATCOkgn-DBWEL这样的字符串。webpack配置上面可以定制哈希类名：
```javascript
// const getCSSModuleLocalIdent = require('react-dev-utils/getCSSModuleLocalIdent');

module: {
  loaders: [
    // ...
    {
      test: /\.css$/,
      loader: "style-loader!css-loader?modules&localIdentName=[path][name]---[local]---[hash:base64:5]"
    },
  ]
}
```
你会发现.title被编译成了demo03-components-App---title---GpMto
                               [path][name]---[local]---[hash:base64:5]

如果是老项目中途引入CSS  Module，也可以这么配置:
```javascript
const sassRegex = /\.(scss|sass)$/;
const sassModuleRegex = /\.module\.(scss|sass)$/;
a.scss
a.module.scss


module.exports = {
  entry: __dirname + '/index.js',
  output: {
    publicPath: '/',
    filename: './bundle.js'
  },
  module: {
    loaders: [
      {
        test: /\.jsx?$/,
        exclude: /node_modules/,
        loader: 'babel',
        query: {
          presets: ['es2015', 'stage-0', 'react']
        }
      },
      {
        test: sassRegex,
        exclude: sassModuleRegex,
        loader: "style-loader!css-loader!sass-loader"
      },
      {
        test: sassModuleRegex,
        loader: "style-loader!css-loader?modules!sass-loader"
      },
    ]
  }
};
```

### 3.2 业务代码
```javascript
import React from 'react';
import style from './App.css';

export default () => {
  return (
    <>
    	<h1>四个demo</h1>
      <h1 className={style.title1}>
        第一个：local局部作用域
      </h1>
      <h2 className={gTitle2}>
        第二个：global全局作用域
      </h2>

			<div className={style.box1}>
        第三个：composes组合class
      </div>
			<div className={style.box2}>
        第四个：输入变量
      </div>
		</>
  );
};
```

#### 细说第一个：local局部作用域
```javascript
// ===== html =====
<h1 className={style.title1}>
  第一个：local局部作用域
</h1>

// ===== css =====
.title1 {
  color: red;
}

._3zyde4l1yATCOkgn-DBWEL {
  color: red;
}

:local(.title2) {
  color: green;
}
```

#### 细说第二个：global全局作用域
```javascript
// ===== html =====
<h2 className={title2}>
  第二个：global全局作用域
</h2>

// ===== css =====
:global(.title2) {
  color: green;
}
```

#### 细说第三个：composes组合class
```javascript
// ===== html =====
<div className={style.box1}>
  第三个：composes组合class
</div>

// ===== css =====
.className {
  background-color: blue;
}

.box1 {
  composes: className;
  composes: className from './another.css';
  color: red;
}

// 提问，1、支持多个composes组合吗，2、组合后样式的优先级是什么样的
```

#### 细说第四个：输入变量
CSS Modules 支持使用变量，不过需要安装 PostCSS 和 postcss-modules-values。
1、npm install --save postcss-loader postcss-modules-values
2、把 postcss-loader 加入 webpack.config.js。
3、业务代码如下：
```javascript
// ===== html =====
<div className={style.box2}>
  第四个：输入变量
</div>

// ===== css =====
@value blue: #0c77f8;
@value red: #ff0000;
@value green: #aaf200;

.box2 {
  color: red;
  background-color: blue;
}
```
使用 CSS Modules 时，推荐配合 CSS 预处理器（Sass/Less/Stylus）一起使用。
CSS 预处理器提供了许多有用的功能，如嵌套、变量、mixins、functions 等，同时也让定义本地名称或全局名称变得容易。
[

](https://blog.csdn.net/wulala_hei/article/details/84633258)
## 四、CSS in JS
css-in-js 是一种技术，而不是一个具体的库的实现。
在js文件中写css就是css-in-js技术，而不是独立为一些 css、scss或less这类的文件，这样你就可以在 css 中使用一些属于 js 的如模块声明、变量定义、函数调用和条件判断等语言特性来提供灵活的可扩展的样式定义。
css-in-js 在react社区的热度是最高的，因为 react 本身不会管用户怎么去为组件定义样式问题，而vue有属于框架自己的一套定义样式的方案。
好处：
- 支持一些js的特性
	- 继承
	- 变量
	- 函数
- 支持框架的特性
	- 传值特性
缺点：
运行成本：需要通过JavaScript加载，解析和执行样式。
PostCSS没有解析这些库，因为PostCSS不是设计用于运行时的。
语法高亮等工具还不支持。 CSS-in-JS正在以非常快的速度发展，文本编辑器扩展，linters，代码格式化等等需要追赶新功能以保持同等水平。

CSS-in-JS 库目前已有几十种实现，你可以在 [CSS in JS Playground](https://link.segmentfault.com/?enc=J%2FUyHo5xWZyXOcRjb6GUKw%3D%3D.nsDHW1o788cbVmzvCJ6mN%2BdXTOuw0J9hQpd%2BfhWsX%2B5Xqm1c7%2BPUA3elWXz2Bj9q) 上快速尝试不同的实现。下面列举一些流行的 CSS-in-JS 库：

- styled-components：[https://github.com/styled-com...](https://link.segmentfault.com/?enc=JQ%2FdZ6qZF4xMkFW9BCk3jA%3D%3D.bi9USEgrzw9TXCHBx9GKDIx6ykz%2B9zIeVhhBe7x1y53E8FUFqmLrUMKYzSkyuMDgsw24JcXGI7WwJDlm2H8qpA%3D%3D) 33k（**推荐**）
- emotion：[https://github.com/emotion-js...](https://link.segmentfault.com/?enc=BtV1WRdonylYpVvDBJviBQ%3D%3D.OE93hrkt46EleGZou%2BCTtsvn%2FxD%2B%2F5cHIWa919NMoXMkxW6EYZdd89cn6ZIF7yp6) 13k
- Radium：[https://github.com/Formidable...](https://link.segmentfault.com/?enc=noe51xTTSiZ0fAWgc6QWFg%3D%3D.FUDUJjS1rL6tytvIyLzGnMnAKqfWY0poZOsLmVLGDorojohMEZ4rRgYIkJtkD4Ep) 7k（已不再维护）
- Styled System：[https://github.com/styled-sys...](https://link.segmentfault.com/?enc=qz9aNakTZYjKC6MYCB9ztQ%3D%3D.vo3OMhUDEihsqJ8KxdWKkTNYypNe3gMWyXavtj%2BDsff63FBr9tZbDKOAHcmqyhxC) 7k
- styled-jsx：[https://github.com/vercel/sty...](https://link.segmentfault.com/?enc=rtq7F%2FFDwRVVa26xDlAzXw%3D%3D.rpaWMONvwXO0xQqh3z%2FlNIQVhdiKwL0u7VJJYDMhTU4nhx0tUVW2%2FjgY4dKMX1A8) 6k
- JSS：[https://github.com/cssinjs/jss](https://link.segmentfault.com/?enc=WDQ2H%2B6FVcqxE6g5trx1Yw%3D%3D.zZKEizlL8zGtHgtIOiBNEnWLzf%2Fa4li8bnrBfk1js6M%3D) 6k

![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602859/1647753078103-8341aebe-01f5-4516-bab9-5d30311252c4.png#clientId=u5de5f62e-0fd0-4&from=paste&height=487&id=ud6335025&name=image.png&originHeight=487&originWidth=732&originalType=binary&ratio=1&rotation=0&showTitle=false&size=122195&status=done&style=none&taskId=ue10cc413-8932-4b39-a2bb-d720c3d74c7&title=&width=732)

### 🍑 styled-components 库示例：
#### 🏃‍♀️  第一步

- 使用styled-components前需要安装：
```javascript
npm i -S styled-components
```

- 由于css后期会在模板字符串中编写，默认情况下 vsconde 是没有css样式代码片段的（写样式的时候没有代码提示的），为了提高css代码在模板字符串中编写的效率，建议安装一个vscode的扩展：
- vscode-styled-components
- ![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602859/1647751186604-aa1a0966-e2fb-4121-aa5f-e03f99a9f1c1.png#clientId=u5de5f62e-0fd0-4&from=paste&height=559&id=u30b3ddef&name=image.png&originHeight=559&originWidth=643&originalType=binary&ratio=1&rotation=0&showTitle=false&size=505338&status=done&style=none&taskId=uf0c12442-78bf-4325-a99a-cc0d9fd3699&title=&width=643)
- ![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602859/1647760646103-eb5e28e6-89ea-4281-bb51-bf6d73af5775.png#clientId=u6b998dd4-bb14-4&from=paste&height=442&id=ud4adc30e&name=image.png&originHeight=442&originWidth=637&originalType=binary&ratio=1&rotation=0&showTitle=false&size=213384&status=done&style=none&taskId=u50b6651d-8e6b-4ead-af95-b1166fac72d&title=&width=637)

#### 🏃‍♀️ 第二步 
##### 2.1 内部写法
```javascript
// ======== Basic.jsx文件 ==========
import React, { Component } from 'react';
// 导入样式组件
import styled from 'styled-components';

class Basic extends Component {
    render() {
        return (
            <div>
                <Ha>内部文件写法</Ha>
            </div>
        );
    }
}
const Ha = styled.div`
    font-size: 50px;
    color: red;
    background: pink;
    width: 100%;
    height: 100vh;
`

export default Basic;
```
##### 2.2 外部写法(导入样式组件)
```javascript
// ======== Card.jsx文件 ==========
// 导入样式组件
import { CardText } from './style';

function Card() {
  return (
    <div className="card">
      Card卡片
      <CardText>外部Card卡片写法</CardText>
    </div>
  );
}

export default Card;
```
```javascript
// ======== style.js文件 ==========
// ======== 外部写法(导入样式组件) ========
import styled from 'styled-components';

// const 标签名（首字母大写）= styled.HTML标签名`css样式`
// 导出
export const CardText = styled.div`
    font-size: 50px;
    font-family: 华文行楷;
    color: orange;
    background-color: blue;
    width: 40vw;
`
```
 展示效果如下：![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602859/1647761247586-779ee350-7b41-468d-b201-4828847fe379.png#clientId=u6b998dd4-bb14-4&from=paste&height=787&id=u4719964f&name=image.png&originHeight=787&originWidth=1439&originalType=binary&ratio=1&rotation=0&showTitle=false&size=143166&status=done&style=none&taskId=uc75704f0-143c-4e5c-a92c-e2dfda0a35b&title=&width=1439)

##### 2.3  样式继承
2.3.1. 在styled-components中也可以使用样式的继承
2.3.2. 其继承思想与react的组件继承相似：
	- 继承父的样式：
		- 父有，子没有，继承后子也有
	- 重载父的样式
		- 父有，子有，继承后子覆盖父的
```javascript
// ======== style1.js文件 ==========
// ======== 样式继承 ========
import styled from 'styled-components';

// const 标签名（首字母大写）= styled.HTML标签名`css样式`
// 导出
const Fu = styled.div`
    font-size: 50px;
    font-family:'Courier New',Courier,monospace,kai;
    color: green;
    width: 30vw;
`
// 子继承父
// 继承：color 和 font-family子没有，会用父的
// 重载：font-size两者都有，以子为准
const Zi = styled(Fu)`
    font-size: 80px;    
    background: yellowgreen;
    width: 30vw;
`

export { Fu, Zi };

```
```javascript
// ======== JiCheng.js文件 ==========
import React, { Component } from 'react';
// 导入样式组件
import {Fu, Zi} from './style1';

class JiCheng extends Component {
    render() {
        return (
            <div>
                <Fu>继承-原先的样式</Fu>
                <Zi>继承-现在的样式</Zi>
            </div>
        );
    }
}

export default JiCheng;

```

##### 2.4  属性传递

- 属性传递：样式值的动态传参（组件传值）
- 基于css-in-js的特性，在styled-components中也允许我们使用props（父传子），这样一来，我们可以对部分需要的样式进行传参，方便动态控制样式的改变
```javascript
// ======== style2.js文件 ==========
// ======== 属性传递 ========
import styled from 'styled-components';

// 动态属性传递样式的值
// 没传值就是默认值green，传了值就是值的属性
const ChuanDiStyle = styled.div`
    background: ${(props) => props.bgColor || 'red'};
    font-size: ${(props) => props.Size || '60px'};
    width: 20vw;
`
export { ChuanDiStyle };
```
```javascript
// ======== ChuanDi.js文件 ==========
import React, { Component } from 'react';
// 导入样式组件
import { ChuanDiStyle } from './style2';

class ChuanDi extends Component {
    render() {
        return (
            <div>
                <ChuanDiStyle>原先的样式</ChuanDiStyle>
                <ChuanDiStyle bgColor={'yellow'} Size='30px'>传值的样式</ChuanDiStyle>
            </div>
        );
    }
}

export default ChuanDi;
```
展示效果如下：
![image.png](https://cdn.nlark.com/yuque/0/2022/png/25602859/1647762607463-80dbf282-1e36-43e2-9200-c86f810a527a.png#clientId=u6b998dd4-bb14-4&from=paste&height=786&id=u0f1d1634&name=image.png&originHeight=786&originWidth=1439&originalType=binary&ratio=1&rotation=0&showTitle=false&size=162086&status=done&style=none&taskId=u56989cd2-a88c-4088-8572-60cf7d05649&title=&width=1439)

### 扩展 -》定制表格
参考：[https://segmentfault.com/a/1190000017549783](https://segmentfault.com/a/1190000017549783)
### 扩展-》主题色
ThemeProvider 官方文档：[https://styled-components.com/docs/advanced#theming](https://styled-components.com/docs/advanced#theming)
```javascript
   const Wrapper = styled.div`
    /* 应用于Wrapper组件本身和Wrapper组件里的所有html标签 */
    	color: black;

    /* 应用于Wrapper组件里的h3标签 */
    h3 {
    	color: red
    }

    /* 应用于Wrapper组件里的className为blue的html标签 */
    .blue {
    	color: blue
    }
  `

  render(
    <Wrapper>
      <p>黑色 p 标签 </p>
      <h3>红色 h3 标签</h3> 
      <p className="blue" >蓝色 p 标签</p>
    </Wrapper>
  )
```
```javascript
  // react 中使用 styled-components
  import styled, { ThemeProvider } from 'styled-components';
  
  const Box = styled.div`
    color: ${props => props.theme.color};
  `;
  
  <ThemeProvider theme={{ color: 'mediumseagreen' }}>
    <Box>I'm mediumseagreen!</Box>
  </ThemeProvider>
```

CSS Modules 与 styled-components 是两种截然不同的 CSS 模块化方案，它们最本质的区别是：前者是在外部管理 CSS，后者是在组件中管理 CSS。两者没有孰好孰坏。

### styled-components更多使用技巧
（更具体的内容请参考 [官方文档](https://link.segmentfault.com/?enc=5ttmy4UvoGcBV%2FppAEfwJA%3D%3D.Zdr713jjMzuhCdF1w8nmF8YIZ45bMK7d6aWe0n7%2FINo%3D)）：

- 可以通过插值的方式给样式组件传递参数（props），这在需要动态生成样式规则时特别有用。
- 可以通过构造函数 styled() 来继承另一个组件的样式。
- 使用 createGlobalStyle 来创建全局 CSS 规则。
- styled-components 会为自动添加浏览器兼容性前缀。
- styled-components 基于 [stylis](https://link.segmentfault.com/?enc=kRSPtxoaSqyAgmzEHCROJQ%3D%3D.7Xc4diIe7T9JC%2F%2B%2BoE3NwHaGl3OI4VEcl7DIhh7DGRZcxJXQ%2BJANlhp4rWFtfPbx)（一个轻量级的 CSS 预处理器），你可以在样式组件中直接使用嵌套语法，就像在 Sass/Less/Stylus 中的那样。
- 强烈推荐使用 styled-components 的 Babel 插件 [babel-plugin-styled-components](https://link.segmentfault.com/?enc=3kEEvE1RWGJa1fyx9vTZxw%3D%3D.AAlY8doG1mj5nZnksyWUPVbscQjXnl7vJQsNblpUhp5R3%2BfVD%2F5EVVGsilVpxHOyjC0IvGcxFFnk%2Fpnx7TPGipVTMiUrTh8pv8N5ERtEZrA%3D)（当然这不是必须的）。它提供了更好的调试体验的支持，比如更清晰的类名、SSR 支持、压缩代码等等。
- 你也可以在 Vue 中使用 styled-components，[vue-styled-components](https://link.segmentfault.com/?enc=xEb3JzERsX%2BSUq20dsgFTQ%3D%3D.5UeZvYAWC8N28Lw7aR3F1yFRyHJRFDXBmEr0MHrWHtIIE3tk8hUh%2Fvk8LOogJTT8i%2B0f8dwDXTQg%2Bc2kuS7GIA%3D%3D)，不过好像没人会这么做\~
- 默认情况下，模版字符串中的 CSS 代码在 VSCode 中是没有智能提示和语法高亮效果的，需要安装 [扩展](https://link.segmentfault.com/?enc=QiXf%2B344Z4lTUziLw6KLiQ%3D%3D.FvccRb9yrggzVRPeInehrYk4DTgLuV%2BFSBdA%2FAvh9Wxl%2FPxOzV1dVOXE43pvWpx9UsKi2pdAdryXBd5cTKLLvfY2LCs3agzI0DyMh6jCxJ1qfrM%2BV14k7yHZMK%2FIYWCn)。

## 源码
### css-modules-demos：[https://gitee.com/vvweb/css-modules-demos](https://gitee.com/vvweb/css-modules-demos)
### css-in-js-demos：[https://gitee.com/vvweb/css-in-js-demo](https://gitee.com/vvweb/css-in-js-demo)
