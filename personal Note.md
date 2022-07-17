# html面试

## what is javascript?

单线程-只有一个调用栈-同一时刻只能做一件事

调用栈（stack）：调用栈是一个数据结构，用于记录我们当前处于程序的哪个位置。

阻塞（blocking）：就是调用栈中执行很慢的东西

回调函数：是可以被其他函数调用的函数，是一个会在将来某个时间进入栈的回调。

浏览器API：setTimeout、ajax

setTimeout:浏览器API，如果设置为0，就是想要代码在栈底部运行，或者说是要让栈空了再执行。

eventloop:做的事情就是查看栈和任务列队，如果栈为空，就把任务列队的第一个放入栈，

重绘：页面会在16.6秒内重绘一次，保持也能能保持在60帧。

## script标签的属性



### async：解析HTML中的脚步进行异步下载，下载成功立即执行，有可能会阻断HTML的解析。

### defer: 完全不会阻碍HTML的解析，解析完成之后再按照顺序执行脚本。

## 从浏览器输入url到请求返回发生了什么

### 1.Url:Uniform Resource Locator，统一资源定位符，用于定位互联网上的资源，也称网址。

如有以下网址：

```
scheme: // host.domain:port / path / filename ? abc = 123 # 456789

scheme       - 定义因特网服务的类型。常见的协议有 http、https、ftp、file，
               其中最常见的类型是 http，而 https 则是进行加密的网络传输。
host         - 定义域主机（http 的默认主机是 www）
domain       - 定义因特网域名，比如 baidu.com
port         - 定义主机上的端口号（http 的默认端口号是 80）
path         - 定义服务器上的路径（如果省略，则文档必须位于网站的根目录中）。
filename     - 定义文档/资源的名称
query        - 即查询参数
fragment     - 即 # 后的hash值，一般用来定位到某个位置
```

### 2.DNS域名解析

浏览器并不能直接通过域名找到指定服务器，而是要通过IP地址进行访问。

#### IP地址：（IP address）是IP协议提供的同一格式的地址。

#### 域名解析：DNS提供通过域名查询IP，或从IP逆向查询域名的服务。DNS是一个网络服务器。

##### DNS域名解析分为递归查询和迭代查询两种方式，现在大多为迭代查询。

### DNS优化

#### -DNS缓存

​	DNS有多级缓存，由近到远分别是：浏览器缓存，系统缓存，路由器缓存，IPS服务器缓存，根域名服务器缓存，顶级域名服务器缓存，主域名服务器缓存。

#### -DNS负载均衡，本质上就是为同一个主机名配置多个IP地址，在多用户进行访问的时候，按照物理距离去进行分配，使各IP地址访问量分摊，实现负载均衡。CDN就是用了DNS负载均衡也称DNS重定向技术。

#### -Dns-prefetch：是一种预解析技术，当浏览网页时，浏览器会对本域名下的其他地址进行预解析缓存，这样当你在点击当前域名下的其他地址时，就不要进行DNS解析，从而省去用户等待时间。

### 3.TCP三次握手：

- #### 第一次：浏览器发起，确定发送能力；

- #### 第二次：服务器发起，确定接受能力；

- #### 第三次：浏览器发起，确定了浏览器对于返回数据的接受能力；

### 4.http请求

### 5.服务器处理请求并返回报文

### 6.浏览器渲染页面

![image.png](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/77972f24d69243bb93679f155f305095~tplv-k3u1fbpfcp-zoom-in-crop-mark:1434:0:0:0.awebp)

### 7.断开TCP链接

# CSS面试题

## 盒模型

css3中的盒模型都是有margin border padding content 组成的，但是对于盒模型的大小有两个标准

### 标准盒模型：盒模型的宽高只包括content

### 怪异盒模型（IE盒模型）：盒模型的宽高包括content+padding+border

## 重绘（repaint)和重排（reflow):

### 重绘：

可以理解为重新渲染dom树

### 重排：

无论通过何种方式改变了一个dom元素的大小，需要重新进行计算的时候就会触发重排。

### 如何减少重绘和重排：

- #### 最小化重绘和重排：

  集中进行样式改变，有统一样式的可以通过类名实现。

- #### 批量操作dom

  - 获取dom和信息时，存入一个变量防止多次获取。
  - 利用document.createDocumentFragment()来创造dom，处理好了放入应该存在的位置。

