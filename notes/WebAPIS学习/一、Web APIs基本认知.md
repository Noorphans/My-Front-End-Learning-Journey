#  Dom获取&属性操作 

[toc]





## DOM和BOM基本认知

* **WebAPI是**一套 **操作**网页内容(**DOM**)与浏览器窗口(BOM)**的对象**



### 变量声明

* 变量声明有三个： var 、let、 const

1. `声明变量优先const`

   * 常量也是变量，只不过使用**const**声明被称为“常量”

   * const语义化更好

   * 实际开发中，如React框架，基本用const

   * 使用规范和变量一样

   * 当**某个变量**永远 **不会改变**的时候，就可以用**const声明**，而不是let

     

2. 常量使用：

     ```javascript
     //声明一个常量
     const G = 9.8
     //输出这个常量
     console.log(G)
     ```
     
     > **注：**
     >
     > 1. const声明的值不能更改 即**不允许重新赋值**，**声明时就必须赋值（初始化**），即不需要重新赋值的数据用const
     > 2. **有了变量先const，发现后面是要被修改的，再改为let**
     > 3. 对于**（复杂）引用数据类型，const声明的变量，栈里存的是地址，**不是值



3. 以下能把let改为const吗？

   * 能，值未做改变 可以改为const

   ```javascript
   document.write('我叫' + '流星雨') // 我叫流星雨
   let uname = '流星雨'
   let song = '告白'
   document.write(uname + song) // 流星雨告白
   ```

   ```javascript
   let num1 = +prompt('请输入第一个值')
   let num2 = +prompt('请输入第二个值')
   alert(`两者和为${num1} + ${num2}`) //值未做改变 可以改为const
   ```

   > 解析：这个程序我们只写了一次，写完之后，页面刷新得到结果就结束，不再做其他操作，循环也没问题，所以值没有发生改变

   

   * 不能，变量进行重新赋值，值发生改变 不能const

   ```javascript
   let num = 1
   num = num + 1
   //  num += 1
   console.log(num) //结果是2
   ```

   ```javascript
   for(let i = 0; i < nums.length; i++) {
       document.write(nums[i])
   } // i不断++,值有改变
   ```

   

   * 能，地址值未发生改变，可以const

   ```javascript
   let arr = ['blue', 'black']
   arr.push('white')
   console.log(arr)
   ```

   ```javascript
   let person = {
     uname: 'sally',
     age: 18,
     sex: '女'
   }
   person.height = 159
   console.log(person)
   ```

   

   * 利用堆栈思想-图片分析：
     * 数组和对象属于复杂数据类型放在堆里
     * 先声明一个数组arr，数组里面有一个值放在堆里
     * 寻找值之前在栈里存放一个地址，即arr开辟一个空间存放地址值，地址值指向堆里的数据值，给数组里添加一个blue，原数组的基础上追加一个元素而已，原数组没变地址值也就没变，地址值没变也就可以改为const（通俗理解：张老师在大夏天加了一件马甲衣，但他还是张老师，只是加了件衣服）

     ![image-20231125132919015](http://images.newstar.net.cn/sally-imgsimage-20231125132919015.png)

   

   * 不能，地址值发生改变，不可以用const

   ```javascript
   let arr = ['blue', 'black']
   arr = [1, 2, 4]
   console.log(arr)
   ```

   

   * 图片分析:中括号是数组，arr得到的是新数组，把新数组给了arr，相当于arr又开辟一个新的数组存放数据值，此时不同数组或对象就有不同地址值寻找，新地址指向数据值，arr指向新地址值（对象做了改变，所以不能const）

     ![image-20231125134303383](http://images.newstar.net.cn/sally-imgsimage-20231125134303383.png)
     
     
     
     


   * 但如果给数组和对象**追加或者删除**属性，就可以const

   ```javascript
const arr = ['blue', 'black']
arr[0] = 1
arr[1] = 2
arr[2] = 3
   ```





### 什么情况下用const？

`const声明数组的对象可以修改里面的属性，是因为对象是引用数据类型，存的是地址值，只要地址不变就不会报错`

1. (5个)**基本数据类型**: 值发生改变 就用let**不能const**
2. 复杂数据类型(Array、object)：地址值未改变(只是添加数组元素)可以用const
3. **数组和对象尽量const声明**





### 什么时候用let声明变量？

1. 基本数据类型的值或引用数据类型的地址发生改变
2. 一个变量进行加减运算
3. for循环中的i++





## DOM和BOM作用与分类

1. 作用：使用JS去操作html和浏览器
2. 分类：`DOM`(文档对象模型)、`BOM`(浏览器对象模型)





## 什么是DOM

1. DOM(Document object model)**文档对象模型**：

   * 是用来呈现以及与任意HTML或XML文档交互的API ，即通过js方式**操作网页内容**的功能，如页面元素的移动、大小等
   * 是将整个 HTML 文档的每一个标签元素视为一个对象，这个对象下包含了许多的属性和方法，通过操作这些属性或者调用这些方法实现对 HTML 的动态更新，为实现网页特效以及用户交互提供技术支撑。
   * 简言之 DOM 是用来动态修改 HTML 的，其目的是开发网页特效及用户交互。

2. DOM作用：

   \- 操作网页内容

   \- 开发网页内容特效和实现用户交互


![demo](http://images.newstar.net.cn/sally-imgsdemo.gif)





## DOM树(文档树)

### DOM树是什么？

1. 将HTML文档以树状结构直观表现出来，称为文档数或DOM树
2. 描述网页内容关系的名词
3. 作用：`文档树直观地体现了标签与标签之间的关系`



\- 举例说明：

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>标题</title>
</head>
<body>
  文本
  <a href="">链接名</a>
  <div id="" class="">文本</div>
</body>
</html>
```

如下图所示，将 HTML 文档以树状结构直观的表现出来.

![web-api](http://images.newstar.net.cn/sally-imgsweb-api.jpg)





### DOM 节点

节点是文档树的组成部分，**每一个节点都是一个 DOM 对象**，主要分为元素节点、属性节点、文本节点等。

1. 【元素节点】其实就是 HTML 标签，如上图中 `head`、`div`、`body` 等都属于元素节点。
2. 【属性节点】是指 HTML 标签中的属性，如上图中 `a` 标签的 `href` 属性、`div` 标签的 `class` 属性。
3. 【文本节点】是指 HTML 标签的文字内容，如 `title` 标签中的文字。
4. 【根节点】特指 `html` 标签。
5. 其它...



\- 举例说明：>DOM - 查找节点

```html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>DOM - 查找节点</title>
</head>
<body>
  <h3>查找元素类型节点</h3>
  <p>从整个 DOM 树中查找 DOM 节点是学习 DOM 的第一个步骤。</p>
  <ul>
      <li>元素</li>
      <li>元素</li>
      <li>元素</li>
      <li>元素</li>
  </ul>
  <script>
  	const p = document.querySelector('p')  // 获取第一个p元素
  	const lis = document.querySelectorAll('li')  // 获取第一个p元素
  </script>
</body>
</html>
```

结论：任意 DOM 对象都包含 nodeType 属性，用来检检测节点类型





## DOM对象（非常重要）

1. DOM核心思想:把网页内容当做对象来处理

2. DOM对象:浏览器根据html标签生成的**JS对象**,在**html里是标签**，即在JS的DOM里获取过来的叫DOM对象（`任何一个标签都是一个对象，只要是对象就有属性和方法`）

   * 所有标签属性都可以在这个对象上面找到
   * 修改这个对象属性会自动映射到标签身上

   ```javascript
   <div>123</div>
   <script>
     const div = document.querySelector('div')
     // 打印对象
     console.dir(div) // 这里的div为dom 对象
   </script>
   ```

   

![image-20231124175436521](http://images.newstar.net.cn/sally-imgsimage-20231124175436521.png)



![image-20231124175727940](http://images.newstar.net.cn/sally-imgsimage-20231124175727940.png)



​					`所以把div获取过来得到的是一个对象，即在html里是标签，在JS的里获取过来的叫DOM对象`





3. **document最大对象**

* 是DOM里提供的一个**对象**

* 它提供的属性和方法都是**用来访问和操作网页内容的**

  \- 例如：document.write()

* 网页所有内容都在document里面

​     ![image-20230923195446590](http://images.newstar.net.cn/sally-imgs/image-20230923195446590.png) 

 

* document` 是 JavaScript 内置的专门用于 DOM 的对象，该对象包含了若干的属性和方法，`document` 是学习 DOM 的核心。

```javascript
<script>
  // document 是内置的对象
  // console.log(typeof document);

  // 1. 通过 document 获取根节点
  console.log(document.documentElement); // 对应 html 标签

  // 2. 通过 document 节取 body 节点
  console.log(document.body); // 对应 body 标签

  // 3. 通过 document.write 方法向网页输出内容
  document.write('Hello World!');
</script>
```

上述列举了 `document` 对象的部分属性和方法，对 `document` 有一个整体的认识。





### 获取DOM对象

目标：能够查找/获取DOM对象

2. 我们想要操作某个标签首先做什么？

   \- 选中该标签，跟css选择器类似，选中标签才能操作

3. `查找(获取)元素DOM元素即 利用JS选择页面中标签元素`



#### 根据css选择器来获取DOM元素(重点)

1. 选择匹配的第一个元素 即获取一个DOM元素（能直接操作修改）


* 语法：

  ```javascript
  document.querySelector('css选择器')
  ```

* 参数：包含一个或多个有效的css选择器 字符串

  * 括号里`参数`**必须**是`字符串`，也**必须**`加引号`

* 返回值：CSS选择器匹配的`第一个元素`,一个 HTMLElement对象。如果没有匹配到，则返回null

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
     <ul class="nav">
       <li>测试1</li>
       <li>测试2</li>
       <li>测试3</li>
     </ul>
     <!-- id快速生成：标签#标签名 p#nav-->
     <script>
       // 写法1：获取匹配的第一个元素，css选择器
       // const box = document.querySelector('div')
       // 写法2：获取匹配的第一个元素，类名写法 .类名 .box
       // const box = document.querySelector('.box')
       // console.log(box)
  
       // const nav = document.querySelector('#nav')
       // 可以直接修改，nav对象，style属性，对象名.属性名
       // nav.style.color = 'red' 
       // console.log(nav)
  
       // 1.获取第一个小ul li
       const li = document.querySelector('ul li:first-child')  
       console.log(li) // 结果是innerHTML和innerText为测试1
      // li:first-child 获取li的第一个元素
      </script>
  </body>
  </html>
  ```

  > 解析：
  >
  > 1. 先写document，所有标签都在页面里，而页面所有内容存在document里
  > 2. querySelector查询选择器：选择匹配的第一个元素
  > 3. 更多详情参考[文档对象模型方法]([document.querySelector() - Web API 接口参考 | MDN (mozilla.org)](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/querySelector))



2. 选择匹配的多个元素 即获取多个DOM元素（不能直接修改，只能通过遍历方式一次给里面元素做修改）

* 语法：

  ```javascript
  document.querySelectorAll('css选择器')
  ```

* 参数：包含一个或多个有效的css选择器 字符串

  * 括号里`参数`**必须**是`字符串`，也**必须**`加引号`

* 返回值：返回的是css选择器匹配的NodeList ,一个列表 **对象集合** 数组形式展示

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
     <ul class="nav">
       <li>测试1</li>
       <li>测试2</li>
       <li>测试3</li>
     </ul>
     <!-- id快速生成：标签#标签名 p#nav-->
     <script>
       // 写法1：获取匹配的第一个元素，css选择器
       // const box = document.querySelector('div')
       // 写法2：获取匹配的第一个元素，类名写法 .类名 .box
       // const box = document.querySelector('.box')
       // console.log(box)
  
       // const nav = document.querySelector('#nav')
       // 可以直接修改，nav是对象，style是属性，写法：对象名.属性名
       // nav.style.color = 'red' 
       // console.log(nav)
  
       // 2.选择所有的小li
       const lis = document.querySelectorAll('ul li')
       console.log(lis) //NodeList(3) [li,li,li]
      </script>
  </body>
  </html>
  ```

  


> * querySelectorAll()得到的是一个`伪数组`
>
>   \- 有长度有索引号的数组
>
>   \- 但是没有pop() push()等数组方法
>
>   \- 想要得到里面的每一个对象，则需要遍历(for)方式获得

  \- 举例说明：

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
   <ul class="nav">
     <li>测试1</li>
     <li>测试2</li>
     <li>测试3</li>
   </ul>
   <!-- id快速生成：标签#标签名 p#nav-->
    <script>
     // 依次改颜色 遍历   
     // 2.选择所有的小li
     const lis = document.querySelectorAll('.nav li')
    // console.log(lis)
    for (let i = 0; i < lis.length; i++) {
      console.log(lis[i]) //  每一个小li对象
    }         
    </script>
  </body>
  </html>
  ```

  

  >**注意**：哪怕**只有一个元素**，通过`querySelectorAll()`获取过来的也是一个`伪数组`，里面只有一个元素而已(也不能直接改样式)

  \- 举例说明：

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
   <ul class="nav">
     <li>测试1</li>
     <li>测试2</li>
     <li>测试3</li>
   </ul>
   <!-- id快速生成：标签#标签名 p#nav-->
   <script>
     // 依次改颜色 遍历   
     // 2.选择所有的小li
     const lis = document.querySelectorAll('.nav li')
    // console.log(lis)
    for (let i = 0; i < lis.length; i++) {
      console.log(lis[i]) //  每一个小li对象
    }  
     const p = document.querySelectorAll('#nav')
     console.log(p) // NodeList [p#nav]
   </script>
  </body>
  </html>
  ```

  

  > 只有一个元素的情况下,可以用p[0] `数组中的第一个元素`

  ```javascript
    const p = document.querySelectorAll('#nav')
    p[0].style.color = 'red'
  ```





### 其他获取DOM元素方法(了解)

<img src="http://images.newstar.net.cn/sally-imgs/image-20230924200036046.png " alt="image-20230924200036046"  /> 

> 解析：
>
> 1. getElementBId 专门获取元素类型节点，根据标签的`id`属性查找，这里已经通过id来获取，所以括号里不用加#，Element为元素
> 2. getElementByTagName等同于标签选择器，获取页面所有div，伪数组
> 3. getElementByClassName类名可多次使用，获取页面所有类名为w的，伪数组





## 操作元素内容

目标：能够修改元素的文本更换内容

1. DOM对象都是根据标签生成的,所以**操作标签**,**本质上就是操作DOM对象**

2. 操作元素内容 就是操作对象使用的点语法

3. 如果想要**修改标签元素**的里面的`内容`，可使用如下方式：

   * 对象.innerText (属性)  
   * 对象.innerHTML (属性)






### 对象.innerText

* innerText属性只显示纯文本，`不解析标签`
* 将文本内容添加/更新到任意标签位置

```javascript
<div class="box">我是文字的内容</div>
<script> 
// 1. 获取元素
const box = document.querySelector('.box')
// 2.修改文字内容 对象.innerText 属性
console.log(box.innerText) // 获取文字内容
box.innerText = '我是一个盒子' //修改文字内容,内容更改 对象.属性

// box.innerText = `<strong>我要更换内容</strong>``
// 文字未加粗，只解析文本
</script>
```

> 解析：box是个对象，对象有属性和方法，直接log打印是通过js获取文字内容 即打印输出，所以修改文字内容用对象.属性

\- 举例说明：

```javascript
<div class="box">我是文字的内容</div>
<script>
const obj = {
name: '老师'
}
console.log(obj.name) //对象的属性就是获取
//修改内容
obj.name = '张老师'
console.log(obj) 
</script>
```





### 对象.innerHTML（建议用）

* 将文本内容添加(更新)到任意标签位置
* innerHTML属性，`会解析标签`，**多标签**建议使**用模板字符串**

```javascript
<div class="box">我是文字的内容</div>
<script>
const box = document.querySelector('.box')
// 3.修改内容 解析标签 innerHTML
console.log(box.innerHTML)
// box.innerHTML = '更换内容'
box.innerHTML = `<strong>更换内容</strong>`// 文字加粗
</script>
```



> **注**：如果分不清哪个是否解析，纠结到底用谁，可以选择innerHTML（不写多个标签就行了）





## 操作元素属性

### 操作元素常用属性

1. 还可以**通过JS设置/修改** 标签**常用元素属性**，比如通过 src更换 图片

2. 最常见的属性比如： href、title、src 等

* 语法：

```javascript
对象.属性 = 值
```

```javascript
<img src="../images/hero/1.webp" alt="" />
<a href="https://www.sina.com.cn/" class="">跳转</a>
<script>
// 1.获取图片元素
const pic = document.querySelector('img')

// 3. 获取链接元素
const a = document.querySelector('a')
// 2.修改图片对象的属性
pic.src = '../images/hero/10.webp'
pic.title = '夏洛特'

// 4.修改链接的属性
a.href = 'https://onestar.love/'
</script>
```

> **注：**对象.属性 = '新值'






### 操作元素样式属性

1. 还可以通过 JS 设置/修改标签元素的样式属性
   * 比如通过 轮播图小圆点自动更换颜色样式
   * 点击按钮可以滚动图片，这是移动的图片的位置 left 等等

2. 通过以下几种方式操作属性：
   * 通过style属性 操作CSS(修改样式)
   * 操作类名(className) 操作CSS
   * 通过classList操作类控制CSS(重点)



#### 通过style属性 操作CSS(重点)

* 修改少量样式较有优势

* 语法：

```javascript
  对象.style.样式属性 = 值 
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
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
  // 如果样式属性是-连接的单词 采取小驼峰命名法
  box.style.backgroundColor = 'hotpink'
  box.style.border = '2px solid gray'
  box.style.borderTop = '2px solid green'
</script>
</body>
</html>

```

> **注：**
>
> 1. 修改样式通过`style`属性引出(任何标签都有`style`属性，通过`style`属性可以动态更改网页标签的样式
> 2. 若`CSS`属性有`-连接符`，单词转为`小驼峰`命名法
>    * 例如：background-color ———— backgroundColor 
> 3. 赋值的时候，需要的时候不要忘记加`CSS单位` (样式属性，大部分数字后都要加单位)
> 4. 生成的是行内样式，权重比较高(想在CSS里调样式得加!import)



#### 操作类名(className) 操作CSS

1. 如果修改的样式比较多，直接通过style属性较繁琐，采取CSS类名形式
2. 可以同时修改多个样式。即修改大量样式更方便，但多个类名操作较麻烦

* 语法：

```javascript
// active 是一个CSS类名
元素.className = 'active'
```

> **注：**
>
> 1. **class是关键字，所以使用className代替**,*属性虽然写的是className但解析时还是class*
> 2. className是使用**新值`换`旧值**(会覆盖之前的类名)，如果添加一个类,需要保留之前的类名
> 3. 但是多个类名操作比较麻烦

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Document</title>
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
  div.className = 'nav box'
</script>
</body>
</html>

```



#### classList操作类控制CSS(重点)

1. 为了**解决className**容易**覆盖**以前的**类名**，我们可以通过**classList方式追加和删除类名**
2. 修改大量样式更方便且`classList追加和删除不影响以前的类名`
3. 三个方法：add() remove() toggle()

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
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Document</title>
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
<div class="box active">文字</div>
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
</html>

```

  > **注：**
  >
  > 1. 追加类 add()类名不加点，并且是字符串
  > 2. 删除类 remove()类名不加点，并且是字符串
  > 3. 切换类 toggle(),查看有无类名，有就删掉，没有就加上
  > 4. 三个方法，注意加()
  > 5. 三者都不影响以前的类名





### 操作表单元素属性

1. 表单很多情况，也需要修改属性，比如点击眼睛，可以看到密码，本质是把表单类型转换为文本框

2. 正常的有属性有取值的 跟其他的标签属性没有任何区别


   * 获取: DOM对象.属性名

   * 设置/修改: DOM对象.属性名 = 新值

   ```html
<input type="text" value="电脑" />
<button>点击</button>
<!--disabled="disabled"属性值一模一样只需要写一个 -->
<script>
// 1.获取元素
const uname = document.querySelector('input')
// 2.获取值 获取表单里面的值 用的 表单.value
// console.log(uname.value) // 电脑
// console.log(uname.innerHTML) // innerHTML仅限于普通元素，得不到表单元素
// 3.设置表单的值
// uname.value = '我要买电脑'
// console.log(uname.type)
uname.type = 'password'
</script>
   ```

   > **注：**
   >
   > * innerHTML可以得到元素内容，但仅限于普通元素，得不到表单元素，想要表单元素只有value
   > * **但button**为双标签，比较特殊，需使**用innerHTML**





3. 表单属性中添加就有效果,移除就没有效果，一律使用**布尔值**表示。若为true，代表添加了该属性;若为false，代表移除了该属性

* 比如： **disabled、checked**、selected

![image-20231003211733950](http://images.newstar.net.cn/sally-imgs/image-20231003211733950.png)



```html
<!DOCTYPE html>
<html lang="en">

<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0" />
<title>Document</title>
</head>

<body>
<!-- <input type="text" value="电脑" /> -->
<input type="checkbox" name="" id="" />
<button>点击</button>
<!--disabled="disabled"属性值一模一样只需要写一个 -->
<script>
// // 1.获取元素
// const uname = document.querySelector('input')
// // 2.获取值 获取表单里面的值 用的 表单.value
// // console.log(uname.value) // 电脑
// // console.log(uname.innerHTML) // innerHTML仅限于普通元素，得不到表单元素
// // 3.设置表单的值
// // uname.value = '我要买电脑'
// // console.log(uname.type)
// uname.type = 'password'

// 1.获取
const ipt = document.querySelector('input')
// console.log(ipt.checked) // false 只接受布尔值
ipt.checked = true
// ipt.checked = 'true' //会选中，不提倡 有隐式转换

const button = document.querySelector('button')
// console.log(button.disabled) // 默认false 不禁用
button.disabled = true // 禁用按钮
</script>
</body>

</html>
```

> **注：**
>
> 1. `disabled、checked常用`，是否禁用和勾选，一律使用**布尔值**表示
>
>   * checked = true (勾选)
>   * disabled = true (禁用)
>
> 2. selected下拉菜单很少用到，disabled、checked





### 自定义属性

1. 标准属性: 标签天生自带的属性 比如class id title等, 可以直接使用点语法操作比如： disabled、checked、selected

2. 自定义属性：

   * 在html5中推出来了专门的data-自定义属性

   * 在**标签上**一律以`data-`**开头**

   * 在**DOM对象上**一律以`dataset对象`方式**获取**

     ![image-20231003214311902](http://images.newstar.net.cn/sally-imgs/image-20231003214311902.png)

     ```html
     <!DOCTYPE html>
     <html lang="en">
       <head>
         <meta charset="UTF-8" />
         <meta name="viewport" content="width=device-width, initial-scale=1.0" />
         <title>Document</title>
       </head>
       <body>
         <div data-id="1" data-spm="不知道">1</div>
         <div data-id="2">2</div>
         <div data-id="3">3</div>
         <div data-id="4">4</div>
         <div data-id="5">5</div>
         <script>
           const one = document.querySelector('div')
           console.log(one.dataset.id) // 结果为1，dataset对象集合
           console.log(one.dataset.spm) // 结果为 不知道
         </script>
       </body>
     </html>
     
     ```

     

#### 自定义属性-知识点补充

* 没有序号，如何选出div

  ```javascript
  <div data-id="0"></div>
  <script>
    const div = document.querySelector('div')
    console.log(div.dataset.id) // 拿到0
  </script>
  ```

  

#### 属性选择器-知识点补充

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
     /* 带中括号的为属性选择器，根据属性来选择 */
    /* 选择input，他有一个属性为value */
    /* input[value] {
      color: red;
    } */
      
    /*input两个都有type，但是值不同 */
    input[type=text] {
      color: red;
    }
  </style>
</head>

<body>
  <input type="text" value="123" data-id="0" data-name="andy">
  <input type="password">
  <script>
    const input = document.querySelector('input[value]')
    // console.log(input)
    console.log(input.dataset) // 自定义属性集合
    console.log(input.dataset.name) // 自定义属性集合
  </script>
</body>

</html>
```

> **分析：**
>
> 1. `属性选择器用中括号[]代替,根据属性来选择`
> 2. input[value]， 选择input，他有一个属性为value
> 3. input[type=text]， input 两个都有type，但是值不同 





## 定时器

1. 网页中经常会需要一种功能：每隔一段时间需要**自动**执行一段代码，不需要我们手动去触发

   例如：网页中的倒计时，要实现这种需求，需要**定时器函数**

2. 目标：能够使用**定时器**函数**重复执行**代码

3. 定时器函数有两种：**间歇**函数**setInterval**、 **延时**函数**setTimeout**

4. **作用：**可以根据时间**自动重复执行**某些代码





### 定时器-间歇函数

* 定时器函数可以开启和关闭定时器
* 目标：知道间歇函数的作用，利用间歇函数创建定时任务。

#### 开启定时器

* 语法：

  ```javascript
  setInterval(函数, 间隔时间)
  ```

  > `setInterval` 是 JavaScript 中内置的函数，它的作用是间隔固定的时间自动重复执行另一个函数，也叫定时器函数。

* 作用：每隔一段时间调用前面这个函数（**间隔时间单位是毫秒**）

  ```javascript
  <script>
  // 开启定时器 
  // 写法1：匿名函数写法：setInterval(函数, 毫秒)
  // setInterval(function () {
  //   console.log('一秒执行一次')
  // }, 1000)
  
  // 写法2：具名函数写法：setInterval(函数名, 间隔时间) 函数名不加小括号
  // setInterval(fn, 3000)
  function fn() {
    console.log('三秒执行一次')
  }
  let n = setInterval(fn, 3000) // 每间隔3秒执行一次
  console.log(n) // 序号为2
  
  // 写法3：
  // setInterval('fn()', 1000) 极为少见的写法
  </script>
  ```

  **注：**`函数名不需要加括号`

  

  > **注**定时器返回的是一个id数字**(也就是一个序号，页面中有几个定时器开，就有几个序号排列。每个定时器都有独一无二的的序号)

  \- 举例说明：

  ```javascript
function fn() {
    console.log('三秒执行一次')
  }
  
  // 使用 setInterval 调用 fn 函数,重复调用fn
  let n = setInterval(fn, 3000) 
  console.log(n) // 序号为2
  
  
  let m = setInterval(function () {
    console.log(11)
  }, 1000)
  console.log(m) // 序号为3
  ```
  
  > **注：**`此处用let声明，因为定时器要开要关，返回的值是数字型，里面的值会有变化，后面有重新赋值操作`



#### 关闭定时器

* 语法：

  ```javascript
  let 变量名 = setInterval(函数, 间隔时间)
  clearInterval(变量名)
  ```

  > **注：**
  >
  > 1. 一般不会刚创建就停止，而是满足一定条件再停止
  > 2. 函数名**不加括号**
  > 3. 关闭定时器必须有变量名

  \- 举例说明：

  ```javascript
  function timer() {
    console.log('一秒执行一次')
  }
  let n = setInterval(timer, 1000)
  clearInterval(n) // 关闭定时器 
  ```

  

