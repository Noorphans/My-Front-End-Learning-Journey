# WebAPIs之DOM和BOM

## 声明变量优先const

* 常量也是变量，只不过使用**const**声明被称为“常量”

* 当**某个变量**永远 **不会改变**的时候，就可以用**const声明**，而不是let

* const语义化更好

* 实际开发中，如React框架，基本用const

* 使用规范和变量一样

  * 常量使用：

    ```javascript
    //声明一个常量
    const G = 9.8
    //输出这个常量
    console.log(G)
    ```

    > **注：**
    >
    > 1. const声明的值不能更改(**不允许重新赋值**)，**声明时就必须赋值（初始化**），即不需要重新赋值的数据用const
    > 2. **有了变量先const，发现后面是要被修改的，再改为let**
    > 3. 对于**引用数据类型，const声明的变量，栈里存的是地址**



* 以下能把let改为const吗？

  ```javascript
  let num1 = +prompt('请输入第一个值')
  let num2 = +prompt('请输入第二个值')
  alert(`两者和为${num1} + ${num2}`) //值未做改变 可以改为const
  ```

  

  ```javascript
  let num = 1
  num = num + 1
  //  num += 1
  console.log(num) //变量进行重新赋值，值发生改变 不能const
  ```

  

  ```javascript
  // let arr = ['blue', 'black']
  // arr.push('white')
  // console.log(arr)
  // 地址值未改变，可以const
  let person = {
    uname: 'sally',
    age: 18,
    sex: '女'
  }
  person.height = 159
  console.log(person)
  ```

  > **注：**
  >
  > 1. (5个)**基本数据类型**: 值发生改变 就用let**不能const**
  > 2. 复杂数据类型(Array、object)：地址值未改变(只是添加数组元素)可以用const
  > 3. **数组和对象尽量const声明**



* 什么时候用let声明变量？
  * 基本数据类型的值或引用数据类型的地址发生改变
  * 一个变量进行加减运算
  * for循环中的i++





## WebAPI基本认知

* **WebAPI是**一套 **操作**网页内容(**DOM**)与浏览器窗口(BOM)**的对象**

### 作用和分类

* 作用：使用JS去操作html和浏览器

* 分类：DOM(文档对象模型)、BOM(浏览器对象模型)

  

### 什么是DOM

* Document object model**文档对象模型**是用来呈现以及与任意HTML或XML文档交互的API 即**操作网页内容**的功能，如页面元素的移动、大小等
* DOM作用：
  * 开发网页内容特效和实现用户交互



### DOM树(文档树)

* DOM树是什么？
  * 将HTML文档以树状结构直观表现出来，称为文档数或DOM树
  * 作用：**文档树直观地体现了标签与标签之间的关系**

* 描述网页内容关系的名词