- #### 使用`absolute`或`float`是元素脱离文档流：

  - 这种操作方式比较适用于较大的图片或动画

- #### 借用GPU加速

  - 使用transform属性，比如translate会比定位更加高效，因为它不会触发重绘和重排，transform会是浏览器为元素重新建立一个图层，使动画在一个独立的层中渲染。

  

# js面试题

## 数据类型

### 1.数据类型

#### es6新增：

- BigInt：可以表示任意大小的数。（number有最大最小界限，+-(2^53+1))

- Symbol:代表独一无二的值，最大的用法是用来定义对象的唯一属性名。

### 2.数据类型的判断 

#### typeof

​	可以判断基本数据类型，引用数据类型的结果都得到Object。

```js
console.log(typeof undefined); // undefined
console.log(typeof 2); // number
console.log(typeof true); // boolean
console.log(typeof "str"); // string
console.log(typeof Symbol("foo")); // symbol
console.log(typeof 2172141653n); // bigint
console.log(typeof function () {}); // function
// 不能判别
console.log(typeof []); // object
console.log(typeof {}); // object
console.log(typeof null); // object

```

#### instanceof

​	能判断**对象**类型，不能判断基本数据类型，**其内部运行机制是判断在其原型链中能否找到该类型的原型**。

```js
class People {}
class Student extends People {}

const vortesnail = new Student();

console.log(vortesnail instanceof People); // true
console.log(vortesnail instanceof Student); // true

```

#### **Object.prototype.toString.call()**：

​	所有原始数据类型都是能判断的，还有 **Error 对象，Date 对象**等。

```
Object.prototype.toString.call(2); // "[object Number]"
Object.prototype.toString.call(""); // "[object String]"
Object.prototype.toString.call(true); // "[object Boolean]"
Object.prototype.toString.call(undefined); // "[object Undefined]"
Object.prototype.toString.call(null); // "[object Null]"
Object.prototype.toString.call(Math); // "[object Math]"
Object.prototype.toString.call({}); // "[object Object]"
Object.prototype.toString.call([]); // "[object Array]"
Object.prototype.toString.call(function () {}); // "[object Function]"
```



### 				3.手写深拷贝

### 4.0.1+0.2 !==0.3

## 原型和原型链

```js
function Foo() {}

let f1 = new Foo();
let f2 = new Foo();
```

<img src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/4a61ca07672a45d3aecf382100cc9719~tplv-k3u1fbpfcp-zoom-in-crop-mark:1434:0:0:0.awebp" alt="image.png siz" style="zoom:50%;" />

### 总结：

#### 原型：

- 每一个 JavaScript 对象（null 除外）在创建的时候就会与之关联另一个对象，这个对象就是我们所说的原型，每一个对象都会从原型"继承"属性，其实就是 `prototype` 对象。

#### 原型链：

- 由相互关联的原型组成的**链状结构**就是原型链。

## 作用域与作用链

### 作用域：

- 规定了如何查找变量，也就是确定当前执行代码对变量的访问权限。换句话说，作用域决定了代码区块中变量和其他资源的可见性。（全局作用域、函数作用域、块级作用域）

### 作用链：

- 从当前作用域开始一层层往上找某个变量，如果找到全局作用域还没找到，就放弃寻找 。这种层级关系就是作用域链。（由多个执行上下文的**变量对象**构成的链表就叫做作用域链）

## 执行上下文

## 闭包

​	在 JavaScript 中，每当创建一个函数，闭包就会在函数创建的同时被创建出来。可以在一个内层函数中访问到其外层函数的作用域。

也可以这样说：

​	闭包是指那些能够访问自由变量的函数。 自由变量是指在函数中使用的，但既不是**函数参数**也不是**函数的局部变量**的**变量**。 闭包 = 函数 + 函数能够访问的自由变量。

### 闭包的应用：

#### 函数作为参数被传入

```js
function print(fn) {
  const a = 200;
  fn();
}

const a = 100;
function fn() {
  console.log(a);
}

print(fn); // 100

```

####  函数作为返回值被返回

```js
function create() {
  const a = 100;

  return function () {
    console.log(a);
  };
}

const fn = create();
const a = 200;
fn(); // 100
```

##  call、apply、bind 实现

### call

