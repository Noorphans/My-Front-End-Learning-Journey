# Bom操作

[toc]



## Window对象

目标：学习 window 对象的常见属性，知道各个 BOM 对象的功能含义



### BOM(浏览器对象模型)

1. BOM(Browser Object Model )是浏览器对象模型

![1676047436362](http://images.newstar.net.cn/sally-imgs1676047436362.png)

2. window对象更大，是一个全局对象，也可以说是JavaScript中的顶级对象

   * 像document、alert()、console.log()这些都是window的属性，基本BOM的属性和方法都是window的
   * 所有通过var定义在全局作用域中的变量、函数都会变成window对象的属性和方法
   * window对象下的属性和方法调用的时候可以省略window

   ```javascript
   <script>
   // document.querySelector()
   
   // dom在Window里面，只不过Window已经是最大，所以document其实省略了window。就如中国上海人，省略中国
   // window.document.querySelector()
   console.log(document === window.document) // true
   
   // 声明的函数或全局变量默认挂在Window身上，调用时是 window.fn() 
   function fn() {
     console.log(11)
   }
   // 结果还是11
   window.fn()
   
   // 以前var全局声明的变量也挂在Window身上，const和let是挂在自己的作用域内
   var num = 10
   console.log(window.num)
   </script>
   ```

3. document是核心，所以叫Dom





## 定时器-延时函数

1. JavaScript 内置的一个用来让代码延迟执行的函数，叫 setTimeout

2. **语法：**

   ```javascript
   setTimeout(回调函数, 等待的毫秒数)
   ```

   \- 举例说明：

   ```javascript
   <script>
   setTimeout(function () {
     console.log('时间到了')
   }, 2000) // 延迟两秒钟执行一次
   </script>
   ```

   

3. setTimeout 仅仅只执行一次，所以可以理解为就是把一段代码延迟执行, 平时省略window

4. **清除延时函数**：

   ```javascript
   let timerId = setTimeout(回调函数, 等待的毫秒数)
   clearTimeout(timerId)
   ```

   > **注:**
   >
   > 1. 延时器需要等待,所以后面的代码先执行
   > 2. 每一次调用延时器都会产生一个新的延时器(`返回值是一个正整数，表示定时器的编号`)

   \- 举例说明：

   ```javascript
   <script>
   // 1. 开启延迟函数
   let timerId = setTimeout(function () {
     console.log('时间到了,我只执行一次')
   }, 2000)
   // 1.1 延迟函数返回的还是一个正整数数字，表示延迟函数的编号
   console.log(timerId)
   
   // 1.2 延迟函数需要等待时间，所以下面的代码优先执行
   
   // 2. 关闭延迟函数
   clearTimeout(timerId)
   </script>
   ```

   



5. **两种定时器对比：**执行的次数
   * 延时函数: 执行一次
   * 间歇函数:每隔一段时间就执行一次,除非手动清除





## JS执行机制(掌握)

谷歌浏览器内置了V8引擎，专门为了解析js

* JavaScript 语言的一大特点就是`单线程`，也就是说，`同一个时间只能做一件事。`
  1. 这是因为 Javascript 这门脚本语言诞生的使命所致——JavaScript 是为处理页面中用户的交互，以及操作DOM 而诞生的。比如我们对某个 DOM 元素进行添加和删除操作，不能同时进行。 应该先进行添加，之后再删除。
  2. 单线程就意味着，所有任务需要排队，前一个任务结束，才会执行后一个任务。这样所导致的问题是：如果 JS 执行的时间过长，这样就会造成页面的渲染不连贯，导致页面渲染加载阻塞的感觉
  3. 为了解决这个问题，利用多核 CPU 的计算能力，HTML5 提出 Web Worker 标准，**允许 JavaScript 脚本创建多个线程**。于是，JS 中出现了`同步`和`异步`。 



### 同步

前一个任务结束后再执行后一个任务，程序的执行顺序与任务的排列顺序是一致的、同步的。比如做饭的同步做法：我们要烧水煮饭，等水开了（10分钟之后），再去切菜，炒菜





### 异步

你在做一件事情时，因为这件事情会花费很长时间，在做这件事的同时，你还可以去处理其他事情。比如做饭的异步做法，我们在烧水的同时，利用这10分钟，去切菜，炒菜。



> **他们的本质区别：** `这条流水线上各个流程的执行顺序不同。 `



#### 同步任务

同步任务都在主线程上执行，形成一个`执行栈。`

![image-20231207161129464](http://images.newstar.net.cn/sally-imgsimage-20231207161129464.png) 



#### 异步任务

耗时的任务都是异步任务，因为他们不能同步执行而是放后面执行

* JS 的异步是通过回调函数实现的。

* 一般而言，异步任务有以下三种类型:
  1. 普通事件，如 click、resize 等
  2. 资源加载，如 load、error 等
  3. 定时器，包括 setInterval、setTimeout 等
* 异步任务相关添加到`任务队列`中（任务队列也称为消息队列）。

![image-20231207162152659](http://images.newstar.net.cn/sally-imgsimage-20231207162152659.png) 



#### 任务执行顺序 过程

1. 先执行`执行栈中的同步任务`。

2. 异步任务放入任务队列中.

3. 一旦执行栈中的所有同步任务执行完毕，系统就会按次序读取任务队列中的`异步任务`，于是被读取的异步任务结束等待

   状态，进入执行栈，开始执行。 

![image-20231207173211918](http://images.newstar.net.cn/sally-imgsimage-20231207173211918.png) 



\- 举例说明：

```javascript
<script>
console.log(1) // 同步任务
console.log(2) // 同步任务
setTimeout(function () {
  console.log(3) // 异步任务
}, 0)
console.log(4) // 同步任务
</script>
```



![image-20231207191506293](http://images.newstar.net.cn/sally-imgsimage-20231207191506293.png)

  

![image-20231207192253467](http://images.newstar.net.cn/sally-imgsimage-20231207192253467.png)

由于主线程不断的重复获得任务、执行任务、再获取任务、再执行，所以这种机制被称为`事件循环（event loop)。`



\- 举例说明：

```javascript
<script>
// console.log(1) // 同步任务
// console.log(2) // 同步任务
// setTimeout(function () {
//   console.log(3) // 异步任务
// }, 0)
// console.log(4) // 同步任务

console.log(1)
document.addEventListener('click', function () {
  console.log(4)
})
console.log(2)

setTimeout(function () {
  console.log(3)
}, 3000)
</script>
```

结论：放代码 抽代码 推代码 用代码，然后一直循环放抽推用这个过程。放代码到执行栈，先执行同步任务，异步任务由异步API抽离代码到任务队列，任务队列推代码到执行栈再用代码

![image-20231207203535010](http://images.newstar.net.cn/sally-imgsimage-20231207203535010.png)







## location对象

* location有很多方法：比如通过js形式跳转页面(很多情况下自动跳转页面，如注册成功了，5秒自动跳转到首页);也可实现下载功能

* location 的数据类型是对象，它拆分并保存了 URL 地址的各个组成部分




### 常用属性和方法

| 属性/方法 | 说明                                                 |
| --------- | ---------------------------------------------------- |
| href      | 属性，获取完整的 URL 地址，赋值时用于地址的跳转      |
| search    | 属性，获取地址中携带的参数，符号 ？后面部分          |
| hash      | 属性，获取地址中的啥希值，符号 # 后面部分            |
| reload()  | 方法，用来刷新当前页面，传入参数 true 时表示强制刷新 |



#### href属性(重点)

* 获取完整的 URL 地址，对其赋值时用于地址的跳转

```javascript
// 可以得到当前文件URL地址
console.log(location.href)
// href 经常用href做页面跳转，利用js的方法去跳转页面
location.href = 'http://www.baidu.com'
```



#### search属性

* 获取地址中携带的参数，符号 ？后面部分

```javascript
 console.log(location.search)
```

\- 举例说明：

```javascript
<body>
  <form>
    <input type="text" name="search"> <button>搜索</button>
  </form>
  <a href="#/music">音乐</a>
  <a href="#/download">下载</a>

  <button class="reload">刷新页面</button>
  <script>
    //  search属性  得到 ? 后面的地址 
    console.log(location.search)  // ?search=笔记本
  </script>
</body>
```



#### hash属性

> 后期vue路由的铺垫，经常用于不刷新页面，显示不同页面，比如 网易云音乐

* 获取地址中的哈希值，符号 # 后面部分

```javascript
 console.log(location.hash)
```

\- 举例说明：

```javascript
<body>
  <form>
    <input type="text" name="search"> <button>搜索</button>
  </form>
  <a href="#/music">音乐</a>
  <a href="#/download">下载</a>

  <button class="reload">刷新页面</button>
  <script>
    // hash属性  得到 # 后面的地址
    console.log(location.hash)
  </script>
</body>
```



#### reload方法

* 用来刷新当前页面，传入参数 true 时表示强制刷新`ctrl+f5`

```javascript
<body>
  <form>
    <input type="text" name="search"> <button>搜索</button>
  </form>
  <a href="#/music">音乐</a>
  <a href="#/download">下载</a>

  <button class="reload">刷新页面</button>
  <script>
    // reload 方法  刷新页面 
    const btn = document.querySelector('.reload')
    btn.addEventListener('click', function () {
      // location.reload() // F5 页面刷新
      location.reload(true) // 强制页面刷新 ctrl+f5
    })
  </script>
</body>
```







## navigator对象(了解)

navigator的数据类型是对象，该对象下记录了浏览器自身的相关信息，主要用来获取浏览器的信息

常用属性和方法：

- 通过 userAgent 检测浏览器的版本及平台

~~~javascript
// 检测 userAgent（浏览器信息）
(function () {
  const userAgent = navigator.userAgent
  // 验证是否为Android或iPhone
  const android = userAgent.match(/(Android);?[\s\/]+([\d.]+)?/)
  const iphone = userAgent.match(/(iPhone\sOS)\s([\d_]+)/)
  // 如果是Android或iPhone，则跳转至移动站点
  if (android || iphone) {
    location.href = 'http://m.itcast.cn'
  }})();
~~~

`不用背，PC端就PC端，移动端就移动端，在PC端想打开移动端就直接复制粘贴使用，地址改为所需地址`





## history对象

history的数据类型是对象，主要管理历史记录， 该对象与浏览器地址栏的操作相对应，如前进、后退、历史记录等

* **常用属性和方法：**

![image-20231207221053897](http://images.newstar.net.cn/sally-imgsimage-20231207221053897.png)

\- 举例说明：

```javascript
<button>后退</button>
<button>前进</button>
<script>
const back = document.querySelector('button:first-child')
const forward = back.nextElementSibling
back.addEventListener('click', function () {
  // 后退一步
  // history.back()
  history.go(-1)
})
forward.addEventListener('click', function () {
  // 前进一步
  // history.forward()
  history.go(1)
})
</script>
```



* history 对象一般在实际开发中比较少用，但是会在一些 OA 办公系统中见到
 ![1676047834796](http://images.newstar.net.cn/sally-imgs1676047834796.png) 







## 本地存储(重点)

* `本地存储`可以看作`是`一个小型的`仓库`或数据库，用来`存放数据`的，只不过这个数据库是放在浏览器里面的
  * 比如以前的变量也是一个小仓库，只不过变量放在内存里的，一刷新就没了
  * 但是不想丢失数据，就在浏览器里新建了一个小仓库，把数据存放进去，只要浏览器在数据就在





### 本地存储介绍

1. 数据存储在`(本地)用户浏览器`中，简单说是放在硬盘中
2. 设置、读取方便、甚至页面刷新不丢失数据
3. 容量较大，sessionStorage和localStorage 约 5M 左右
4. 页面刷新或者关闭不丢失数据，实现数据持久化
5. 常见的使用场景：如[ECMAScript 6](https://todomvc.com/examples/vanilla-es6/) 这个网址，todos输入内容后，页面刷新数据不丢失






### 本地存储分类

#### localStorage(重点)

1. 目标： 能够使用localStorage 把数据存储的浏览器中

2. **作用:** 数据可以长期保留在本地浏览器（用户的电脑）中，刷新页面和关闭页面，数据也不会丢失，除非手动删除

3. **特性：**

   * 以键值对的形式存储，并且存储的是字符串， 省略了window；
   * 可以多窗口（页面）共享（同一浏览器可以共享）

4. 语法：

   * **存储数据：**

   ```javascript
   localStorage.setItem('key', 'value') // key键 value值
   ```

   **注：**`除了数字，键值 要加引号`，值存储是会转换成字符串，因为本地存储`只能存储字符串数据类型`,不管放什么进去都是字符串。

   

   \- 举例说明：

   ```javascript
   <script>
   // 1. 要存储一个名字  'uname'， '张老师'
   // localStorage.setItem('键'，'值')
   localStorage.setItem('uname', '张老师')  // 打来浏览器检查Application查看
   </script>
   ```

   

   * **获取数据：**

   ```javascript
   localStorage.getItem('key')
   ```

   \- 举例说明：

   ```javascript
   <script>
    // 获取方式  所有键都加引号
    console.log(localStorage.getItem('uname'))
   </script>
   ```

   

   * **删除数据：**

   ```javascript
   localStorage.removeItem('key')
   ```

   \- 举例说明：

   ```javascript
   <script>
   // 手动 删除本地存储  只删除名字
   localStorage.removeItem('uname')
   </script>
   ```

   

   * 修改数据：

   ```javascript
   localStorage.setItem(key, value) 
   ```

   \- 举例说明：

   ```javascript
   <script>
   // 改  如果原来有这个键，则是改，如果么有这个键是增
   localStorage.setItem('uname', 'red老师')
   </script>
   ```

   > **注：** `修改`数据和`存储`数据`语法一样`，如果原来`有`这个键，则是`改`，`没有`这个键是`增`

   

   

5. **浏览器查看本地数据:** 

![image-20231208140551303](http://images.newstar.net.cn/sally-imgsimage-20231208140551303.png)





  

#### sessionStorage（了解）

* 特性：

  1. 生命周期为关闭浏览器窗口
  2. 在同一个窗口(页面)下数据可以共享
  3. 以键值对的形式存储使用
  4. 用法跟localStorage 基本相同，区别是，当页面浏览器被关闭时，存储在 sessionStorage 的`数据会被清除`

* 语法：

  * 存储数据：

  ```javascript
  sessionStorage.setItem(key,value)
  ```

  

  * 获取数据：

  ```javascript
  sessionStorage.getItem(key)
  ```

  

  * 删除数据:

  ```javascript
  sessionStorage.removeItem(key)
  ```

  





## localStorage存储复杂数据类型

1. **问题：**本地只能存储字符串,无法存储复杂数据类型.

\- 举例说明：

```javascript
<script>
const obj = {
  uname: '张老师',
  age: 18,
  gender: '女'
}
// 存储 复杂数据类型  无法直接使用
localStorage.setItem('obj', obj) // value是 [object object] 
// 取
console.log(localStorage.getItem('obj')) // 结果[object object] 

</script>
```

![image-20231208145049612](http://images.newstar.net.cn/sally-imgsimage-20231208145049612.png) 





### JSON.stringify(存之前)

1. **解决：**需要将复杂数据类型转换成 `JSON字符串`,在`存储`到本地

2. **语法：**`JSON.stringify(复杂数据类型)`

\- 举例说明：

```javascript
<script>
const obj = {
  uname: '张老师',
  age: 18,
  gender: '女'
}
// 1.复杂数据类型存储必须转换为 JSON字符串存储
localStorage.setItem('obj', JSON.stringify(obj)) // value是{"uname":"pink老师","age":18,"gender":"女"}
// JSON 对象的属性和值有引号，而是引号统一是双引号


// 2.取
// console.log(typeof localStorage.getItem('obj')) // 存的数据是字符串类型
</script>
```

![image-20231208150006499](http://images.newstar.net.cn/sally-imgsimage-20231208150006499.png) 

> **注：**JSON对象,首先是1个字符串,`属性和值`有引号，引号统一`双引号`







### JSON.parse(取出来)

1. **问题：**因为本地存储里面取出来的是字符串，不是对象，无法直接使用
2. **解决：**把`取出来的字符串转换为对象`
3. **语法：** `JSON.parse(JSON字符串)`

\- 举例说明：

```javascript
<script>
const obj = {
  uname: '张老师',
  age: 18,
  gender: '女'
}
// 把JSON字符串转换为 对象
console.log(JSON.parse(localStorage.getItem('obj')))

// 写法2：
// const str = localStorage.getItem('obj') // {"uname":"pink老师","age":18,"gender":"女"}
// console.log(JSON.parse(str))
</script>
```

> **结论：** 只要使用本地存储复杂数据类型，就分两步
>
> 1. 第一步：存之前 通过`JSON.stringify`转换成 `JSON字符串`
> 2. 第二步：取过来 通过 `JSON.parse`转换成对象





 

## 数组map和jion方法

### 数组中map方法 迭代数组

1. **使用场景：** map 可以遍历数组`处理数据`，并且`返回新的数组`

2. 语法：

```javascript
<body>
  <script>
  const arr = ['red', 'blue', 'pink']
  // 1. 数组 map方法 处理数据并且 返回一个数组
   const newArr = arr.map(function (ele, index) {
    // console.log(ele)  // ele 得到 数组元素 'red' 'blue' 'pink'
    // console.log(index) // index 得到 索引号 0 1 2
    return ele + '颜色'
	})
console.log(newArr)
</script>
</body>
```

3. `map也称为映射。`映射是个术语，指两个元素的集之间元素相互“对应”的关系。
4. `map重点在于有返回值，`forEach没有返回值（undefined）



> **注：** 不要通过map遍历数组,因为违背了设计map方法的初衷。设计的主要原则是 想要的到一个数组，返回一个数组就用map





### 数组中join方法

1. **作用：**join() 方法用于把数组中的所有元素`转换一个字符串`
2. **参数：**数组元素是通过**参数里面指定的分隔符进行分隔**的,若为`空字符串('')`则所有元素之间`都没有任何字符（分隔符）`
3. **语法：**

```javascript
<body>
  <script>
    const arr = ['red', 'blue', 'pink']
    // 2. 数组join方法  把数组转换为字符串
    // 小括号为空则逗号分割
    console.log(newArr.join())  // red颜色,blue颜色,pink颜色
    // 小括号是空字符串，则元素之间没有分隔符
    console.log(newArr.join(''))  //red颜色blue颜色pink颜色
    console.log(newArr.join('|'))  //red颜色|blue颜色|pink颜色
  </script>
</body>
```



