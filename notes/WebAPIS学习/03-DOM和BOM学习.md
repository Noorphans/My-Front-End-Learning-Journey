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

* innerText属性，会解析标签，**多标签**建议使**用模板字符串**

  



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

  > **注：**innerHTML可以得到元素内容，但仅限于普通元素，得不到表单元素，想要表单元素只有value







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

  * 在标签上一律**以data-开头**

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

  