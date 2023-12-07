# Dom事件进阶

[toc]



## 事件流

### 事件流和两个阶段说明

#### 事件流

1. 事件流：

* 是对事件执行过程的描述，了解事件的执行过程有助于加深对事件的理解，提升开发实践中对事件运用的灵活度。

* 是指`事件`完整执行过程中的`流动`路径（事件捕获-事件目标阶段-事件冒泡）

![event](http://images.newstar.net.cn/sally-imgsevent.png)

2. 说明：如上图所示，任意事件被触发时总会经历两个阶段：【捕获阶段】和【冒泡阶段】（假设页面里有个div，当触发事件时，会经历这两个阶段）

3. 简单理解：
   * `捕获`阶段是**从父到子**(从大到小)的传导过程，`冒泡`阶段是**从子向父**(从小到大)的传导过程。



> 注：**实际工作都是使用事件冒泡为主**



\- 举例说明：事件流如何影响事件执行

```html
<body>
  <h3>事件流</h3>
  <p>事件流是事件在执行时的底层机制，主要体现在父子盒子之间事件的执行上。</p>
  <div class="outer">
    <div class="inner">
      <div class="child"></div>
    </div>
  </div>
  <script>
    // 获取嵌套的3个节点
    const outer = document.querySelector('.outer');
    const inner = document.querySelector('.inner');
    const child = document.querySelector('.child');
		
    // html 元素添加事件
    document.documentElement.addEventListener('click', function () {
      console.log('html...')
    })
		
    // body 元素添加事件
    document.body.addEventListener('click', function () {
      console.log('body...')
    })

    // 外层的盒子添加事件
    outer.addEventListener('click', function () {
      console.log('outer...')
    })
    
    // 中间的盒子添加事件
    outer.addEventListener('click', function () {
      console.log('inner...')
    })
    
    // 内层的盒子添加事件
    outer.addEventListener('click', function () {
      console.log('child...')
    })
  </script>
</body>
```

> 解析：
>
> * 执行上述代码后发现当单击事件触发时，其祖先元素的单击事件也【相继触发】
>
> * 我们知道当某个元素的事件被触发时，事件总是会先经过其祖先才能到达当前元素，然后再由当前元素向祖先传递，事件在流动的过程中遇到相同的事件便会被触发。



4. 事件相继触发的【执行顺序】：事件的执行顺序是`可控制`的，即可以在捕获阶段被执行，也可以在冒泡阶段被执行



#### 事件捕获阶段(了解)

事件是在捕获阶段执行的，我们称为捕获模式，它会先执行`父盒子`事件再去执行子盒子事件。

1. **事件捕获概念：**从DOM的根元素开始去执行对应的事件 (从外到里)

2. 事件捕获需要写对应代码才能看到效果

   * 代码：

   ```javascript
   DOM.addEventListener(事件流，时间处理函数，是否使用捕获机制)
   ```

   >**注：**
   >
   >1. `addEventListener` 第3个参数决定了事件是在捕获阶段触发还是在冒泡阶段触发
   >2. `addEventListener` 第3个参数为 `true` 表示捕获阶段触发（很少使用）；若为`false`表示冒泡阶段触发，默认值为 `false`
   >3. 若是用 L0 事件监听，则只有冒泡阶段，没有捕获

   \- 举例说明：

   ```javascript
   <body>
     <h3>事件流</h3>
     <p>事件流是事件在执行时的底层机制，主要体现在父子盒子之间事件的执行上。</p>
     <div class="outer">
       <div class="inner"></div>
     </div>
     <script>
       // 获取嵌套的3个节点
       const outer = document.querySelector('.outer')
       const inner = document.querySelector('.inner')
   
       // 外层的盒子
       outer.addEventListener('click', function () {
         console.log('outer...')
       }, true) // true 表示在捕获阶段执行事件
       
       // 中间的盒子
       outer.addEventListener('click', function () {
         console.log('inner...')
       }, true)
     </script>
   </body>
   ```



#### 事件冒泡阶段（重点）

事件是在冒泡阶段执行的，我们称为冒泡模式，它会先执行`子盒子`事件再去执行父盒子事件，默认是冒泡模式。

1. **事件冒泡概念:** 当一个元素的事件被触发时，同样的事件将会在该元素的所有祖先元素中依次被触发。这一过程被称为事件冒泡
2. 简单理解：当一个元素触发事件后，会依次向上调用所有父级元素的`同名事件`(同种类型事件)

\- 举例说明：

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Document</title>
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
    document.addEventListener('click', function () {
      alert('我是爷爷')
    })
    fa.addEventListener('click', function () {
      alert('我是爸爸')
    })
    son.addEventListener('click', function () {
      alert('我是儿子')
    })
  </script>
</body>

</html>
```



> **注：**
>
> 1. 事件冒泡是默认存在的
> 2. 事件流只会在父子元素具有相同事件类型时才会产生影响
> 3. 绝大部分场景都采用默认的冒泡模式（其中一个原因是早期 IE 不支持捕获）
> 4. L2事件监听第三个参数若为 false或者默认都是冒泡



##### 阻止冒泡

1. 阻止冒泡：是指阻断事件的流动，保证事件只在当前元素被执行，而不再去影响到其对应的祖先元素。

2. **问题：**因为默认就有冒泡模式的存在，所以容易导致事件影响到父级元素

3. **需求：**若想把事件就限制在当前元素内，就需要阻止事件冒泡

4. **前提：**阻止事件冒泡需要拿到事件对象

5. **语法**:

   ```javascript
    事件对象.stopPropagation()
   ```

   > **注：** 此方法专门用来阻断事件冒泡(事件流动传播)，不光在冒泡阶段有效，捕获阶段也有效

   

   \- 举例说明：

   ```html
   <!DOCTYPE html>
   <html lang="en">
   
   <head>
     <meta charset="UTF-8" />
     <meta name="viewport" content="width=device-width, initial-scale=1.0" />
     <title>Document</title>
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
     </script>
   </body>
   
   </html>
   ```

   > **结论：**
   >
   > 1. 先要明确哪一块区域不能冒泡
   > 2. 需要阻止什么事件传递就给这块区域最大盒子注册该事件
   > 3. 在事件处理函数里面接受事件对象，并添加上e.stopPropagation()



##### 阻止元素默认行为

* 我们某些情况下需要阻止默认行为的发生，比如 阻止 链接的跳转，表单域跳转

* 语法：

  ```javascript
  e.preventDefault()
  ```



\- 举例说明：

```javascript
<form action="http://www.itcast.cn">
<input type="submit" value="免费注册" />
</form>
<a href="http://www.baidu.com">百度一下</a>
<script>
const form = document.querySelector('form')
form.addEventListener('submit', function (e) {
  // 阻止默认行为  提交
  e.preventDefault()
})

// 阻止链接跳转
const a = document.querySelector('a')
a.addEventListener('click', function (e) {
  e.preventDefault()
})
</script>
```



##### 事件冒泡的必要性

`如果没有冒泡，给大盒子注册点击事件，点击的是里面的小盒子，会导致大盒子的点击无法执行`





### 解绑事件(了解)

#### on事件方式

* 直接使用`null`覆盖偶 就可以实现事件的解绑
* 语法：

```javascript
// 绑定事件
btn.onclick = function () {
    alert?('点击了')
}
// 解绑事件
btn.onclick = null
```



\- 举例说明：

```javascript
<button>点击</button>
<script>
const btn = document.querySelector('button')
// btn.onclick = function () {
//   alert('点击了')
//   // L0 传统方法onclick，事件移除解绑
//   btn.onclick = null
// }

function fn() {
  alert('点击了')
}
btn.addEventListener('click', fn)
// L2 事件移除解绑
btn.removeEventListener('click', fn)
</script>
```



#### addEventListener方式

* 必须使用`removeEventListener`(事件类型, 事件处理函数, [获取捕获或者冒泡阶段])

\- 举例说明：

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

1. 事件委托：是利用事件流的特征解决一些现实开发需求的知识`技巧`，主要的作用是提升程序效率。

2. 优点：减少注册次数，可以提高程序性能

3. 原理：事件委托其实是利用事件冒泡的特点(**自己不注册事件，将对应事件注册给祖先元素**)

   * (委托给父元素)给`父元素注册事件`，当我们触发子元素的时候，会冒泡到父元素身上，从而触发父元素的事件
   * ul.addEventListener('click' , function(){}) 执行父级点击事件

   ![image-20231128195941887](http://images.newstar.net.cn/sally-imgsimage-20231128195941887.png)

<img src="http://images.newstar.net.cn/sally-imgs/image-20231023142243502.png">

4. 图片分析：
   * 大的父元素ul 包含li子元素
   * 事件写到ul上，li则不添加事件，不需要循环
   * 给小li做点击事件，点击的是小li，没有监听事件，但事件本身有事件流，会冒泡，往ul父元素身上跑，ul有事件监听,所以会执行里面的代码

5. 代码实现：

```javascript
事件对象.target.tagName
```

> **注：**事件对象.target.tagName 可以获得真正触事件的元素



\- 举例说明：

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

**结论：**找到真正被触发的元素 `e.target`;如果要加判断条件 必须是当前某种元素的话加上`tagName`



6. 以往我们如果同时给多个元素注册事件，用 for循环注册事件(而事件委托 注册一次事件就能完成此效果)

\- 举例说明：大量的事件监听是比较耗费性能的

```javascript
<script>
  // 假设页面中有 10000 个 button 元素
  const buttons = document.querySelectorAll('table button');

  for(let i = 0; i <= buttons.length; i++) {
    // 为 10000 个 button 元素添加了事件
    buttons.addEventListener('click', function () {
      // 省略具体执行逻辑...
    })
  }
</script>
```



而利用事件流的特征，可以对上述的代码进行优化，事件的的冒泡模式总是会将事件流向其父元素的，如果父元素监听了相同的事件类型，那么父元素的事件就会被触发并执行，正是利用这一特征对上述代码进行优化，如下代码所示：

```javascript
<script>
  // 假设页面中有 10000 个 button 元素
  let buttons = document.querySelectorAll('table button');
  
  // 假设上述的 10000 个 buttom 元素共同的祖先元素是 table
  let parents = document.querySelector('table');
  parents.addEventListener('click', function () {
    console.log('点击任意子元素都会触发事件...');
  })
</script>
```

我们的最终目的是保证只有点击 button 子元素才去执行事件的回调函数，如何判断用户点击是哪一个子元素呢？

![event](http://images.newstar.net.cn/sally-imgsevent.png)



事件对象中的属性 `target` 或 `srcElement`属性表示真正触发事件的元素，它是一个元素类型的节点。

```javascript
<script>
  // 假设页面中有 10000 个 button 元素
  const buttons = document.querySelectorAll('table button')
  
  // 假设上述的 10000 个 buttom 元素共同的祖先元素是 table
  const parents = document.querySelector('table')
  parents.addEventListener('click', function (ev) {
    // console.log(ev.target);
    // 只有 button 元素才会真正去执行逻辑
    if(ev.target.tagName === 'BUTTON') {
      // 执行的逻辑
    }
  })
</script>
```

优化过的代码只对祖先元素添加事件监听，相比对 10000 个元素添加事件监听执行效率要高许多！





## 其他事件

### 页面加载事件

#### load事件

加载外部资源（如图片、外联CSS和JavaScript等）加载完毕时触发的事件

1. 为什么要学：

* 有些时候需要等页面资源全部处理完了做一些事情
* 老代码喜欢把script写在head中，这时候直接找dom元素找不到

2. **事件名：load**

3. 监听页面所有资源加载完毕：

   * 给window添加load事件

   ```javascript
    window.addEventListener('load',function(){
        // 执行的操作
    })
   ```

   > **注意：**不光可以监听整个页面资源加载完毕，也可以针对某个资源绑定load事件



\- 举例说明：

```javascript
  <script>
    // 1.老代码script写法
    /* const btn = document.querySelector('button')
    btn.addEventListener('click', function () {
      alert(11)  // 11弹不出来，不能读取该属性 为空，从上往下执行 代码抓不到btn
    }) */

    // 2.使用页面加载事件
    // 等待页面所有资源加载完毕，就回去执行回调函数
    // window.addEventListener('load', function () {
    //   const btn = document.querySelector('button')
    //   btn.addEventListener('click', function () {
    //     alert(11)
    //   })
    // })

     img.addEventListener('load', function () {
       // 等待图片加载完毕，再去执行里面的代码
     })
  </script>
</head>

<body>
  <button>点击</button>
</body>
```



#### DOMContentLoaded事件

当初始的HTML文档被完全加载和解析完成之后，DOMContentLoaded 事件被触发，而`无需等待样式表、图像等完全加载`,比页面加载事件执行速度更快

1. **事件名：DOMContentLoaded**

2. 监听页面DOM加载完毕：

   * 给document添加DOMContentLoaded事件

   ```javascript
   document.addEventListener('DOMContentLoaded',function(){
       // 执行的操作
     })
   ```



\- 举例说明：

```javascript
  <script>
    // DOMContentLoaded事件
    document.addEventListener('DOMContentLoaded', function () {
      const btn = document.querySelector('button')
      btn.addEventListener('click', function () {
        alert(11)
      })
    })
  </script>
</head>

<body>
  <button>点击</button>
</body>
```





### (页面)元素滚动事件

滚动条在滚动的时候持续触发的事件

1. 为什么要学:**很多网页需要检测用户把页面滚动到某个区域后做一些处理， 比如固定导航栏，比如返回顶部**

2. 事件名：scroll

3. 监听整个页面滚动：

   * **给window或document添加 scroll 事件**

   ```javascript
   window.addEventListener('scroll', function () {
       // 执行的操作
   })
   ```

   \- 举例说明：

   ```html
   <!DOCTYPE html>
   <html lang="en">
   
   <head>
     <meta charset="UTF-8" />
     <meta name="viewport" content="width=device-width, initial-scale=1.0" />
     <title>Document</title>
     <style>
       body {
         height: 3000px;
       }
     </style>
   </head>
   
   <body>
     <script>
       const div = document.querySelector('div')
       // 页面滚动事件
       window.addEventListener('scroll', function () {
          console.log('我滚了')
       })
     </script>
   </body>
   
   </html>
   ```



4. 监听某个元素的内部滚动直接给某个元素加即可





#### 页面滚动事件-获取位置

`scrollLeft和scrollTop （属性）`

1. scrollLeft被卷去的左侧;scrollTop被卷去的头部

   * 获取被卷去的大小

   * 获取元素内容往左、往上滚出去看不到的距离

   * 这两个值是可`读写`的，可以读取，也可以修改（赋值）

     ![image-20231024173935981](http://images.newstar.net.cn/sally-imgs/image-20231024173935981.png)

     

2. 尽量在scroll事件里面获取被卷去的距离

```javascript
div.addEventListener('scroll', function () {
    console.log(this.scrollTop)
  })
```



3. 开发中，我们经常检测页面滚动的距离，比如页面滚动100像素，就可以显示一个元素，或者固定一个元素

\- 举例说明：

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Document</title>
  <style>
    body {
      padding-top: 100px;
      height: 3000px;
    }

    div {
      display: none;
      margin: 100px;
      overflow: scroll;
      width: 200px;
      height: 200px;
      border: 1px solid #000;
    }
  </style>
</head>

<body>
  <div>
    我里面有很多文字 我里面有很多文字 我里面有很多文字 我里面有很多文字 我里面有很多文字
    我里面有很多文字 我里面有很多文字 我里面有很多文字 我里面有很多文字 我里面有很多文字
    我里面有很多文字 我里面有很多文字 我里面有很多文字 我里面有很多文字
  </div>
  <script>
    const div = document.querySelector('div')
    // 页面滚动事件
    window.addEventListener('scroll', function () {
      // console.log('我滚了')
      // 我想知道页面到底滚动了多少像素,被卷去了多少  scrollTop
        
      // 获取html元素写法： document.documentElement ，documentElement就是html
      // console.log(document.documentElement.scrollTop)

      const n = document.documentElement.scrollTop
      if (n >= 100) {
        div.style.display = 'block'
      } else {
        div.style.display = 'none'
      }
    })

    // 给div盒子 添加滚动式事件
    // const div = document.querySelector('div')
    // div.addEventListener('scroll', function () {
    //   // console.log(111)
      
    //   // scrollTop 被卷去的头部
    //   console.log(div.scrollTop)
    // })
  </script>
</body>

</html>
```

> **结论：**
>
> 1. 想知道页面到底滚动了多少像素,被卷去了多少？用`scrollTop`
> 2. 获取html元素写法： `document.documentElement` ,html文档返回对象是html元素 即documentElement就是html
> 3. 检测页面滚动的头部距离（被卷去的头部）用`document.documentElement.scrollTop`



#### 页面滚动事件-滚动到指定的坐标

##### 写法一：scrollTop细节

\- 举例说明：

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Document</title>
  <style>
    body {
      height: 3000px;
    }
  </style>
</head>

<body>
  <script>
    document.documentElement.scrollTop = 800
    window.addEventListener('scroll', function () {
      // 必须写到里面
      const n = document.documentElement.scrollTop
      // 得到是什么数据   数字型 不带单位
      // console.log(n)
    })
  </script>
</body>

</html>
```

> **结论：**
>
> 1. `document.documentElement.scrollTop`必须写到里面,得到是数字型数据 不带单位
> 2. `scrollTop`可`读写`，可以读取，也可以修改（赋值）,**赋值一定数字型，不带单位** document.documentElement.scrollTop = 800



##### 写法二：scrollTo()

* scrollTo() 方法可把内容滚动到指定的坐标

* 语法：

```javascript
元素.scrollTo(x, y)
```

\- 举例说明：

```javascript
window.scrollTo(0, 1000) //让页面滚动到 y轴 1000像素的位置
```





### 页面尺寸(缩放)事件

#### resize 

会在窗口尺寸改变(浏览器窗口大小发生变化)的时候触发事件：

* 事件名：resize 

```javascript
window.addEventListener('resize', function() {
    // 执行的代码
})
```

\- 举例说明：

```javascript
<script>
// resize 浏览器窗口大小发生变化的时候触发的事件
window.addEventListener('resize', function () {
  console.log(1)
})
</script>
```



#### clientwidth和clientHeight

* 检测屏幕宽度：

  * clientWidth

  ```javascript
  window.addEventListener('resize', function() {
      let w = document.documentElement.clientWidth
       console.log(w)
  })
  ```

  \- 举例说明：

  ```html
  <!DOCTYPE html>
  <html lang="en">
  
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
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
      console.log(div.clientWidth) //获取元素宽度（不含边框，margin，滚动条等）
      // resize 浏览器窗口大小发生变化的时候触发的事件
      window.addEventListener('resize', function () {
        console.log(1)
      })
    </script>
  </body>
  
  </html>
  ```



* 获取元素宽高：
  1. `clientwidth和clientHeight`
  2. 获取元素的可见部分宽高(`不包含边框border`，margin，滚动条等）

![image-20231025163043710](http://images.newstar.net.cn/sally-imgs/image-20231025163043710.png)





## 元素尺寸与位置

* 使用场景：
  1. 前面案例滚动多少距离，都是我们自己算的，最好是页面滚动到某个元素，就可以做某些事。
  2. 简单说，就是**通过js**的方式，得到`元素在页面中的位置`
  3. 这样我们可以做，页面滚动到这个位置，就可以做某些操作，省去计算了

![image-20231025182232446](http://images.newstar.net.cn/sally-imgs/image-20231025182232446.png)





### 元素尺寸与位置-尺寸

* 获取宽高：
  1. 获取元素的自身宽高、包含元素自身设置的宽高、padding、`border`
  2. `offsetWidth`和offsetHeight (得到元素 内容 + padding + border的宽高)
  3. 获取出来的是数值,方便计算
  4. 注意: 获取的是可视宽高, 如果盒子是隐藏的,获取的结果是0



### 元素尺寸与位置-位置(重点)

* 获取位置：
  1. 获取元素距离自己定位父级元素的左、上距
  2. `offsetLeft` 和 `offsetTop` 注意是`只读`属性

![image-20231025182659609](http://images.newstar.net.cn/sally-imgs/image-20231025182659609.png)



#### offsetTop和offsetLeft得到的位置以谁为准

1. 检测盒子的位置：查找最近一级带有定位的祖先元素
   * 简单理解：得到的位置以`带有定位的父级为准`，父级有定位以父级位置为准，没有定位往下继续找`最近一级带有定位的父级为准`，类似绝对定位
2. 如果都没有则以 文档左上角 为准

\- 举例说明：

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Document</title>
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
    // console.log(div.offsetLeft) // 结果108 因为body有个8像素的外边距，100+8
    const p = document.querySelector('p')
    // 检测盒子的位置  查找最近一级带有定位的祖先元素
    console.log(p.offsetLeft) // 父加上定位，结果就是50
    //div父没加定位，就是158，因为子盒子到父盒子是50像素距离，父到边框是100距离加一个外边距8
  </script>
</body>

</html>
```

> **分析：**
>
> 1. offsetLeft受父级影响，如果div没加定位，就是158，因为到父盒子是50像素距离，父到边框是100距离加一个外边距8
> 2. 父加上定位，则结果就是50

![image-20231129145813280](http://images.newstar.net.cn/sally-imgsimage-20231129145813280.png)







### 获取元素大小位置的另外方法

* 获取方法返回元素的大小及其相对于视口（可视区）的位置
* 语法：

```javascript
element.getBoundingClientRect()
```

\- 举例说明：

```javascript
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Document</title>
  <style>
    body {
      height: 2000px;
    }

    div {
      width: 200px;
      height: 200px;
      background-color: pink;
      margin: 100px;
    }
  </style>
</head>

<body>
  <div></div>
  <script>
    const div = document.querySelector('div')
    console.log(div.getBoundingClientRect())
  </script>
</body>

</html>
```





## 总结-尺寸与位置 

![image-20231124192322784](http://images.newstar.net.cn/sally-imgsimage-20231124192322784.png)

