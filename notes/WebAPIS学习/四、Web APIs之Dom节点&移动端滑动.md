# Dom节点&移动端滑动

[toc]



## 日期对象

1. 目的：掌握 Date 日期对象的使用，动态获取当前计算机的时间（可以让网页显示日期）。
2. ECMAScript 中内置了获取系统时间的对象 Date，使用 Date 时与之前学习的内置对象 console 和 Math 不同，它需要借助 new 关键字才能使用。
3. 日期对象：用来表示时间的对象
4. 作用：可以得到当前系统时间



### 实例化

目标：能够实例化日期对象

1. 在代码中发现了 `new` 关键字时，一般将这个操作称为`实例化`，实例化日期对象 new Date
2. 创建一个时间对象并获取时间

3. 语法：

* 获得当前时间

  ```javascript
  const date = new Date()  // 系统默认时间
  console.log(date)
  ```



* 获得指定时间

  ```javascript
  const date = new Date('2020-05-01 08:30:00')  // 指定时间
  // date 变量即所谓的时间对象
  console.log(date)
  ```





### 时间对象的方法

目标：能够使用日期对象中的方法写出常见日期

**使用场景：**因为日期对象返回的数据我们不能直接使用，所以需要转换为实际开发中`常用`的格式

​      ![image-20231204221556358](http://images.newstar.net.cn/sally-imgsimage-20231204221556358.png) 

\- 举例说明：

```javascript
<script>
    // 获得日期对象
    const date = new Date() // 实例化对象
    // 调用时间对象方法
    // 通过方法分别获取年、月、日，时、分、秒
    console.log(date.getFullYear()) // 四位年份
    console.log(date.getMonth() + 1)  // 月份是1-12，取值是0-11，所以要 + 1
    console.log(date.getDate())
    console.log(date.getDay())  // 返回的是星期几，取值0-6,0代表周日
    console.log(date.getHours())
    console.log(date.getMinutes())
    console.log(date.getSeconds())
  </script>
```



\- 显示格式化时间(修改成我们想要的时间)：

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    div {
      width: 300px;
      height: 40px;
      border: 1px solid pink;
      text-align: center;
      line-height: 40px;
    }
  </style>
</head>

<body>
  <div></div>
  <script>
    /* 
    需求：将当前时间以：YYYY-MM-DD HH:mm 形式显示在页面 2008-08-08 08:08
    分析：
    ①：调用日期对象方法进行转换
    ②：记得数字要补0
    ③：字符串拼接后，通过 innerText 给 标签
    */

    const div = document.querySelector('div')
    function getMyDate() {
      const date = new Date()

      // 数字补0
      let h = date.getHours()
      let m = date.getMinutes()
      let s = date.getSeconds()
      h = h < 10 ? '0' + h : h
      m = m < 10 ? '0' + m : m
      s = s < 10 ? '0' + s : s
      return `今天是：${date.getFullYear()}年${date.getMonth() + 1}月${date.getDate()}日 ${h}:${m}:${s}`
    }
    div.innerHTML = getMyDate()
    // 让时间变动 加定时器
    setInterval(function () {
      div.innerHTML = getMyDate()
    }, 1000)
  </script>
</body>

</html>
```





### 时间的另一种写法

* 方法：

```javascript
div.innerHTML = date.toLocaleString()
```

\- 举例说明：

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    div {
      width: 300px;
      height: 40px;
      border: 1px solid pink;
      text-align: center;
      line-height: 40px;
    }
  </style>
</head>

<body>
  <div></div>
  <script>
    const div = document.querySelector('div')
    // 得到日期对象
    const date = new Date()
    div.innerHTML = date.toLocaleString() // 2023/12/5 10:49:21
    setInterval(function () {
      const date = new Date()
      div.innerHTML = date.toLocaleString()  // 时间变动

    }, 1000)
    // div.innerHTML = date.toLocaleDateString()  // 获得年月日 2023/12/5
    // div.innerHTML = date.toLocaleTimeString()  // 获得时间 10:51:33
  </script>
</body>

</html>
```





### 时间戳

`时间戳是唯一的，ECMAScript中时间戳是以毫秒计的,经常用于倒计时`

1. **使用场景：** 如果计算倒计时效果，前面方法无法直接计算，需要借助于时间戳完成
2. **什么是时间戳:** `是`指1970年01月01日00时00分00秒起至现在的总秒数或`毫秒数`(因毫秒数小，计算更精确)，它是一种特殊的计量`时间的方式`。
3. **算法：**

* 将来的时间戳 - 现在的时间戳 = 剩余时间毫秒数

* 剩余时间毫秒数 转换为 剩余时间的 年月日时分秒 就是 倒计时时间
* 比如 将来时间戳 2000ms - 现在时间戳 1000ms = 1000ms
* 1000ms 转换为就是 0小时0分1秒



#### 获取时间戳的方法

##### getTime() 方法

* `必须实例化`

```javascript
const date = new Date() // 实例化
console.log(date.getTime())
```



##### (重点) 简写 +new Date() 

* `无需实例化`
* 可以返回`当前`时间戳或者`指定`的时间戳

```javascript
console.log(+new Date())
```

> **注：**new Date返回的是黑色字符串格式，同理：'1'是字符串，加一个正号 +'1',就是数字型1，所以new Date()要加+

```javascript
// 2. +new Date()
console.log(+new Date()) // 当前时间戳
console.log('-----------------');
console.log(+new Date('2023-12-5 18:30:00')) // 指定时间 比当前时间戳更大

// 3. 我要根据日期 Day()  0 ~ 6  返回的是 星期一
const arr = ['星期天', '星期一', '星期二', '星期三', '星期四', '星期五', '星期六']
// const date = new Date()
console.log(arr[new Date().getDay()])

// 等同于以下写法
// const date = new Date()
// console.log(date.getDay)
```



##### Date.now()

* 无需实例化
* `但是只能得到当前的时间戳， 而前面两种可以返回指定时间的时间戳`

```javascript
console.log(Date.now())
```





## 节点操作

> 掌握元素节点创建、复制、插入、删除等操作的方法，能够依据元素节点的结构关系查找节点

回顾之前 DOM 的操作都是针对元素节点的属性或文本的，除此之外也有专门针对元素节点本身的操作，如插入、复制、删除、替换等。





### DOM节点

目标：能说出DOM节点的类型

* DOM节点：DOM树里每一个内容都称之为节点

* 节点类型(分类)：

  1. `元素节点`

  * 所有的标签 比如 body、 div标签
  * html 是根节点

  2. 属性节点

  * 所有的属性 比如 href、 class属性

  3. 文本节点

  * 所有的文本 比如标签里面的文字

  4. 其他

![image-20231205134914057](http://images.newstar.net.cn/sally-imgsimage-20231205134914057.png) 





### 查找节点

DOM 树中的任意节点都不是孤立存在的，它们要么是父子关系，要么是兄弟关系，不仅如此，我们可以依据`节点之间的关系查找节点`。

* **节点关系：针对的找亲戚返回的都是对象**
  1. 父节点
  2. 子节点
  3. 兄弟节点



#### 父节点查找

`parentNode`获取父节点，以相对位置查找节点，实际应用中非常灵活

1. parentNode 属性

2. 返回最近一级的父节点 找不到返回为null

3. 写法：

```javascript
子元素.parentNode
```

\- 举例说明：

```javascript
<body>
  <div class="grandfather">
    <div class="father">
      <div class="baby">x</div>
    </div>
    <script>
      const baby = document.querySelector('.baby')
      console.log(baby) // 返回dom对象
      console.log(baby.parentNode) // 父节点也返回dom对象
      console.log(baby.parentNode.parentNode) // 父节点也返回dom对象
    </script>
</body>
```



#### 子节点查找

##### childNodes

1. 获得`所有子节点`、包括文本节点（空格、换行）、注释节点等
2. 回车换行会被认为是空白文本节点

```javascript
<body>
  <button class="btn1">所有的子节点</button>
  <!-- 获取 ul 的子节点 -->
  <ul>
    <li>HTML</li>
    <li>CSS</li>
    <li>JavaScript 基础</li>
    <li>Web APIs</li>
  </ul>
  <script>
    const btn1 = document.querySelector('.btn1')
    btn1.addEventListener('click', function () {
      // 父节点
      const ul = document.querySelector('ul')

      // 所有的子节点，回车换行会被认为是空白文本节点
      console.log(ul.childNodes)
    })
  </script>
</body>
```



##### children 属性 （重点）

1. 仅获得所有`元素节点`,也就是只包含元素子节点
2. 返回的还是一个伪数组（要想得到里面的每个孩子要遍历）
3. 写法：

```javascript
父元素.children
```

\- 举例说明：

```javascript
<body>
  <ul>
    <li>
      <p>第一个段落</p>
    </li>
    <li></li>
    <li></li>
    <li></li>
    <li></li>
  </ul>
  <script>
    const ul = document.querySelector('ul')  // ul
    console.log(ul.children)  // 得到伪数组  选择的是 亲儿子 
  </script>
</body>
```





#### 兄弟关系查找

1. 下一个兄弟节点：`nextElementSibling` 属性,获取前一个节点，以相对位置查找节点
2. 上一个兄弟节点：`previousElementSibling` 属性,获取后一个节点，以相对位置查找节点

```javascript
<body>
  <ul>
    <li>1</li>
    <li>2</li>
    <li>3</li>
    <li>4</li>
    <li>5</li>
  </ul>
  <script>
    const li2 = document.querySelector('ul li:nth-child(2)')
    console.log(li2.previousElementSibling)  // 上一个兄弟1
    console.log(li2.nextElementSibling)  // 下一个兄弟3
  </script>
</body>
```





### 增加节点(重点)

在已有的 DOM 节点中插入新的 DOM 节点时，需要关注两个关键因素：首先要得到新的 DOM 节点，其次在哪个位置插入这个节点。

1. 很多情况下，我们需要在页面中增加元素

* 比如，点击发布按钮，可以新增一条信息

2. 一般情况下，我们新增节点，按照如下操作：

* 创建一个新的节点
* 把创建的新的节点放入到指定的元素内部

3. 学习路线：

* `创建节点`
* 追加节点



#### 创建节点

1. 即创造出一个新的网页元素，再添加到网页内，一般**先创建节点**，然后插入节点
2. 创建元素节点方法：

```javascript
document.createElement('标签名')
```

\- 举例说明:

```javascript
<script>
// 1. 创建节点
const div = document.createElement('div')
console.log(div)
</script>
```

**结论：**`createElement`动态创建任意 DOM 节点



#### 追加节点

要想在界面看到，还得插入到某个父元素中



##### 插入到父元素的最后一个子元素

\- 在末尾（结束标签前）插入节点:

```javascript
父元素.appendChild(要插入的元素)
```

\- 举例说明：

```javascript
<body>
  <ul>
    <li>我是老大</li>
  </ul>
  <script>
    // // 1. 创建节点简洁版
    // const div = document.createElement('div')
    // // console.log(div)

    // // 2. 追加节点  作为最后一个子元素
    // 获取ul
    const ul = document.querySelector('ul')
    // 创建新节点，ul里放小li
    const li = document.createElement('li')
    li.innerHTML = '我是li' // 往li里面添加内容
    ul.appendChild(li) // 追加到li里面，在老大后面
  </script>
</body>
```



##### 插入到父元素中某个子元素的前面

\- 在父节点中任意子节点之前插入新节点:

```javascript
父元素.insertBefore(要插入的元素, 在哪个元素前面)
```

\- 举例说明：

```javascript
<body>
<ul>
<li>我是老大</li>
</ul>
<script>
// // 2. 追加节点  插入到父元素中某个子元素的前面
// 获取ul
const ul = document.querySelector('ul')
// 创建新节点，ul里放小li
const li = document.createElement('li')
li.innerHTML = '我是li' // 往li里面添加内容
// ul.children // ul的孩子，children得到的是数组，ul.children得到所有孩子，老大是孩子中的一个，也是最大的那个

// insertBefore(插入的元素, 放到哪个元素的前面)
ul.insertBefore(li, ul.children[0]) // ul.children[0]节点前插入，在老大前面
</script>
</body>
```



##### 克隆节点

* 特殊情况下，我们新增节点，按照如下操作：

  1. 复制一个原有的节点
  2. 把复制的节点放入到指定的元素内部

* 克隆一个已有的元素节点：

  ```javascript
  元素.cloneNode(布尔值)
  ```

* cloneNode会克隆出一个跟原标签一样的元素，括号内传入布尔值
  1. 若为true，则代表克隆时会包含后代节点一起克隆
  2. 若为false，则代表克隆时不包含后代节点
  3. 默认为false



\- 举例说明：

```javascript
<body>
  <ul>
    <li>1</li>
    <li>2</li>
    <li>3</li>
  </ul>
  <script>
    // 获取ul
    const ul = document.querySelector('ul')
    // 1. 克隆节点  元素.cloneNode(true)
    //const li1 = ul.children[0].cloneNode(true)
    // console.log(li1)
    // 2. 追加ul在后面 先获取ul
	ul.appendChild(ul.children[0].cloneNode(true))
    // ul.appendChild(li1)
  </script>
</body>
```

> **结论：**
>
> 1. `cloneNode` 复制现有的 DOM 节点，传入参数 true 会复制所有子节点
> 2. 深克隆cloneNode(true) 有什么克隆什么，克隆所有子节点
> 3. 浅克隆cloneNode() 只克隆标签





### 删除节点

删除现有的 DOM 节点，也需要关注两个因素：首先由父节点删除子节点，其次是要删除哪个子节点。

1. 若一个节点在页面中已不需要时，可以删除它

2. 在 JavaScript 原生DOM操作中，要删除元素必须通过`父元素删除`

3. **语法**

   ```javascript
   父元素.removeChild(要删除的元素) // 父删子
   ```

   结论：`removeChild` 删除节点时一定是由父子关系,如不存在父子关系则删除不成功



4. 删除节点和隐藏节点（display:none）

* 隐藏节点，看不见，但还是存在的
* 删除节点，则从html中删除节点，真删掉了，页面中不存在这个东西了



\- 举例说明：

```javascript
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    .box {
      display: none;
    }
  </style>
</head>

<body>
  <div class="box">123</div>
  <ul>
    <li>没用了</li>
  </ul>
  <script>
    const ul = document.querySelector('ul')
    // 删除节点  父元素.removeChild(子元素) 父删子
    ul.removeChild(ul.children[0]) //真删掉了，页面中不存在这个东西了
  </script>
</body>

</html>
```





## M端(移动端)事件（了解）

移动端也有自己独特的地方。比如`触屏事件 touch`（也称触摸事件），Android 和 IOS 都有。

1. `触屏事件 touch`（也称触摸事件），Android 和 IOS 都有。
2. touch 对象代表一个触摸点: 
   * 触摸点可能是一根手指，也可能是一根触摸笔。
   * 触屏事件可响应用户手指（或触控笔)对屏幕或者触控板操作
3. 常见的触屏事件如下：

![image-20231206141217054](http://images.newstar.net.cn/sally-imgsimage-20231206141217054.png) 







## JS插件-swiper插件的使用(重点)

移动端做轮播图很麻烦，日常开发中使用插件来做

* 插件: 就是别人写好的一些代码,我们只需要复制对应的代码,就可以直接实现对应的效果

* 学习插件的基本过程：
  1. [熟悉官网,了解这个插件可以完成什么需求](https://www.swiper.com.cn/)
  2. [看在线演示,找到符合自己需求的demo](https://www.swiper.com.cn/demo/index.html)
  3. [查看基本使用流程](https://www.swiper.com.cn/usage/index.html) 
  4. [查看APi文档,去配置自己的插件](https://www.swiper.com.cn/api/index.html)
  5. 注意: 多个swiper同时使用的时候, 类名需要注意区分
  6. 使用思路：
     * 官网下载swiper，解压到本地文件
     * JS和CSS文件放到项目文件下，并引用到页面中
     * 然后去挑选自己喜欢的demo风格，挑中了在新窗口打开复制粘贴(不能乱动别人写好的东西！)
     * 最后去定制也就是看播放说明，中文教程-Swiper使用方法-API文档
     * 自己写样式在less里







## 重绘和回流

* 浏览器是如何进行界面渲染的？

  1. 解析（Parser）HTML，生成DOM树(DOM Tree)

  2. 同时解析（Parser） CSS，生成样式规则 (Style Rules)

  3. 根据DOM树和样式规则，生成渲染树(Render Tree)

  4. 进行布局 Layout(回流/重排):根据生成的渲染树，得到节点的几何信息（位置，大小）

  5. 进行绘制 Painting(重绘): 根据计算和获取的信息进行整个页面的绘制

  6. Display: 展示在页面上

![image-20231207094327988](http://images.newstar.net.cn/sally-imgsimage-20231207094327988.png) 

  

* 会导致回流（重排）的操作：
  1. 页面的首次刷新
  2. 浏览器的窗口大小发生改变
  3. 元素的大小或位置发生改变
  4. 改变字体的大小
  5. 内容的变化（如：input框的输入，图片的大小）
  6. 激活css伪类 （如：:hover）
  7. 脚本操作DOM（添加或者删除可见的DOM元素）
  8. **简单理解影响到布局了，就会有回流**



* 思考下述代码的重绘重排过程：

![image-20231207094910703](http://images.newstar.net.cn/sally-imgsimage-20231207094910703.png) 







### 回流(重排)

* 当 Render Tree 中部分或者全部元素的尺寸、结构、布局等发生改变时，浏览器就会重新渲染部分或全部文档的过程称为 **回流**





### 重绘

* 由于节点(元素)的样式的改变并不影响它在文档流中的位置和文档布局时(比如：color、background-color、outline等), 称为重绘
* `重绘不一定引起回流，而回流一定会引起重绘。`