# 一. Typescript 概念
  - TypeScript 是添加了类型系统的 JavaScript（超集），适用于任何规模的项目
  - TypeScript 是一门静态类型、弱类型的语言
  - TypeScript 是完全兼容 JavaScript 的，它不会修改 JavaScript 运行时的特性
  - TypeScript 拥有很多编译选项，类型检查的严格程度由你决定
  - TypeScript 可以和 JavaScript 共存，这意味着 JavaScript 项目能够渐进式的迁移到 TypeScript
  - TypeScript 增强了编辑器（IDE）的功能，提供了代码补全、接口提示、跳转到定义、代码重构等能力
  - TypeScript 拥有活跃的社区，大多数常用的第三方库都提供了类型声明
  - TypeScript 与标准同步发展，符合最新的 ECMAScript 标准（stage 3）
# 二. 安装 Typescript
在开发环境下安装 tsc 命令
```javascript
npm install typescript --dev/yarn add typescript --dev
//npm或yarn安装
```
编译一个 TypeScript 文件
```powershell
yarn tsc xxx.ts
```
我们约定使用 TypeScript 编写的文件以 .ts 为后缀，用 TypeScript 编写 React 时，以 .tsx 为后缀。

# 三. tsconfig
创建 tsconfig.json 文件
```powershell
.\node_modules\.bin\tsc --init / yarn tsc --init
```
常用的 tsconfig 选项以及注解
```json
{
	"compilerOptions": {
		"target": "ESNext", // 编译的目标是什么版本的
		"lib": [ // 编译过程中需要引入的库文件的列表
			"es5",
			"es2015",
			"es2016",
			"es2017",
			"es2018",
			"dom"
		],
		"sourceMap": true, // 是否生成 map 文件
		"strict": true,   //是否开启严格模式
		
		"allowUnreachableCode": true, // 不报告执行不到的代码错误。
		"allowUnusedLabels": false, // 不报告未使用的标签错误
		"alwaysStrict": false, // 以严格模式解析并为每个源文件生成 "use strict"语句
		"baseUrl": ".", // 工作根目录
		"experimentalDecorators": true, // 启用实验性的 ES 装饰器
		"jsx": "react", // 在 .tsx 文件里支持 JSX
		"module": "commonjs", // 指定生成哪个模块系统代码
		"noImplicitAny": false, // 是否默认禁用 any
		"removeComments": true, // 是否移除注释
		"types": [ //指定引入的类型声明文件，默认是自动引入所有声明文件，一旦指定该选项，则会禁用自动引入，改为只引入指定的类型声明文件，如果指定空数组[]则不引用任何文件
			"node", // 引入 node 的类型声明
		],
		"paths": { // 指定模块的路径，和 baseUrl 有关联，和 webpack 中 resolve.alias 配置一样
			"src": [ //指定后可以在文件之直接 import * from 'src';
				"./src"
			],
		},
		"outDir": "dist", // 输出目录
		"rootDir": "src", // 文件目录
		"declaration": true, // 是否自动创建类型声明文件
		"declarationDir": "./lib", // 类型声明文件的输出目录
		"allowJs": true, // 允许编译 javascript 文件。
	},
	// 指定一个匹配列表（属于自动指定该路径下的所有 ts 相关文件）
	"include": [
		"src/**/*"
	],
	// 指定一个排除列表（include 的反向操作）
	"exclude": [
		"demo.ts"
	],
	// 指定哪些文件使用该配置（属于手动一个个指定文件）
	"files": [
		"demo.ts"
	]
}
```
# 四. Typescript 基础类型
### 1.原始数据类型(Primitive data types)

原始数据类型包括：布尔值、数值、字符串、null、undefined 以及 ES6 中的新类型 Symbol 和 ES2020 中的新类型 BigInt
```javascript
const a:string='123'
const b:number=123
const c:boolean=true;
//const d:boolean=null;
const e:void=undefined;
const f:null=null;
const g:undefined=undefined;
const h:symbol=Symbol();
const i:bigint=BigInt(9007199254740992);
```
### 2.Object 类型(Object types)

在 Typescript 中的 object 并不单指普通的对象类型，是泛指所有非原始数据类型，也就是对象、数组、函数
```javascript
const fun1:object={};
const fun2:object=[];
const fun3:object=function(){};
//这里的 object 是全小写
```
如果需要声明一个普通的对象类型，就需要使用类似于对象字面量的语法
```javascript
const obj:{attr1:number,attr2:string}={age:18,name:'lgl'}
```
但是在 typescript 中限制对象类型一般会使用接口,这里就不做过多的介绍了
### 3.Array 类型(Array types)

在 Typescript 中，数组类型有多种定义方式，比较灵活。常见如下两种
```javascript
const arr1: number[] = [1, 2, 3]
//类型 + 方括号
const arr2: Array <number> = [1,2,3]
//数组泛型
```
### 4.元组类型(Tuple types)

