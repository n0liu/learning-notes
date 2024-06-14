## 一、泛型是什么
用来处理不同类型的对象而并非单一类型的对象。它具有下列特性

1. 复用性
2. 支持未来数据类型
3. 泛型就是对类型进行编程

复用性
```typescript
function id(arg: boolean): boolean {
  return arg;
}
function id(arg: number): number {
  return arg;
}
function id(arg: string): string {
  return arg;
}
```
如果想输入什么，输出就是什么，在不使用泛型的情况下只能只用any
```typescript
function identity(arg: any): any {
    return arg;
}
```
但是如果我们使用any类型，在我们调用这个方法获得返回值后我们就失去了这个输出结果的数据类型。我们如果输入一个数字(number)，那么能得到的就只有any类型。失去了类型保护和语法提示
因此，我们需要使用类型捕捉的方式来进行类型的获取。这样我们在获取返回值时也可以获取到返回值的类型。在这里，我们使用一种叫做_类型变量_(type variable)的特殊变量。这种变量专门处理变量的类型而不是变量的值。
使用泛型对上面的代码进行重构
T 是一个抽象类型，只有在调用的时候才确定它的值
```typescript
function id<T>(arg: T): T {
  return arg;
}
```
为了便于大家更好地理解上述的内容，我们来举个例子，在这个例子中，我们将一步步揭示泛型的作用。
首先定义一个类：
```typescript
class People {
  name!: string;
  age!: number;
  constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }
}

```
再定义一个工厂函数：
```typescript
function create(Constructor: { new (...args: any): any }) {
  return new Constructor();
}

```
此时我们在调用工厂函数返回值得时候，其实已经失去了约束和提示，因为我们的参数设定的是any,返回值类型也是any
```typescript
// function create(Constructor: new (...args: any) => any): any
create(People).wsy;

```
加入泛型,此时就能提示出类上有的属性
```typescript
function create<T>(Constructor: { new (...args: any): T }) {
  return new Constructor();
}
create(People); 
```
对于刚接触 TypeScript 泛型的读者来说，首次看到 <T> 语法会感到陌生。但这没什么可担心的，就像传递参数一样，我们传递了我们想要用于特定函数调用的类型。
其中 T 代表 **Type**，在定义泛型时通常用作第一个类型变量名称。但实际上 T 可以用任何有效名称代替。除了 T 之外，以下是常见泛型变量代表的意思：