![image-20230923154110361](http://images.newstar.net.cn/sally-imgs/image-20230923154110361.png)





### DOM对象（非常重要）

* DOM对象怎么创建的？
  * 浏览器根据html标签生成的**JS对象**即DOM对象
  * DOM核心思想：把网页内容当做**对象**来处理

* 在**html里是标签**，在**JS的DOM里**获取过来的**叫DOM对象**
* **任何一个标签都是一个对象**，只要是对象就有属性和方法
  * 所有标签属性都可以在这个对象上面找到
  * 修改这个对象属性会自动映射到标签身上

* **document最大对象**

  ![image-20230923195446590](http://images.newstar.net.cn/sally-imgs/image-20230923195446590.png)

  * 它是DOM里提供的一个**对象**

  * 它提供的属性和方法都是**用来访问和操作网页内容的**

    * 如：document.write()

  * 网页所有内容都在document里面

    

## 获取DOM对象

* 如何查找/获取DOM对象

* 我们想要操作某个标签首先做什么？

  * 选中该标签，跟css选择器类似，选中标签才能操作

* **查找(获取)元素DOM元素即 利用JS选择页面中标签元素**

  

### 根据css选择器来获取DOM元素(重点)

1. 选择匹配的第一个元素（获取一个DOM元素）

   * 能直接操作修改

   * 语法：

     ```javascript
     document.querySelector('css选择器')
     ```

     ```html
     <!DOCTYPE html>
     <html lang="en">
     <head>
       <meta charset="UTF-8" />
       <meta name="viewport" content="width=device-width, initial-scale=1.0" />
       <title>Document</title>
       <style>
         .box {
           width: 300px;
           height: 300px;
         }
       </style>
     </head>
     <body>
       <!-- 以前的写法 css通过.box获取 -->
       <div class="box">123</div>
       <div class="box">abc</div>
       <p id="nav">导航栏</p>
       <ul>
         <li>测试1</li>
         <li>测试2</li>
         <li>测试3</li>
       </ul>
       <!-- id快速生成：标签#标签名 p#nav-->
       <script>
         // 写法1：获取匹配的第一个元素
         // const box = document.querySelector('div')
         // console.log(box)
           
         // 写法2：类名写法 .类名 .box
         // const box = document.querySelector('.box')
         // console.log(box)
           
          const nav = document.querySelector('#nav')
         // 可以直接修改，nav对象，style属性，对象名.属性名
           nav.style.color = 'red'
         // console.log(nav)
     
         // 获取第一个小li
         // const li = document.querySelector('ul li:first-child')  // <li>测试1</li>
         // li:first-child 获取li的第一个元素
       </script>
     </body>
     </html>
     
     ```

     

     > **注：** 
     >
     > * 先写document，所有标签都在页面里，而页面所有内容存在document里
     > * querySelector查询选择器：选择匹配的第一个元素
     > * 括号里**参数**必须**加引号**，包含一个或多个有效的css选择器 **字符串**
     > * **返回值**：返回的是css选择器匹配的**第一个元素**，一个HTMlElement对象，如果没有匹配到，则返回null

   * [文档对象模型方法]([document.querySelector() - Web API 接口参考 | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/querySelector))

   

2. 选择匹配的多个元素（获取多个DOM元素）

   * 不能直接修改，只能通过遍历方式一次给里面元素做修改

   * 语法：

     ```javascript
     document.querySelectorAll('css选择器')
     ```

     ```javascript
     // 选择所有的小li
     const lis = document.querySelectorAll('ul li')
     console.log(lis) //NodeList(3) [li,li,li]
     ```

     

     > **注：**
     >
     > * 参数包含一个或多个有效的css选择器 **字符串**
     > * **返回值**：返回的是css选择器匹配的NodeList ,一个列表 **对象集合** 数组形式展示

   * querySelectorAll()得到的是一个**伪数组**

   * 有长度有索引号的数组，但是没有pop() push()等数组方法

   * 想要得到里面的每一个对象，则需要遍历(for)方式获得

     ```html
     <body>
     <ul class="nav">
       <li>我的首页</li>
       <li>产品介绍</li>
       <li>练习方式</li>
     </ul>
     <script>
       // 获取元素
       const lis = document.querySelectorAll('.nav li')
       // console.log(lis)
       //for循环遍历  
       for (let i = 0; i < lis.length; i++) {
         console.log(lis[i]) // 每一个小li对象
       }
     </script>
     </body>
     ```

     

     ```html
     <title>Document</title>
       <style>
     
     ```
   
    </style>
     </head>
   
     <body>
       <ul>
         <li class="item">1</li>
         <li class="item">2</li>
         <li class="item">3</li>
       </ul>
       <script>
         const lis = document.querySelectorAll('.item')
         // lis[0].classList.add('active')
         console.log(lis)
         for (let i = 0; i < lis.length; i++) {
           lis[i].style.color = 'red'
         }
       </script>
     ```
   
     
   
   * 哪怕**只有一个元素**，通过**querySelectorAll()**获取过来的也是一个**伪数组**，里面只有一个元素而已
   
     ```javascript
      const p = document.querySelectorAll('#nav')
      console.log(p)
     ```
   









### 其他获取DOM元素方法(了解)

![image-20230924200036046](http://images.newstar.net.cn/sally-imgs/image-20230924200036046.png)

* Element元素 ，getElementBId已经通过id来获取，所以括号里不用加#
* getElementByTagName等同于标签选择器，获取页面所有div，伪数组
* getElementByClassName类名可多次使用，获取页面所有类名为w的，伪数组





## 操作元素内容

* 目的是修改元素的文本更换内容
* DOM对象都是根据标签生成的,所以**操作标签**,**本质上就是操作DOM对象**
* 就是操作对象使用的点语法
* 如果想要**修改标签元素**的里面的**内容**，可使用如下方式：
  1. 对象.innerText (属性)  
  2. 对象.innerHTML (属性)



### 对象.innerText

```javascript
// 1. 第一步获取元素
const box = document.querySelector('.box')
// 2.修改文字内容 对象.innerText 属性
console.log(box.innerText) // 获取文字内容
box.innerText = '内容更改 对象.属性' //修改文字内容

// box.innerText = `<strong>不解析标签</strong>``
// 文字未加粗，只解析文本
```

* 将文本内容添加(更新)到任意标签位置

* innerText属性，显示纯文本，不解析标签



### 对象.innerHTML

```javascript
// 3.修改内容 解析标签 innerHTML
console.log(box.innerHTML)
// box.innerHTML = '更换内容'
box.innerHTML = `<strong>更换内容</strong>`// 文字加粗
```

* 将文本内容添加(更新)到任意标签位置
* innerHTML属性，会解析标签，**多标签**建议使**用模板字符串**







## 操作元素属性

### 操作元素常用属性

* 还可以**通过JS设置/修改** 标签**常用元素属性**，比如通过 src更换 图片

* 最常见的属性比如： href、title、src 等

* 语法：

  ```javascript
  对象.属性 = 值
  ```

  ```javascript
  <img src="../images/hero/1.webp" alt="" />
  <script>
    // 1.获取图片元素
    const pic = document.querySelector('img')
    // 2.修改图片对象的属性
    pic.src = '../images/hero/10.webp'
    pic.title = '夏洛特'
  </script>
  ```

  > **注：**对象.属性 = '新值'





### 操作元素**样式**属性

* 可以通过 JS 设置/修改标签 **元素的样式属性**
* 修改少量样式较有优势
* 比如通过 轮播图小圆点自动更换颜色样式
* 点击按钮可以滚动图片，这是移动的图片的位置 left 等等



#### 通过 style 属性操作CSS(修改样式)

  ```javascript
  对象.style.样式属性 = 值 
  ```

  ```html
  <title>通过 style 属性修改样式</title>
  <style>
  div {
    width: 200px;
    height: 200px;
    background-color: pink;
  }
  </style>
  </head>
  <body>
  <div class="box"></div>
  <script>
  // 1.获取元素
  const box = document.querySelector('.box')
  // 2.修改样式属性 对象.style.样式属性 = '值' 别忘跟单位
  box.style.width = '300px'
  // 样式属性是-连接的单词 采取小驼峰命名法
  box.style.backgroundColor = 'hotpink'
  box.style.border = '2px solid gray'
  box.style.borderTop = '2px solid green'
  </script>
  </body>
  ```

  > **注：**
  >
  > 1. 修改样式通过**style**属性引出
  > 2. 若CSS属性有-连接符，单词转为**小驼峰**命名法
  >    * 例如：background-color ———— backgroundColor 
  > 3. 赋值的时候，需要的时候不要忘记加**CSS单位** (样式属性，大部分数字后都要加单位)
  > 4. 生成的是行内样式，权重比较高(想在CSS里调样式得加!import)








#### 操作类名(className) 操作CSS

  * 可以同时修改多个样式。即修改大量样式更方便

  * 修改的样式比较多，直接通过style属性较繁琐，采取CSS类名形式

    ```javascript
    // active 是一个CSS类名
    元素.className = 'active'
    ```

    > **注：**
    >
    > 1. **class是关键字，所以使用className代替**,*属性虽然写的是className但解析时还是class*
    > 2. className是使用**新值换旧值**(会覆盖之前的类名)，如需保留之前的类名，则添加一个类名
    > 3. 多个类名操作麻烦
    
    ```html
    <style>
          div {
            width: 200px;
            height: 200px;
            background-color: orange;
          }
          .nav {
            color: red;
          }
          .box {
            width: 300px;
            height: 300px;
            background-color: paleturquoise;
            margin: 100px auto;
            padding: 10px;
            border: 1px solid black;
          }
        </style>
      </head>
      <body>
        <div class="nav">123</div>
        <script>
          // 1.获取元素
          const div = document.querySelector('div')
          // 2.添加类名 属性虽然写的是className但解析时还是class
          div.className = 'nav box' //保留之前的类名
        </script>
      </body>
    ```
    
    



#### classList操作类控制CSS(重点)

* 三个方法：add() remove() toggle()

* 为了**解决className**容易**覆盖**以前的**类名**，我们可以通过**classList方式追加和删除类名**

* 修改大量样式更方便且**classList追加和删除不影响以前的类名**

* 语法：

  ```javascript
    // 追加一个类
    元素.classList.add('类名')
    // 删除一个类
    元素.classList.remove('类名')
    // 切换一个类
    元素.classList.toggle('类名')
  ```

  ```html
     <style>
          .box {
            width: 200px;
            height: 200px;
            color: #000;
          }
          .active {
            color: orange;
            background-color: bisque;
          }
        </style>
      </head>
      <body>
        <div class="box">文字</div>
        <script>
         const box = document.querySelector('.box')
          // 追加一个类 元素.classList.add('类名')
          // 追加类 add()类名不加点，并且是字符串
          // box.classList.add('active')
    
          // 删除一个类 元素.classList.remove('类名')
          // 删除类 remove()类名不加点，并且是字符串
          // box.classList.remove('box')
    
          // 切换一个类 元素.classList.toggle('类名')
          // 切换类 toggle(),有无类名，有就删掉，没有就加上
          box.classList.toggle('active')
        </script>
      </body>
  ```

  > **注：**
  >
  > 1. 追加类 add()类名不加点，还是字符串
  > 2. 删除类 remove()类名不加点，并且是字符串
  > 3. 切换类 toggle(),有无类名，有就删掉，没有就加上
  > 4. 三个方法，注意加()
  > 5. 不影响以前的类名





### 操作表单元素属性

* 表单很多情况，也需要修改属性，比如点击眼睛，可以看到密码，本质是把表单类型转换为文本框

* 正常的有属性有取值的 跟其他的标签属性没有任何区别

  * 获取: DOM对象.属性名
  * 设置/修改: DOM对象.属性名 = 新值

* 语法：

  ```javascript
  表单.value = '用户名'
  表单.type  = 'password'
  ```

  ```javascript
  <input type="text" value="电脑" />
  <script>
    const uname = document.querySelector('input')
    // 获取值 获取表单里面的值 用的 表单.value
    // console.log(uname.value) // 电脑
    // console.log(uname.innerHTML) // innerHTML得不到表单元素
  
    // // 设置表单的值
    // uname.value = '我要买电脑'
    // console.log(uname.type)
    uname.type = 'password'
  </script>
  ```

  > **注：**
  >
  > * innerHTML可以得到元素内容，但仅限于普通元素，得不到表单元素，想要表单元素只有value
  > * **但button**为双标签，比较特殊，需使**用innerHTML**
  >
  > 







* 表单属性中添加就有效果,移除就没有效果，一律使用**布尔值**表示。若为true，代表添加了该属性;若为false，代表移除了该属性
* 比如： **disabled、checked**、selected

![image-20231003211733950](http://images.newstar.net.cn/sally-imgs/image-20231003211733950.png)

```javascript
<input type="checkbox" name="" id="" />
<button>点击</button>

<script>
const ipt = document.querySelector('input')
console.log(ipt.checked) // false
ipt.checked = true

const button = document.querySelector('button')
// console.log(button.disabled) // 默认false 不禁用
button.disabled = true // 禁用按钮
</script>
```

>**注：**
>
>1. **disabled、checked常用**，是否禁用和勾选，，一律使用**布尔值**表示
>   * checked = true (勾选)
>   * disabled = true (禁用)
>2. selected下拉菜单很少用到，disabled、checked





### 自定义属性

* **标准属性:** 标签天生自带的属性 比如class id title等, 可以直接使用点语法操作比如： disabled、checked、selected

* **自定义属性：**

  * 在html5中推出来了专门的data-自定义属性

  * 在标签上一律**以 data- 开头**

  * 在DOM对象上一律**以dataset对象方式获取**

    ![image-20231003214311902](http://images.newstar.net.cn/sally-imgs/image-20231003214311902.png)

  ```javascript
  <div data-id="1" data-spm="不知道">1</div>
  <div data-id="2">2</div>
  <div data-id="3">3</div>
  <div data-id="4">4</div>
  <div data-id="5">5</div>
  <script>
    const one = document.querySelector('div')
    console.log(one.dataset.id) //1  dataset对象集合
    console.log(one.dataset.spm) // 不知道
  </script>
  ```






#### 补充-自定义属性

* 没有序号，如何选出div

  ```javascript
  <div data-id="0"></div>
      <script>
        const div = document.querySelector('div')
        console.log(div.dataset.id) // 拿到0
      </script>
  ```

  





## 定时器

* 网页中经常会需要一种功能：每隔一段时间需要**自动**执行一段代码，不需要我们手动去触发
* 例如：网页中的倒计时，要实现这种需求，需要**定时器函数**
* 目标：能够使用**定时器**函数**重复执行**代码
* 定时器函数有两种：**间歇**函数**setInterval**、 **延时**函数**setTimeout**
* **作用：**可以根据时间**自动重复执行**某些代码



### 定时器-间歇函数

* 定时器函数可以开启和关闭定时器



#### 开启定时器

* 语法：

  ```javascript
  setInterval(函数, 间隔时间)
  ```

  * 作用：每隔一段时间调用前面这个函数
  * **间隔时间单位是毫秒**

  ```javascript
  // 开启定时器 写法1：匿名函数：setInterval(函数, 毫秒)
  // setInterval(function () {
  //   console.log('一秒执行一次')
   }, 1000)
  
  // 写法2：具名函数写法：setInterval(函数名, 间隔时间) 函数名不加小括号
  function fn() {
    console.log('三秒执行一次')
  }
  setInterval(fn, 3000) // 每间隔3秒执行一次
  
  // 写法3：
  // function fn() {
  //  console.log('一秒执行一次')
  }
  // setInterval('fn()', 1000) 极为少见的写法
  ```

  > **注：**
  >
  > 1. 函数名**不需要加括号**
  > 2. **定时器返回的是一个id数字**(也就是一个序号，页面中有几个定时器开，就有几个序号排列。每个定时器都有独一无二的的序号)

  ```javascript
  function fn() {
    console.log('三秒执行一次')
  }
  
  let n = setInterval(fn, 3000) 
  console.log(n) // 序号为2
  
  
  let m = setInterval(function () {
    console.log(11)
  }, 1000)
  console.log(m) // 序号为3
  ```

  * `注：此处用let声明，因为定时器要开要关，返回的值是数字型，里面的值会有变化，后面有重新赋值操作`





#### 关闭定时器

* 语法：

  ```javascript
  let 变量名 = setInterval(函数, 间隔时间)
  clearInterval(变量名)
  ```

  * 一般不会刚创建就停止，而是满足一定条件再停止
  * 函数名**不加括号**
  * 关闭定时器必须有变量名

  ```javascript
  function timer() {
    console.log('一秒执行一次')
  }
  let n = setInterval(timer, 1000)
  clearInterval(n) // 关闭定时器 
  ```

  



## 事件监听

* 也称为**绑定事件**或**注册事件**

* 事件：是在编程时系统内部发生的**动作**或者发生的事情

  * 比如用户在网页上**单击**一个按钮

* 事件监听:是让程序员检测是否有事件产生，一旦**有事件触发**，**就立即调用**一个函数**做出响应**

  * 比如鼠标经过显示下拉菜单
  * 比如点击可以播放轮播图等

* 语法：

  ```javascript
  元素对象.addEventListener('事件类型', 要执行的函数)
  ```

  > **事件监听三要素：**
  >
  > * 事件源：那个dom元素被事件触发了，要获取dom元素
  > * 事件类型：用什么方式触发，比如鼠标单击click、鼠标经过mouseover等
  > * 事件调用的函数(事件处理程序)：要做什么事

  ```javascript
  <button>按钮</button>
  <script>
    const btn = document.querySelector('.btn')
    // 修改元素样式
    btn.addEventListener('click', function () {
      alert{'点击了'}
    })
  </script>
  ```

  > **注：**
  >
  > 1. **事件类型加引号**
  > 2. **函数是点击之后再去执行，每次点击都会执行一次**





### 拓展-事件监听版本

* DOM LO (L全称Level级别)

  事件源.on事件 = function() { }

  ```javascript
  <button>点击</button>
  <script>
  const btn = document.querySelector('button')
  btn.onclick = function () {
    alert(11)
  }
  btn.onclick = function () {
    alert(22)
  } // 结果被22覆盖
  </script>
  ```

  > **注：**DOM LO，是最早级别，事件监听的第一个版本，写法是on事件
  >
  > * on方式会被覆盖，等同于赋值的方式
  > * 只有冒泡，没有捕获且只能做冒泡





* DOM L2 

  事件源.addEventListener(事件， 事件处理函数)

  > **注：**
  >
  > 1. 可以冒泡和捕获
  > 2. addEventListener方式可绑定多次，拥有事件更多特性，推荐使用

  





## 补充-两种注册事件的区别

### 传统on注册(L0)

* 同一个对象,后面注册的事件会覆盖前面注册(同一个事件)
* 直接使用null覆盖偶就可以实现事件的解绑
* 都是冒泡阶段执行的





### 事件监听注册（L2）

* 语法: addEventListener(事件类型, 事件处理函数, 是否使用捕获)
* 后面注册的事件不会覆盖前面注册的事件(同一个事件)
* 可以通过第三个参数去确定是在冒泡或者捕获阶段执行
* 必须使用removeEventListener(事件类型, 事件处理函数, 获取捕获或者冒泡阶段)
* 匿名函数无法被解绑









## 事件类型

### 鼠标事件 鼠标触发

* click 鼠标点击

  * mouseenter 鼠标经过

  * mouseleave 鼠标离开

    ```html
     <style>
          div {
            width: 200px;
            height: 200px;
            background-color: pink;
          }
        </style>
      </head>
      <body>
        <div></div>
        <script>
          const div = document.querySelector('div')
          // 鼠标经过
          div.addEventListener('mouseenter', function () {
            console.log('我来了')
          })
          // 鼠标离开
          div.addEventListener('mouseleave', function () {
            console.log('我走了')
          })
        </script>
    ```

    







### 补充-鼠标经过事件的区别

1. 鼠标经过事件：

   * 鼠标经过mouseover 和 鼠标离开mouseout 会有冒泡效果

     ```html
     <style>
           .dad {
             width: 400px;
             height: 400px;
             background-color: pink;
           }
     
           .baby {
             width: 200px;
             height: 200px;
             background-color: purple;
           }
         </style>
       </head>
       <body>
         <div class="dad">
           <div class="baby"></div>
         </div>
         <script>
           const dad = document.querySelector('.dad')
           const baby = document.querySelector('.baby')
           dad.addEventListener('mouseover', function () {
             console.log('鼠标经过')
           })
           dad.addEventListener('mouseout', function () {
             console.log('鼠标离开')
           })
         </script> 
     ```

     

   * 鼠标经过**mouseenter 和 鼠标离开mouseleave 没有冒泡效果 (推荐)**





### 焦点事件 表单获得光标

* focus 获得焦点

* blur 失去焦点

  ```javascript
   <input type="text" />
      <script>
        const input = document.querySelector('input')
        input.addEventListener('focus', function () {
          console.log('有焦点触发')
        })
        input.addEventListener('blur', function () {
          console.log('失去焦点触发')
        })
      </script>
  ```





### 键盘事件 键盘触发

* Keydown 键盘按下触发

* **Keyup 键盘抬起触发**  (建议常用)

  ```javascript
  <input type="text">
  <script>
  const input = document.querySelector('input')
  // 1. 键盘事件
  // input.addEventListener('keydown', function () {
  //   console.log('键盘按下了')
  // })
  // input.addEventListener('keyup', function () {
  //   console.log('键盘谈起了')
  // })
  // 2. 用户输入文本事件  input
  input.addEventListener('input', function () {
    console.log(input.value)
  })
  </script>
  ```





### 文本事件 表单输入触发

* input 用户输入事件

  ```javascript
  <input type="text" />
  <script>
  // 2. 用户输入文本事件  input
  const input = document.querySelector('input')
  input.addEventListener('input', function () {
    console.log(input.value)
  })
  </script>
  ```







## 事件对象

* 事件对象 **也是个对象**，(存储了事件的相关信息)即这个**对象里有事件触发时的相关信息**

* 例如：鼠标点击事件中，事件对象就存了鼠标点在哪个位置等信息

* 使用场景：
  * 可以判断用户按下哪个键，比如按下回车键可以发布新闻
  * 可以判断鼠标点击了哪个元素，从而做相应的操作



### 获取事件对象(重点)

* 如何获取

* 语法：

  * 在事件绑定的回调函数的**第一个参数就是事件对象**

  * 一般命名为**event、ev、e**

    ```javascript
    元素.addEventListener('click', function(e){
        
    }) // e为事件对象
    ```

    



### 事件对象常用属性

* type 

  获取当前的事件类型

  

* clientX/clientY 

  获取光标相对于浏览器可见窗口左上角的位置

  

* offsetX/offsetY 

  获取光标相对于当前DOM元素左上角的位置

  

* **key** 

  用户按下的键盘键的值

  现在不提倡使用keyCode

  ```javascript
  <input type="text" />
  <script>
  const input = document.querySelector('input')
  input.addEventListener('keyup', function (e) {
  // console.log(11)
  // console.log(e.key)
  if (e.key === 'Enter') {
    console.log('我按下了回车键')
  }
  })
  </script>
  ```

  



## 环境对象

* 环境对象：指的是 <u>函数内部特殊</u>的**变量this**，它**<u>代表着当前函数运行时所处的环境</u>**

* 目标：分析判断函数运行在不同环境中this所指代的对象

* **作用：**弄清this指向，让代码更简洁

  * 函数的调用方式不同，this 指代的对象也不同

    ```javascript
    <button>点击</button>
    <script>
    // 每个函数里都有this 环境对象 普通函数里this指向window
    // function fn() {
    //   console.log(this)
    // }
    // window.fn()
    const btn = document.querySelector('button')
    btn.addEventListener('click', function () {
      console.log(this) // btn调用的 对象就是btn
      // btn.style.color = 'red'
      this.style.color = 'red'
    })
    </script>
    ```

    > **注：**
    >
    > 1. 【**谁调用， this 就是谁**】 是判断this指向的粗略规则
    > 2. 直接调用函数，其实相当于是 window.函数，所以this指代 window

    

    





## 回调函数

* 如果将函数 A 做为参数传递给函数 B 时，我们称函数 A 为回调函数，即当**一个函数当做参数**来**传递给另外一个函数**的时候，**这个函数就是回调函数**

* 常见使用场景：

  ```javascript
  function fn() {
    console.log('我是回调函数')
  }
  // fn传递给了setInterval，fn就是回调函数
  setInterval(fn, 1000)
  ```

  ```javascript
   box.addEventListener('click', function () {
     console.log('我也是回调函数')
   })
  ```

  > **注：**
  >
  > 1. 把函数当做另外一个函数的参数传递，这个函数就叫**回调函数**
  > 2. 回调函数**本质还是函数**，只不过把它**当成参数使用**
  > 3. 使用**匿名函数作为回调函数**较常见
  > 4. 回调函数不会立马执行，时机成熟才调用









## 事件流

###  事件流和两个阶段说明

#### 事件流

* 指的**是事件**完整执行过程中的**流动**路径 （事件捕获-事件目标阶段-事件冒泡）

![image-20231020164631217](http://images.newstar.net.cn/sally-imgs/image-20231020164631217.png)

* 说明：假设页面里有个div，当触发事件时，会经历两个阶段，分别是捕获阶段、冒泡阶段

* 简单来说：**捕获**阶段是 从**父到子**(从大到小) ; **冒泡**阶段**是从子到父**（从小到大）

  > **注：** **实际工作都是使用事件冒泡为主**





#### 事件捕获阶段

* 简单了解事件捕获过程

* **事件捕获概念：**

  * 从DOM的根元素开始去执行对应的事件 (从外到里)

  * 事件捕获需要写对应代码才能看到效果

  * 代码：

    ```javascript
    DOM.addEventListener(事件流，时间处理函数，是否使用捕获机制)
    ```

    > * addEventListener第三个参数传入 **true** 代表是捕获阶段触发（很少使用）
    >
    > * 若传入false代表冒泡阶段触发，默认就是false
    >
    > * 若是用 L0 事件监听，则只有冒泡阶段，没有捕获





#### 事件冒泡阶段（重点）

* **事件冒泡概念:** 当一个元素的事件被触发时，同样的事件将会在该元素的所有祖先元素中依次被触发。这一过程被称为事件冒泡

* 简单理解：当一个元素触发事件后，会依次向上调用所有父级元素的 **同名事件**

  ```html
  <style>
  .father {
  width: 500px;
  height: 500px;
  background-color: pink;
  }
  
  .son {
  width: 200px;
  height: 200px;
  background-color: purple;
  }
  </style>
  </head>
  <body>
  <div class="father">
  <div class="son"></div>
  </div>
  <script>
  const fa = document.querySelector('.father')
  const son = document.querySelector('.son')
  //  蓝翔  济南   山东   冒泡阶段
  document.addEventListener('click',function () {
  alert('我是爷爷')
  })
  fa.addEventListener('click',function () {
  alert('我是爸爸')
  })
  son.addEventListener('click',function () {
  alert('我是儿子')
  })
  </script>
  ```

  > **注：**
  >
  > * 事件冒泡是默认存在的
  > * L2事件监听第三个参数是 false，或者默认都是冒泡





#### 阻止冒泡

* **问题：**因为默认就有冒泡模式的存在，所以容易导致事件影响到父级元素

* **需求：**若想把事件就限制在当前元素内，就需要阻止事件冒泡

* **前提：**阻止事件冒泡需要拿到事件对象

* **语法：**

  ```javascript
  事件对象.stopPropagation()
  ```

  > **注：** 此方法可**阻断事件流动传播**，不光在冒泡阶段有效，捕获阶段也有效

  ```javascript
  <script>
  const fa = document.querySelector('.father')
  const son = document.querySelector('.son')
  //  蓝翔  济南   山东   冒泡阶段
  document.addEventListener('click', function () {
    alert('我是爷爷')
  })
  fa.addEventListener('click', function () {
    alert('我是爸爸')
  })
  son.addEventListener('click', function (e) {
    alert('我是儿子')
    // 阻止冒泡（流动传播） 事件对象.stopPropagation()
    e.stopPropagation()
  })
  ```

  > **注：**
>
  > 1. 先要明确哪一块区域不能冒泡
  > 2. 需要阻止什么事件传递就给这块区域最大盒子注册该事件
  > 3. 在事件处理函数里面接受事件对象，并添加上e.stopPropagation()

  







#### 阻止元素默认行为

* **我们某些情况下需要**阻止默认行为的发生，比如 阻止 链接的跳转，表单域跳转

* 语法：

  ```html
  e.preventDefault()
  ```

  ```javascript
  <form action="http://www.baidu.com"></form>
  <input type="submit" value="提交" />
  <script>
    const form = document.querySelector('form')
    form.addEventListener('click', function (e) {
      // 阻止表单默认提交行为
      e.preventDefault()
    })
  </script>
  ```

  



#### 解绑事件（了解）

#####  on事件方式

* **直接使用null**覆盖偶就可以实现事件的解绑

* 语法：

  ```javascript
  // 绑定事件
  btn.onclick = function () {
      alert?('点击了')
  }
  // 解绑事件
  btn.onclick = null
  ```

  ```javascript
  <button>点击</button>
  <script>
  const btn = document.querySelector('button')
  // btn.onclick = function () {
  //   alert('点击了')
  //   // L0 事件移除解绑
  //   btn.onclick = null
  // }
  </script>
  ```

  



##### addEventListener方式

* **必须使用removeEventListener**(事件类型, 事件处理函数, [获取捕获或者冒泡阶段])

* 例如：

  ```javascript
  <button>点击</button>
  <script>
  const btn = document.querySelector('button')
  
  function fn() {
    alert('点击了')
  }
  btn.addEventListener('click', fn)
  // L2 事件移除解绑
  btn.removeEventListener('click', fn)
  </script>
  ```

  > **注：** 匿名函数无法被解绑







## 事件委托

1. 如果同时给**多个元素注册事件**，以往我们**用 for循环注册事件**
2. 而事件委托 注册一次事件就能完成以上效果

3. **事件委托是**利用事件流的特征解决一些开发需求的知识**技巧**

   * 优点：**减少注册次数，可以提高程序性能**

   * 原理：事件委托其实是利用事件冒泡的特点(**自己不注册事件，将对应事件注册给祖先元素**)

     * (委托给父元素)给**父元素注册事件**，当我们触发子元素的时候，会冒泡到父元素身上，从而触发父元素的事件

     * ul.addEventListener('click' , function(){}) 执行父级点击事件

     <img src="http://images.newstar.net.cn/sally-imgs/image-20231023142243502.png" alt="image-20231023142243502" style="zoom:100%;" />

     > **分析：**
     >
     > 1. 大的父元素 包含li子元素
     > 2. 事件写到ul上，li则不添加事件，不需要循环
     > 3. 给小li做点击事件，点击的是小li，没有监听事件，但事件本身有事件流，会冒泡，往ul父元素身上跑，ul有事件监听,所以会执行里面的代码

     

   * 实现：**事件对象.target.tagName** 可以获得**真正触发**事件**的元素**

     ```javascript
      <ul>
           <li>第1个孩子</li>
           <li>第2个孩子</li>
           <li>第3个孩子</li>
           <li>第4个孩子</li>
           <li>第5个孩子</li>
           <p>我不需要变色</p>
         </ul>
         <script>
           // 点击每个小li 当前li 文字变为红色
           // 按照事件委托的方式  委托给父级，事件写到父级身上
           // 1. 获得父元素
           const ul = document.querySelector('ul')
           ul.addEventListener('click', function (e) {
             // alert(11)
             // this.style.color = 'red'
             // console.dir(e.target) // 就是我们点击的那个对象li
             // e.target.style.color = 'red'
             // 我的需求，我们只要点击li才会有效果
             if (e.target.tagName === 'LI') {
               e.target.style.color = 'red'
             }
           })
         </script>
     ```

     > **注：**
     >
     > 1. 找到真正被触发的元素 e.target
     > 2. 如果要加判断条件 必须是当前某种元素的话加上tagName







## 其他事件

### 页面加载事件

* 加载外部资源（如图片、外联CSS和JavaScript等）加载完毕时触发的事件

* 为什么要学？

  * 有些时候需要等页面资源全部处理完了做一些事情

  * 老代码喜欢把script写在head中，这时候直接找dom元素找不到

    ```javascript
    <script>
          const btn = document.querySelector('button')
          btn.addEventListener('click', function () {
            alert(11) // 11弹不出来，不能读取该属性 为空，从上往下执行 代码抓不到btn
          })
    </script>
    </head>
    <body>
    <button>点击</button>
    ```

    

* 事件名：load

* 监听页面所有资源加载完毕：**给window添加load事件**

  ```javascript
   window.addEventListener('load',function(){
       // 执行的操作
   })
  ```

  

  ```javascript
  <script>
    // 等待页面所有资源加载完毕，就回去执行回调函数
    window.addEventListener('load', function () {
      const btn = document.querySelector('button')
      btn.addEventListener('click', function () {
        alert(11)
      })
    })
  </script>
  </head>
  <body>
  <button>点击</button>
  ```

  > **注：**不光可以监听整个页面资源加载完毕，也可以针对某个资源绑定load事件

  ```javascript
   img.addEventListener('load', function () {
          // 等待图片加载完毕，再去执行里面的代码
        })
  ```





### DOMContentLoaded事件

* 当初始的HTML文档被完全加载和解析完成之后，DOMContentLoaded 事件被触发，而**无需等待样式表、图像等完全加载**,比页面加载事件执行速度更快

* 事件名：DOMContentLoaded

* 监听页面DOM加载完毕：**给document添加**DOMContentLoaded事件

  ```javascript
   document.addEventListener('DOMContentLoaded',function(){
          // 执行的操作
        })
  
  ```

  ```javascript
  document.addEventListener('DOMContentLoaded', function () {
          const btn = document.querySelector('button')
          btn.addEventListener('click', function () {
            alert(11)
          })
        })
  ```

  



### 页面元素滚动事件

* 滚动条在滚动的时候持续触发的事件

* 为什么要学？

  * 很多网页需要检测用户把页面滚动到某个区域后做一些处理， 比如固定导航栏，比如返回顶部

* 事件名：scroll

* 监听整个页面滚动：**给window或document添加** scroll 事件

* 监听某个元素的内部滚动直接给某个元素加即可

  ```javascript
  window.addEventListener('scroll', function () {
      // 执行的操作
  })
  ```

  ```javascript
  <style>
    body {
      height: 3000px;
    }
  </style>
  </head>
  <body>
  <script>
    // 页面滚动事件
    window.addEventListener('scroll', function () {
      console.log('我滚了')
    })
  </script>
  ```

  

  

##### 页面滚动事件-获取位置

* **scrollLeft和scrollTop （属性）**

* scrollLeft被卷去的左侧

* scrollTop被卷去的头部

  * 获取被卷去的大小

  * 获取元素内容往左、往上滚出去看不到的距离

  * 这两个值是可**读写**的，可以**读取**，也可以**修改（赋值）**

    ![image-20231024173935981](http://images.newstar.net.cn/sally-imgs/image-20231024173935981.png)

* **尽量在scroll事件里面获取被卷去的距离**

  ```javascript
   div.addEventListener('scroll', function () {
          console.log(this.scrollTop)
        })
  ```








* 开发中，我们经常检测页面滚动的距离，比如页面滚动100像素，就可以显示一个元素，或者固定一个元素

  ```javascript