元组（Tuple）是合并不同类型的对象，数组是合并了相同类型的对象
```javascript
const tuple:[number,string]=[18,'lgl']
const age=tuple[0];
const name=tuple[1];
//用数组下标的方式获取元组中每一个元素的值
const [age1,name1]=tuple
//数组结构
Object.entries({
  age:18,
  name:'lgl'
})
//Object.entries()方法返回一个给定对象自身可枚举属性的键值对数组
//其排列与使用 for...in 循环遍历该对象时返回的顺序一致
//固定长度的元组
```
### 5.枚举类型(Enum Types)

枚举（Enum）类型用于取值被限定在一定范围内的场景，比如发布文章状态分为草稿、未发布、已发布。
```javascript
const article={
  title:'123',
  content:'typescript',
  status:0 //0 草稿 1 未发布 2已发布
}
```
如果我们直接用0、1、2这种方式表示状态的话，时间久了就有可能出现状态混淆、未知状态等问题。

在很多编程语言中都有枚举这种数据结构，但是在JavaScript中没有，我们一般使用对象模拟实现枚举
```javascript
const PostStatus1={
  Draft:0,
  Unpubulished:1,
  Published:2
}
```
在 Typescript中提供了enum关键字。使用enum的优势在于一个枚举类型只会存在几个固定的值，不会存在超出范围的可能性。
```javascript
enum PostStatus {
  Draft=0,
  Unpubulished=1,
  Published=2
  //这里是= 不是:
}
```
枚举类型的值可以不指定，默认是从0开始累加。如果指定了第一个值，后面所有的值都会在其基础上累加。

枚举类型的值可以是字符串，但是字符串无法像数字累加，就只能指定对应的默认值
```javascript
enum PostStatus {
  Draft='aa',
  Unpubulished='bb',
  Published='cc'
}
//PostStatus[0]=>Draft
```
tips:枚举类型会影响编译后的结果。在typescript中大多数类型在编译转换后会被移除，因为其目的是为了做类型检查，但是枚举类型不会，他会被编译为一个双向键值对对象
```javascript
var PostStatus1;
(function (PostStatus1) {
    PostStatus1[PostStatus1["Draft"] = 0] = "Draft";
    PostStatus1[PostStatus1["Unpubulished"] = 1] = "Unpubulished";
    PostStatus1[PostStatus1["Published"] = 2] = "Published";
})(PostStatus1 || (PostStatus1 = {}));
//编译后
```
当不使用索引器的方式访问枚举的时候可以使用常量枚举，常量枚举与普通枚举的区别是，它会在编译阶段被删除，并且不能包含计算成员。
```javascript
const enum PostStatus {
  Draft,
  Unpubulished,
  Published
}
//编译前
var PostStatus2;
(function (PostStatus2) {
    PostStatus2["Draft"] = "aa";
    PostStatus2["Unpubulished"] = "bb";
    PostStatus2["Published"] = "cc";
})(PostStatus2 || (PostStatus2 = {}));
//编译后
```
### 6.函数类型(Function Types)

一个函数有输入和输出，要在 TypeScript 中对其进行约束，需要把输入和输出都考虑到，其中函数声明的类型定义比较简单
```javascript
function sum(x: number, y: number): number {
    return x + y;
}

console.log(sum(1, 2))
```
输入多余的（或者少于要求的）参数，是不被允许的。如果需要定义可选参数，我们可以用?表示可选的参数。可选参数必须接在必需参数后面
```javascript
function sum1(x: number, y?: number): number {
  return x;
}
```
在ES6中，我们允许给函数的参数添加默认值，TypeScript 会将添加了默认值的参数识别为可选参数，此时就不受可选参数必须接在必需参数后面的限制了。
```javascript
function sum2(x: number=10, y: number): number {
    return x + y;
}

console.log(sum2(20,10))
```
如果需要接收任意数量的参数，可以使用 es6的 ...rest 的方式获取函数中的剩余参数（rest 参数）
```javascript
function sum3(x: number, y: number = 10, ...rest: number[]): number {
  let total = 0;
  for (var i of rest) {
    total += i;
  }
  return x + y + total;
}

console.log(sum3(20,10,1,2,3,4,5))
```
如果要我们现在写一个对函数表达式的定义，可能会写成这样：
```javascript
const mySum = function (x: number, y: number): number {
    return x + y;
};
```
这是可以通过编译的，不过事实上，上面的代码只对等号右侧的匿名函数进行了类型定义，而等号左边的 mySum，是通过赋值操作进行类型推论而推断出来的。如果需要我们手动给 mySum 添加类型，则应该是这样：
```javascript
const mySum: (x: number, y: number) => number = function (x: number, y: number): number {
    return x + y;
};
```
tips:在 TypeScript 的类型定义中，=> 用来表示函数的定义，左边是输入类型，需要用括号括起来，右边是输出类型。
### 7.任意类型(Any Types)

任意值（Any）用来表示允许赋值为任意类型
```javascript
function stringify(value:any){
  return JSON.stringify(value)
}
stringify('123')
stringify(123)
stringify(true)
```
可以认为，声明一个变量为任意值之后，对它的任何操作，返回的内容的类型都是任意值。
