# Dom事件基础

[toc]



## 事件监听(绑定)

目标：能够给DOM元素添加事件监听

1. 事件：是在编程时系统内部发生的**动作**或者发生的事情

   * 比如用户在网页上**鼠标单击**一个按钮
   * 用户使用【鼠标拖拽】网页中的一张图片

2. 事件监听：也称为**绑定事件**或**注册事件**，是让程序员检测是否有事件产生，一旦**有事件触发**，**就立即调用**一个函数**做出响应**

   * 比如鼠标经过显示下拉菜单
   * 比如点击可以播放轮播图等

3. 语法：

   ```javascript
   元素对象.addEventListener('事件类型', 要执行的函数)
   ```

   > **注：**
   >
   > * `addEventListener` 是 DOM 对象专门用来添加事件监听的方法
   > * 要执行的函数 又叫 事件调用的函数、事件回调和回调函数，`这个函数不是立马执行的`，它一旦绑用之后不是立即执行，而是`等待事件触发`,事件什么时候触发什么时候执行（比如绑定一个点击事件，它不会立马弹出一个对话框，而是啥时点了按钮即**事件源**才会弹出里面执行的函数）

   

   \- 举例说明：

   ```javascript
   <button>点击</button>
   <script>
   //  点击按钮，弹出对话框
   // 1.事件源 按钮
   // 2.事件类型 鼠标点击
   // 3.事件处理程序 弹出对话框
   const btn = document.querySelector('button')
   btn.addEventListener('click', function () {
     alert('点击了')
   })
   </script>
   ```

   **注：**`事件类型要加引号，要执行的函数是点击之后再去执行，每次点击都会执行一次`

   

4. 完成事件监听分成3个步骤：

   * 获取 DOM 元素
   * 通过 `addEventListener` 方法为 DOM 节点添加事件监听 并 等待事件触发，如用户点击了某个按钮时便会触发 `click` 事件类型
   * 事件触发后，相对应的回调函数会被执行

   

5. `事件监听三要素：`

   * **事件源：**哪个dom元素被事件触发了，要获取dom元素

     \- 通俗理解：张老师点到陈同学，给陈同学添加了绑定事件，点了陈同学的名字。事件源就是陈同学，因为是他被监听了

     ​		  平时我们说的事件源就叫做元素对象，可能是个按钮，也可能是个盒子

     

   * **事件类型：**用什么方式触发，比如鼠标单击click、鼠标经过mouseover、按键盘等 

     \- 举例说明：

     `click` 译成中文是【点击】的意思，它的含义是监听（等着）用户鼠标的单击操作，除了【单击】还有【双击】`dblclick`

     ```javascript
     <script>
       // 双击事件类型
       btn.addEventListener('dblclick', function () {
         console.log('等待事件被触发...');
         // 改变 p 标签的文字颜色
         const text = document.querySelector('.text')
         text.style.color = 'red'
       })
     
       // 只要用户双击击了按钮，事件便触发了！！！
     </script>
     ```

     结论：【事件类型】决定了事件被触发的方式，如 `click` 代表鼠标单击，`dblclick` 代表鼠标双击。

     

   * **事件调用的函数**:又称事件处理程序 即要做什么事

     \- 通俗理解：张老师给陈同学添加事件监听，肯定是要陈同学做某件事，到底要干什么事，要干的事写到此函数里

     

     \- 举例说明：

     `addEventListener` 的第2个参数是函数，这个函数会在事件被触发时立即被调用，在这个函数中可以编写任意逻辑的代码，如改变 DOM 文本颜色、文本内容等。

     ```javascript
     <script>
       // 双击事件类型
       btn.addEventListener('dblclick', function () {
         console.log('等待事件被触发...')
         
         const text = document.querySelector('.text')
         // 改变 p 标签的文字颜色
         text.style.color = 'red'
         // 改变 p 标签的文本内容
         text.style.fontSize = '20px'
       })
     </script>
     ```
     
     结论：【事件处理程序】决定了事件触发后应该执行的逻辑。

   

   



## 解惑-事件监听之const声明