const div = document.querySelector('div')
  // 页面滚动事件
window.addEventListener('scroll', function () {
      // 获取html元素写法： document.documentElement
    const n = document.documentElement.scrollTop
    console.log(n)
  })
  ```

  
  
  
  
  
  
  > **注：**
  >
  > 1. 想知道页面到底滚动了多少像素,被卷去了多少  用scrollTop
  >
  > 2. 获取html元素写法： document.documentElement html文档返回对象是html元素
  
```javascript
  const div = document.querySelector('div')
  // 页面滚动事件
  window.addEventListener('scroll', function () {
    const n = document.documentElement.scrollTop
    if (n >= 100) {
      div.style.display = 'block'
    } else {
      div.style.display = 'none'
    }
  })
```

  



##### 补充-scrollTop细节-滚动指定目标写法1

* 获取页面被卷去的头部 要获得html元素被卷去多少

  ```javas
  // 自定义滚动条不滚动，设置滚动条跑到800
  document.documentElement.scrollTop = 800
  window.addEventListener('scroll', function () {
   // 必须写到里面
    console.log(document.documentElement.scrollTop)
    // 得到是数字型数据 不带单位
    // console.log(n)
  })
  ```

  > **注：**
  >
  > 1. document.documentElement.scrollTop必须写到里面
  > 2. 得到是数字型数据 不带单位
  > 3. 可**读写**，可以**读取**，也可以**修改（赋值）**
  > 4. document.documentElement.scrollTop = 800







##### 页面滚动事件-滚动到指定的坐标写法2

* scrollTo() 方法可把内容滚动到指定的坐标

* 语法：

  ```javascript
  元素.scrollTo(x, y)
  ```

  

* 例如：

  ```javascript
  window.scrollTo(0, 1000) //让页面滚动到 y轴 1000像素的位置
  ```

  

  

  

### 页面尺寸(缩放)事件

* 会在窗口尺寸改变(浏览器窗口大小发生变化)的时候触发事件

* 事件名：resize 

  ```javascript
  window.addEventListener('resize', function() {
      // 执行的代码
  })
  ```

  

* 检测屏幕宽度:

  ```html
  <style>
    div {
      display: inline-block;
      /* width: 200px; */
      height: 200px;
      background-color: pink;
      padding: 10px;
      border: 20px solid red;
    }
  </style>
  </head>
  <body>
  <!-- 注释宽度，我们无法判断盒子的宽度， js可以 -->
  <div>123123123123123123123123123123123123123</div>
  <script>
    const div = document.querySelector('div')
    console.log(div.clientWidth) //获取元素宽度（不含边框border，margin，滚动条等）
    // resize 浏览器窗口大小发生变化的时候触发的事件
    window.addEventListener('resize', function () {
      console.log(1)
    })
  </script>
  ```

  > **注：**
  >
  > * 获取元素宽高：
  >   **clientwidth和clientHeight** 获取元素的可见部分宽高(**不包含边框border**，margin，滚动条等）



![image-20231025163043710](http://images.newstar.net.cn/sally-imgs/image-20231025163043710.png)





## 元素尺寸于位置

* 使用场景：
  1. 前面案例滚动多少距离，都是我们自己算的，最好是页面滚动到某个元素，就可以做某些事。
  2. 简单说，就是**通过js**的方式，得到**元素在页面中的位置**
  3. 这样我们可以做，页面滚动到这个位置，就可以做某些操作，省去计算了

![image-20231025182232446](http://images.newstar.net.cn/sally-imgs/image-20231025182232446.png)





### 元素尺寸于位置-尺寸

* 获取宽高：

  1. 获取元素的自身宽高、**包含**元素自身设置的宽高、padding、**border**
  2. **offsetWidth**和**offsetHeight**
  3. 获取出来的是数值,方便计算

  > **注：** 
  >
  > * 获取的是可视宽高, 如果盒子是隐藏的,获取的结果是0
  > * 得到元素内容 + padding + border的宽高



* 获取位置：
  1. 获取元素距离自己定位父级元素的左、上距离
  2. **offsetLeft 和 offsetTop 注意是只读属性**

![image-20231025182659609](http://images.newstar.net.cn/sally-imgs/image-20231025182659609.png)

> **注：**offsetTop和offsetLeft得到的位置以谁为准？
>
> * **带有定位的父级**
> * 如果**都没有** 则以**文档左上角 为准**

```html
<style>
  div {
    position: relative;
    width: 200px;
    height: 200px;
    background-color: pink;
    margin: 100px;
  }
  p {
    width: 100px;
    height: 100px;
    background-color: purple;
    margin: 50px;
  }
</style>
</head>
<body>
<div>
  <p></p>
</div>
<script>
  const div = document.querySelector('div')
  // console.log(div.offsetLeft)
  const p = document.querySelector('p')
  // 检测盒子的位置  最近一级带有定位的祖先元素
  console.log(p.offsetLeft)
</script>
```