- K（Key）：表示对象中的键类型；
- V（Value）：表示对象中的值类型；
- E（Element）：表示元素类型。
```typescript
function identity <T, U>(value: T, message: U) : T {
  console.log(message);
  return value;
}

console.log(identity<Number, string>(68, "Semlinker"));

```
![](https://cdn.nlark.com/yuque/0/2022/webp/973111/1649532607723-8bd4b570-4afe-43ae-81a8-f21015c83f53.webp#clientId=u5c2d4c07-bff2-4&from=paste&id=JllbW&originHeight=564&originWidth=1178&originalType=url&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=u13342680-2026-4aaa-98bf-2189ba7b719&title=)
对于上述代码，编译器足够聪明，能够知道我们的参数类型，并将它们赋值给 T 和 U，而不需要开发人员显式指定它们。下面我们来看张动图，直观地感受一下类型传递的过程：
![](https://cdn.nlark.com/yuque/0/2022/webp/973111/1649524242475-9e5c763b-c8af-4669-abfc-554da52b8132.webp#clientId=u5c2d4c07-bff2-4&from=paste&id=GXssu&originHeight=480&originWidth=780&originalType=url&ratio=1&rotation=0&showTitle=false&status=done&style=none&taskId=ub0643196-e0db-4504-9055-02f4173c60e&title=)
## 二、泛型接口
为了解决上面提到的问题，首先让我们创建一个用于的 identity 函数通用 Identities 接口：
```typescript
interface Identities<V, M> {
  value: V,
  message: M
}

```
在上述的 Identities 接口中，我们引入了类型变量 V 和 M，来进一步说明有效的字母都可以用于表示类型变量，之后我们就可以将 Identities 接口作为 identity 函数的返回类型：
```typescript
function identity<T, U> (value: T, message: U): Identities<T, U> {
  console.log(value + ": " + typeof (value));
  console.log(message + ": " + typeof (message));
  let identities: Identities<T, U> = {
    value,
    message
  };
  return identities;
}

console.log(identity(68, "Semlinker"));

```
以上代码成功运行后，在控制台会输出以下结果：
```typescript
{ value: 68, message: 'Semlinker' }
```
## 三、泛型类
在类中使用泛型也很简单，我们只需要在类名后面，使用 <T, ...> 的语法定义任意多个类型变量，具体示例如下：
```typescript
interface GenericInterface<U> {
  value: U
  getIdentity: () => U
}

class IdentityClass<T> implements GenericInterface<T> {
  value: T

  constructor(value: T) {
    this.value = value
  }

  getIdentity(): T {
    return this.value
  }

}

const myNumberClass = new IdentityClass<Number>(68);
console.log(myNumberClass.getIdentity()); // 68

const myStringClass = new IdentityClass<string>("Semlinker!");
console.log(myStringClass.getIdentity()); // Semlinker!

```
我们在什么时候需要使用泛型呢？通常在决定是否使用泛型时，我们有以下两个参考标准：

- 当你的函数、接口或类将处理多种数据类型时；
- 当函数、接口或类在多个地方使用该数据类型时。

很有可能你没有办法保证在项目早期就使用泛型的组件，但是随着项目的发展，组件的功能通常会被扩展。这种增加的可扩展性最终很可能会满足上述两个条件，在这种情况下，引入泛型将比复制组件来满足一系列数据类型更干净。
我们将在本文的后面探讨更多满足这两个条件的用例。不过在这样做之前，让我们先介绍一下 Typescript 泛型提供的其他功能。
## 四、泛型约束
有时我们可能希望限制每个类型变量接受的类型数量，这就是泛型约束的作用。下面我们来举几个例子，介绍一下如何使用泛型约束。
### 4.1 确保属性存在
```typescript

 function identity<T extends { length: number }>(arg: T): T {
   console.log(arg.length); // 可以获取length属性
   return arg;
 }
```
T extends { length: number } 用于告诉编译器，我们支持已经实现 Length 接口的任何类型。之后，当我们使用不含有 length 属性的对象作为参数调用 identity 函数时，TypeScript 会提示相关的错误信息：
```typescript
identity(1)
// Argument of type 'number' is not assignable to parameter of type '{ length: number; }'
```
### 4.2 约束类型
```typescript
function sortChinese<T>(arr: Array<T>): T[] {
  return arr.sort((a, b) => {
    return a.localeCompare(b, 'zh-CN');
  });
}
//  Property 'localeCompare' does not exist on type 'T'

```
此时会提示类型“T”上不存在属性“localeCompare”
用extends约束T的类型
```typescript
function sortChinese<T extends string>(arr: Array<T>): T[] {
  return arr.sort((a, b) => {
    return a.localeCompare(b, 'zh-CN');
  });
}
```
### 4.3 检查对象上的键是否存在
泛型约束的另一个常见的使用场景就是检查对象上的键是否存在。不过在看具体示例之前，我们得来了解一下 keyof 操作符，
```typescript
interface Person {
  name: string;
  age: number;
  location: string;
}

type K1 = keyof Person; // "name" | "age" | "location"
type K2 = keyof Person[];  // number | "length" | "push" | "concat" | ...
type K3 = keyof { [x: string]: Person };  // string | number

```
通过 keyof 操作符，我们就可以获取指定类型的所有键，之后我们就可以结合前面介绍的 extends 约束，即限制输入的属性名包含在 keyof 返回的联合类型中。具体的使用方式如下：
```typescript
function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}
```
在以上的 getProperty 函数中，我们通过 K extends keyof T 确保参数 key 一定是对象中含有的键，这样就不会发生运行时错误。这是一个类型安全的解决方案，与简单调用 let value = obj[key]; 不同。
```typescript
const a = {
  name: 'Semlinker',
  age: 18,
  height: 18,
};

function getProperty<T, K extends keyof T>(obj: T, key: K): T[K] {
  return obj[key];
}
console.log(getProperty(a, 'name'));
```
可能会有疑问的是，如果按照下列的写法去写也能够约束key是T的属性
```typescript
function getProperty<T>(obj: T, key: keyof T) {
  return obj[key];
}
const a1 = getProperty(a, 'name');
console.log(a1); 
```
若使用 keyof T 作为 key 的类型，那 obj[key] 就是 T[keyof T] 类型——这无疑不够精确
```typescript
const a1: string | number
```
结论就是不够精准，**泛型约束是必须的，是为了让 obj[key] 成为类型正确的表达式**。
## 五、泛型参数默认类型
未指定默认值
```typescript
function sortChinese<T>(arr: Array<T>): T[] {
  return arr.sort((a, b) => {
    return a.localeCompare(b, 'zh-CN');
  });
}

sortChinese(1);

// 类型“number”的参数不能赋给类型“unknown[]”的参数。
```
指定了默认值
```typescript
function sortChinese<T = string>(arr: Array<T>): T[] {
  return arr.sort((a, b) => {
    return a.localeCompare(b, 'zh-CN');
  });
}

sortChinese(['1']);
// function sortChinese<string>(arr: string[]): string[]
```
如果添加了约束
```typescript
function sortChinese<T extends string = string>(arr: Array<T>): T[] {
  return arr.sort((a, b) => {
    return a.localeCompare(b, 'zh-CN');
  });
}

sortChinese(['1', 's']);
// function sortChinese<"1" | "s">(arr: ("1" | "s")[]): ("1" | "s")[]
```
## 六、类型工具前置条件
#### keyof 索引查询
对应任何类型T,keyof T的结果为该类型上所有公有属性key的联合：
```typescript
interface Eg1 {
  name: string,
  readonly age: number,
}
// T1的类型实则是name | age
type T1 = keyof Eg1

class Eg2 {
  private name: string;
  public readonly age: number;
  protected home: string;
}
// T2实则被约束为 age
// 而name和home不是公有属性，所以不能被keyof获取到
type T2 = keyof Eg2

```
#### T[K] 索引访问
```typescript
interface Eg1 {
  name: string,
  readonly age: number,
}
// string
type V1 = Eg1['name']
// string | number
type V2 = Eg1['name' | 'age']
// any
type V2 = Eg1['name' | 'age2222']
// string | number
type V3 = Eg1[keyof Eg1]

```
T[keyof T]的方式，可以获取到T所有key的类型组成的联合类型； T[keyof K]的方式，获取到的是T中的key且同时存在于K时的类型组成的联合类型； 注意：如果[]中的key有不存在T中的，则是any；因为ts也不知道该key最终是什么类型，所以是any；且也会报错；
#### extends关键词特性
##### 用于接口，表示继承
```typescript
interface T1 {
  name: string,
}

interface T2 {
  sex: number,
}

/**
 * @example
 * T3 = {name: string, sex: number, age: number}
 */
interface T3 extends T1, T2 {
  age: number,
}

```
注意，接口支持多重继承，语法为逗号隔开。如果是type实现继承，则可以使用交叉类型type A = B & C & D。
##### 表示条件类型，可用于条件判断
```typescript
/**
 * @example
 * type A1 = 1
 */
type A1 = 'x' extends 'x' ? 1 : 2;

/**
 * @example
 * type A2 = 2
 */
type A2 = 'x' | 'y' extends 'x' ? 1 : 2;

/**
 * @example
 * type A3 = 1 | 2
 */
type P<T> = T extends 'x' ? 1 : 2;
type A3 = P<'x' | 'y'>

```
为什么A2和A3的值不一样？

- 如果用于简单的条件判断，则是直接判断前面的类型是否可分配给后面的类型
- 若extends前面的类型是泛型，且泛型传入的是联合类型时，则会依次判断该联合类型的所有子类型是否可分配给extends后面的类型（是一个分发的过程）。

总结，就是extends前面的参数为联合类型时则会分解（依次遍历所有的子类型进行条件判断）联合类型进行判断。然后将最终的结果组成新的联合类型。
阻止extends关键词对于联合类型的分发特性
```typescript
type P<T> = [T] extends ['x'] ? 1 : 2;
/**
 * type A4 = 2;
 */
type A4 = P<'x' | 'y'>

```
#### 类型兼容性
集合论中，如果一个集合A的所有元素在集合B中都存在，则A是B的子集；
类型系统中，如果一个类型的属性更具体，则该类型是子类型。（因为属性更少则说明该类型约束的更宽泛，是父类型）
**因此，我们可以得出基本的结论：子类型比父类型更加具体,父类型比子类型更宽泛。**
##### 可赋值性
```typescript
interface Animal {
  name: string;
}

interface Dog extends Animal {
  break(): void;
}

let a: Animal;
let b: Dog;

// 可以赋值，子类型更佳具体，可以赋值给更佳宽泛的父类型
a = b;
// 反过来不行
b = a;

```
从这个例子里可以看出，animal 是一个「更宽泛」的类型，它的属性比较少，所以更「具体」的子类型是可以赋值给它的，因为你是知道 animal 上只有 age 这个属性的，你只会去使用这个属性，dog 上拥有 animal 所拥有的一切类型，赋值给 animal 是不会出现类型安全问题的。
反之，如果 dog = animal，那么后续使用者会期望 dog 上拥有 bark 属性，当他调用了 dog.bark() 就会引发运行时的崩溃。
从可赋值性角度来说，子类型是可以赋值给父类型的，也就是 父类型变量 = 子类型变量 是安全的，因为子类型上涵盖了父类型所拥有的的一切属性。
##### 联合类型
```typescript
type A = 1 | 2 | 3;
type B = 2 | 3;
let a: A;
let b: B;

// 不可赋值
b = a;
// 可以赋值
a = b;

```
是不是A的类型更多，A就是子类型呢？恰恰相反，A此处类型更多但是其表达的类型更宽泛，所以A是父类型，B是子类型。
因此b = a不成立（父类型不能赋值给子类型），而a = b成立（子类型可以赋值给父类型）。
##### 函数类型
函数类型的兼容性判断，要查看 x 是否能赋值给 y，首先看它们的参数列表。
x 的每个参数必须能在 y 里找到对应类型的参数,注意的是参数的名字相同与否无所谓，只看它们的类型。
这里，x 的每个参数在 y 中都能找到对应的参数类型，所以允许赋值:
其实也就是说 y 更加宽泛，y是父类,x是子类?
```typescript
let x = (a: number) => 0;
let y = (b: number, s: string) => 0;

y = x; // OK
x = y; // Error 不能将类型“(b: number, s: string) => number”分配给类型“(a: number) => number”。
```
##### 类的类型兼容性
仅仅只有实例成员和方法会相比较，构造函数和静态成员不会被检查:
```typescript
class Animal {
  feet: number;
  constructor(name: string, numFeet: number) {}
}

class Size {
  feet: number;
  constructor(meters: number) {}
}

let a: Animal;
let s: Size;

a = s; // OK
s = a; // OK
```
##### 泛型的类型兼容性
泛型本身就是不确定的类型,它的表现根据是否被成员使用而不同.
由于没有被成员使用泛型,所以这里是没问题的。
```typescript
interface Person<T> {

}

let x : Person<string>
let y : Person<number>

x = y // ok
y = x // ok
```
这里由于泛型 T 被成员 name 使用了,所以类型不再兼容。
```typescript
interface Person<T> {
    name: T
}

let x : Person<string>
let y : Person<number>

x = y // 不能将类型“Person<number>”分配给类型“Person<string>”。
y = x // 不能将类型“Person<string>”分配给类型“Person<number>”。

```
##### 协变
> 协变与逆变(Covariance and contravariance )是在计算机科学中，描述具有父/子型别关系的多个型别通过型别构造器、构造出的多个复杂型别之间是否有父/子型别关系的用语。

简单说就是，具有父子关系的多个类型，在通过某种构造关系构造成的新的类型，如果还具有父子关系则是协变的，而关系逆转了（子变父，父变子）就是逆变的。可能听起来有些抽象，下面我们将用更具体的例子进行演示说明：
```typescript
interface Animal {
  name: string;
}

interface Dog extends Animal {
  break(): void;
}

let Eg1: Animal;
let Eg2: Dog;
// 兼容，可以赋值
Eg1 = Eg2;

let Eg3: Array<Animal>
let Eg4: Array<Dog>
// 兼容，可以赋值
Eg3 = Eg4

```
通过Eg3和Eg4来看，在Animal和Dog在变成数组后，Array<Dog>依旧可以赋值给Array<Animal>，因此对于type MakeArray = Array<any>来说就是协变的。
##### 逆变
```typescript
interface Animal {
  name: string;
}

interface Dog extends Animal {
  break(): void;
}

type AnimalFn = (arg: Animal) => void
type DogFn = (arg: Dog) => void

let Eg1: AnimalFn;
let Eg2: DogFn;
// 不再可以赋值了，
// AnimalFn = DogFn不可以赋值了, Animal = Dog是可以的
Eg1 = Eg2;
// 反过来可以
Eg2 = Eg1;

```
理论上，Animal = Dog是类型安全的，那么AnimalFn = DogFn也应该类型安全才对，为什么Ts认为不安全呢？看下面的例子：
```typescript
let animal: AnimalFn = (arg: Animal) => {}
let dog: DogFn = (arg: Dog) => {
  arg.break();
}

// 假设类型安全可以赋值
animal = dog;
// 那么animal在调用时约束的参数，缺少dog所需的参数，此时会导致错误
animal({name: 'cat'});

```
从这个例子看到，如果dog函数赋值给animal函数，那么animal函数在调用时，约束的是参数必须要为Animal类型（而不是Dog），但是animal实际为dog的调用，此时就会出现错误。
因此，Animal和Dog在进行type Fn<T> = (arg: T) => void构造器构造后，父子关系逆转了，此时成为“逆变”。
##### 双向协变
Ts在函数参数的比较中实际上默认采取的策略是双向协变：只有当源函数参数能够赋值给目标函数或者反过来时才能赋值成功。
这是不稳定的，因为调用者可能传入了一个具有更精确类型信息的函数，但是调用这个传入的函数的时候却使用了不是那么精确的类型信息（典型的就是上述的逆变）。 但是实际上，这极少会发生错误，并且能够实现很多JavaScript里的常见模式：
```typescript
// lib.dom.d.ts中EventListener的接口定义
interface EventListener {
  (evt: Event): void;
}
// 简化后的Event
interface Event {
  readonly target: EventTarget | null;
  preventDefault(): void;
}
// 简化合并后的MouseEvent
interface MouseEvent extends Event {
  readonly x: number;
  readonly y: number;
}

// 简化后的Window接口
interface Window {
  // 简化后的addEventListener
  addEventListener(type: string, listener: EventListener)
}

// 日常使用
window.addEventListener('click', (e: Event) => {});
window.addEventListener('mouseover', (e: MouseEvent) => {});

```
#### infer
主要是用于extends的条件类型中让Ts自己推到类型
##### infer推导的名称相同并且都处于逆变的位置，则推导的结果将会是交叉类型。
```typescript
type Bar<T> = T extends {
  a: (x: infer U) => void;
  b: (x: infer U) => void;
} ? U : never;

// type T1 = string
type T1 = Bar<{ a: (x: string) => void; b: (x: string) => void }>;

// type T2 = never
type T2 = Bar<{ a: (x: string) => void; b: (x: number) => void }>;

```
##### infer推导的名称相同并且都处于协变的位置，则推导的结果将会是联合类型。
```typescript
type Foo<T> = T extends {
  a: infer U;
  b: infer U;
} ? U : never;

// type T1 = string
type T1 = Foo<{ a: string; b: string }>;

// type T2 = string | number
type T2 = Foo<{ a: string; b: number }>;

```