* 用const声明的变量不是不允许多次赋值和声明吗？那为什么可以在事件监听的函数里面写const呢，那每次点击不就相当于多了一个const num，那这样不会导致冲突吗？

```javascript
<button>点击</button>
<script>
// const num = 10 
// 外面和里面都声明一个const，不会报错，不冲突，因为里面的是在函数内部，属于局部作用域
// 但如果删除函数内部的const，只留外部的const，这是num就是全局变量 被重新赋值，会报错
const btn = document.querySelector('button')
btn.addEventListener('click', function () {
  const num = Math.random()
  // num = 10 // 上面用const，再重写给个值这么写就是错的，常量不允许再次赋值
  console.log(num)
})
</script>
```

> 解析：
>
> 1. 这里的const再次声明使用，用到了垃圾回收机制，即如果在一个函数里的这个变量，当我们执行完这个函数，这个变量不再使用，它会进行销毁回收
> 2. 如这里是 当我给按钮做了一次点击事件，函数执行完了，执行完了const声明的num没有用了，这时就用到JS中的垃圾回收机制，相当于把 const num = Math.random()和console.log(num)这两句话删除了，而再次点击就会创建一个新的num变量，就不会冲突报错了





## 拓展-事件监听的版本

### DOM L0 

* DOM LO：是最早级别，事件监听的第一个版本，写法是on事件（L的全称是Level，级别的意思）

  

* 语法：

  ```javascript
  事件源.on事件 = function() { }
  ```

\- 举例说明：

  ```javascript
<button>点击</button>
<script>
  const btn = document.querySelector('button')
  btn.onclick = function () {
    alert(11)
  }
  btn.onclick = function () {
    alert(22)
  } // 结果被后者22覆盖

  // 相当于赋值的方式
  // let num = 10
  // num =20
</script>
  ```

> **注：**
>
> 1. 同一个事件，`on方式会被覆盖`，等同于**赋值**的方式
>
> 2. 只有冒泡，没有捕获且`只能做冒泡`





### DOM L2(推荐使用)

* DOM L2：第三个版本，使用addEventListener注册事件。

  

* 语法：

  ```javascript
  事件源.addEventListener(事件， 事件处理函数)
  ```

\- 举例说明：

```javascript
<script>
  const btn = document.querySelector('button')

  btn.addEventListener('click', function () {
    alert(11)
  })
  btn.addEventListener('click', function () {
    alert(22)
  }) // 11和22不会被覆盖
</script>
```

> **注：**
>
> 1. 同一件事，不会出现覆盖情况
> 2. 可以冒泡和捕获
> 3. addEventListener方式可绑定多次，拥有事件更多特性，`推荐使用`



* DOM L1：是第二个版本，DOM级别1于1998年10月1日成为W3C推荐标准；
* DOM L3：是第四个版本，DOM3级事件模块在DOM2级事件的基础上重新定义了这些事件，也添加了一些新事件类型）





### 总结-L0和L2注册(绑定)事件的区别

#### 传统on注册(L0)

1. 语法：事件源.on事件 = function() { }
2. 同一个对象,后面注册的事件会覆盖前面注册(同一个事件)
3. 直接使用null覆盖偶就可以实现事件的解绑
4. 都是冒泡阶段执行的



#### 事件监听注册（L2）

1. 语法: addEventListener(事件类型, 事件处理函数, 是否使用捕获)
2. 后面注册的事件不会覆盖前面注册的事件(同一个事件)
3. 可以通过第三个参数去确定是在冒泡或者捕获阶段执行
4. 必须使用removeEventListener(事件类型, 事件处理函数, 获取捕获或者冒泡阶段)
5. 匿名函数无法被解绑





## 事件类型

将众多的事件类型分类可分为：鼠标事件、键盘事件、表单事件、焦点事件等





### 鼠标事件(鼠标触发)

鼠标事件是指跟鼠标操作相关的事件，如单击、双击、移动等。

1. click 鼠标点击
2. `mouseenter` ； mouseover  鼠标经过 



\- 举例说明1：mouseenter 监听鼠标是否移入 DOM 元素