- call() 方法在使用一个指定的 this 值和若干个指定的参数值的前提下调用某个函数或方法。

```
var obj = {
  value: "vortesnail",
};

function fn() {
  console.log(this.value);
}

fn.call(obj); // vortesnail


call()改变了 this 的指向，指向到 obj 。
 fn 函数执行了。
```

#### 手写完成call方法，myCall()

注意点：先增加一个fn 方法，调用结束再删除，在fn中使用this

```
Function.prototype.myCall = function (context) {
  // 判断调用对象
  if (typeof this !== "function") {
    throw new Error("Type error");
  }
  // 首先获取参数
  let args = [...arguments].slice(1);
  let result = null;
  // 判断 context 是否传入，如果没有传就设置为 window
  context = context || window;
  // 将被调用的方法设置为 context 的属性
  // this 即为我们要调用的方法
  context.fn = this;
  // 执行要被调用的方法
  result = context.fn(...args);
  // 删除手动增加的属性方法
  delete context.fn;
  // 将执行结果返回
  return result;
};
```

### apply

#### 手写完成apply方法，myApply()

```
Function.prototype.myApply = function (context) {
  if (typeof this !== "function") {
    throw new Error("Type error");
  }
  let result = null;
  context = context || window;
  // 与上面代码相比，我们使用 Symbol 来保证属性唯一
  // 也就是保证不会重写用户自己原来定义在 context 中的同名属性
  const fnSymbol = Symbol();
  context[fnSymbol] = this;
  // 执行要被调用的方法
  if (arguments[1]) {
    result = context[fnSymbol](...arguments[1]);
  } else {
    result = context[fnSymbol]();
  }
  delete context[fnSymbol];
  return result;
};
```



### bind

有以下特性：

- 1、指定 `this`
- 2、传入参数
- 3、返回一个函数
- 4、柯里化

```
Function.prototype.myBind = function (context) {
  // 判断调用对象是否为函数
  if (typeof this !== "function") {
    throw new Error("Type error");
  }
  // 获取参数
  const args = [...arguments].slice(1),
  const fn = this;
  return function Fn() {
    return fn.apply(
      this instanceof Fn ? this : context,
      // 当前的这个 arguments 是指 Fn 的参数
      args.concat(...arguments)
    );
  };
};

```



## new实现

1. 首先创一个新的空对象。
2. 根据原型链，设置空对象的 `__proto__` 为构造函数的 `prototype` 。
3. 构造函数的 this 指向这个对象，执行构造函数的代码（为这个新对象添加属性）。
4. 判断函数的返回值类型，如果是引用类型，就返回这个引用类型的对象。

```
function myNew(context) {
  const obj = new Object();
  obj.__proto__ = context.prototype;
  const res = context.apply(obj, [...arguments].slice(1));
  return typeof res === "object" ? res : obj;
}

```



## 异步 

### eventloop、宏任务和微任务

#### eventloop

![屏幕录制 2021-07-19 15.01.09.gif](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/1e15fc609aa84eac973c5b8ff163c11c~tplv-k3u1fbpfcp-zoom-in-crop-mark:1434:0:0:0.awebp)

**注意：1.Call Stack 调用栈空闲 -> 2.尝试 DOM 渲染 -> 触发 Event loop**。

- 每次 Call Stack 清空（即每次轮询结束），即同步任务执行完。
- 都是 DOM 重新渲染的机会，DOM 结构有改变则重新渲染。
- 然后再去触发下一次 Event loop。

#### 宏任务和微任务：

宏任务：DOM 渲染后触发，如 `setTimeout` 、`setInterval` 、`DOM 事件` 、`script` 。

微任务：DOM 渲染前触发，如 `Promise.then` 、`MutationObserver` 、Node 环境下的 `process.nextTick` 。

- 微任务是 ES6 语法规定的（被压入 micro task queue）。
- 宏任务是由浏览器规定的（通过 Web APIs 压入 Callback queue）。
- 宏任务执行时间一般比较长。
- 每一次宏任务开始之前一定是伴随着一次 event loop 结束的，而微任务是在一次 event loop 结束前执行的。

### Promise





async&await





## 浏览器的垃圾回收机制

### **标记清除**：

标记阶段即为所有活动对象做上标记，清除阶段则把没有标记（也就是非活动对象）销毁

### **引用计数：**





### 