```javascript
<body>
  <h3>鼠标事件</h3>
  <p>监听与鼠标相关的操作</p>
  <hr>
  <div class="box"></div>
  <script>
    // 需要事件监听的 DOM 元素
    const box = document.querySelector('.box');

    // 监听鼠标是移入当前 DOM 元素
    box.addEventListener('mouseenter', function () {
      // 修改文本内容
      this.innerText = '鼠标移入了...';
      // 修改光标的风格
      this.style.cursor = 'move';
    })
  </script>
</body>
```

\- 举例说明2：

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
  </script>
</body>

</html>
```



3. `mouseleave` ； mouseout   鼠标离开

\- 举例说明1：mouseleave 监听鼠标是否移出 DOM 元素

```javascript
<body>
  <h3>鼠标事件</h3>
  <p>监听与鼠标相关的操作</p>
  <hr>
  <div class="box"></div>
  <script>
    // 需要事件监听的 DOM 元素
    const box = document.querySelector('.box');

    // 监听鼠标是移出当前 DOM 元素
    box.addEventListener('mouseleave', function () {
      // 修改文本内容
      this.innerText = '鼠标移出了...';
    })
  </script>
</body>
```

\- 举例说明2：

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
      background-color: pink;
    }
  </style>
</head>

<body>
  <div></div>
  <script>
    const div = document.querySelector('div')
    // 鼠标离开
    div.addEventListener('mouseleave', function () {
      console.log('我走了')
    })
  </script>
</body>

</html>
```



#### 总结-鼠标经过&离开事件的区别

1. 鼠标经过`mouseenter` 和 鼠标离开`mouseleave` **没有冒泡效果 (推荐)**

   

2. 鼠标经过mouseover 和 鼠标离开mouseout 会有冒泡效果

\- 举例说明:

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
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
      // dad.addEventListener('mouseover', function () {
      //   console.log('鼠标经过') // 有冒泡效果
      // })
      // dad.addEventListener('mouseout', function () {
      //   console.log('鼠标离开') // 有冒泡效果
      // })
      dad.addEventListener('mouseenter', function () {
        console.log('鼠标经过') // 没有冒泡效果
      })
      dad.addEventListener('mouseleave', function () {
        console.log('鼠标经过') // 没有冒泡效果
      })
    </script>
  </body>
</html>

```





### 焦点事件(表单获得光标)

#### focus

* focus 获得焦点

  ```javascript
  <input type="text" />
  <script>
    const input = document.querySelector('input')
    input.addEventListener('focus', function () {
      console.log('有焦点触发')
    })
  </script>
  ```



#### blur

* blur 失去焦点

  ```javascript
  <input type="text" />
  <script>
    const input = document.querySelector('input')
    input.addEventListener('blur', function () {
      console.log('失去焦点触发')
    })
  </script>
  ```

  



### 键盘事件(键盘触发)

#### Keydown

* Keydown 键盘按下触发

  ```javascript
  <input type="text" />
  <script>
    const input = document.querySelector('input')
    // 1. 键盘事件
    input.addEventListener('keydown', function () {
      console.log('键盘按下了')
    })
  </script>
  ```

  

#### Keyup(建议常用)

* Keyup 键盘抬起触发 

  ```javascript
  <input type="text" />
  <script>
    const input = document.querySelector('input')
    // 1. 键盘事件
    input.addEventListener('keyup', function () {
      console.log('键盘弹起了')
    })
  </script>
  ```






### 文本框输入事件（表单输入触发）

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

任意事件类型被触发时与事件相关的信息会被以对象的形式记录下来，我们称这个对象为事件对象

1. 事件对象：也是个对象，这个对象里有事件触发时的相关信息(存储了事件的相关信息)

   \- 例如：鼠标点击事件中，事件对象就存了鼠标点在哪个位置等信息

2. 使用场景：
   * 可以判断用户按下哪个键，比如按下回车键可以发布新闻
   * 可以判断鼠标点击了哪个元素，从而做相应的操作





### 获取事件对象(重点)

1. 事件对象在哪里？
   * 在事件绑定的回调函数的【第1个参数】就是<u>事件对象</u>，一般将这个对数命名为`event、ev、e`

2.语法：

```javascript
元素.addEventListener('click', function(e){
    
}) // e为事件对象
```

\- 举例说明：

```javascript
<button>点击</button>
<input type="text" />
<script>
    // 获取 button 元素
    const btn = document.querySelector('button')
    // 添加事件监听
    btn.addEventListener('click', function (e) {
    // 事件回调函数的第1个参数即所谓的事件对象
      console.log(e)
    })
</script>
```





### 事件对象常用属性

* 部分常用属性

  1. `ev.type` 当前事件的类型
  2. `ev.clientX/clientY` 光标相对于浏览器可见窗口左上角的位置 
  3. `ev.offsetX/offsetY` 光标相对于当前 DOM 元素左上角的位置
  4. `ev.key` 用户按下的键盘键的值（现在不提倡使用keyCode）

  ```javascript
  <input type="text" />
  <script>
      // 获取 input 元素
      const input = document.querySelector('input')
      // 添加事件监听
      input.addEventListener('keyup', function (e) {
        // console.log(11)
        // console.log(e.key)
        if (e.key === 'Enter') {
          console.log('我按下了回车键')
        }
      })
  </script>
  ```

  

  > 注：在事件回调函数内部通过 window.event 同样可以获取事件对象。





## 环境对象

1. 目标：能够分析判断函数运行在不同环境中 this 所指代的对象

2. **环境对象：**指的是 函数内部特殊的`变量this`，this它代表着当前函数运行时所处的环境

3. **作用：**弄清this指向，让代码更简洁

   \- 举例说明1：

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
     console.log(this) // btn调用的 对象就是btn，this指向的是函数的调用者，谁调用，就指向谁
     // btn.style.color = 'red'
     this.style.color = 'red'
   })
   </script>
   ```

   > **结论：**
   >
   > 1. 函数的调用方式不同，`this` 指代的对象也不同
   > 2. `【谁调用， this 就是谁】` 是判断this指向的粗略规则
   > 3. 直接调用函数，其实相当于是 `window.函数`，所以`this`指代 `window`
   > 4. `this` 本质上是一个变量，数据类型为对象

   \- 举例说明2：

   ```javascript
   <script>
     // 声明函数
     function sayHi() {
       // this 是一个变量
       console.log(this);
     }
   
     // 声明一个对象
     let user = {
       name: '张三',
       sayHi: sayHi // 此处把 sayHi 函数，赋值给 sayHi 属性
     }
     
     let person = {
       name: '李四',
       sayHi: sayHi
     }
   
     // 直接调用
     sayHi() // window
     window.sayHi() // window
   
     // 做为对象方法调用
     user.sayHi()// user
   	person.sayHi()// person
   </script>
   ```

   函数直接调用时实际上 `window.sayHi()` 所以 `this` 的值为 `window`





## 回调函数

如果将函数 A 做为参数传递给函数 B 时,即当一个函数当做`参数`来传递给`另一个函数`的时候，我们称函数 A 为`回调函数`。

\- 举例说明1：

```javascript
<script>
function fn() {
  console.log('我是回调函数')
}
// fn作为参数传递给了setInterval，fn就是回调函数
setInterval(fn, 1000)

// box.addEventListener('click', function () {
//   console.log('我也是回调函数')
// })
</script>
```

\- 举例说明2：

```javascript
<script>
  // 声明 foo 函数
  function foo(arg) {
    console.log(arg);
  }

  // 普通的值做为参数
  foo(10);
  foo('hello world!');
  foo(['html', 'css', 'javascript']);

  function bar() {
    console.log('函数也能当参数...');
  }
  // 函数也可以做为参数！！！！
  foo(bar);
</script>
```

函数 `bar` 做参数传给了 `foo` 函数，`bar` 就是所谓的回调函数了！！！



> **注：**
>
> 1. 把函数当做另外一个函数的参数传递，这个函数就叫`回调函数`
> 2. 回调函数`本质`还是`函数`，只不过把它当成`参数`使用
> 3. 使用`匿名函数作为回调函数较常见`
> 4. 回调函数不会立马执行，时机成熟才调用

