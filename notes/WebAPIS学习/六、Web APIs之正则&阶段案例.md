# 正则&阶段案例

[toc]

## 正则表达式

`正则表达式`（Regular Expression）简称reg，`是`用于匹配字符串中字符组合的`模式`，在 JavaScript中，正则表达式也是对象



### 基本介绍

1. 通常用来查找、替换那些符合正则表达式的文本,许多语言都支持正则表达式



\- 举例说明：

请在上图中找出【戴帽子和眼镜的男人】

![image-20231212100140856](http://images.newstar.net.cn/sally-imgsimage-20231212100140856.png) 

戴帽子、戴眼镜、男人都是描述信息，通过这些信息能够在人群中查找到确定的某个人，那么这些用于查找的描述信息编写一个模式，对应到计算机中就是所谓的正则表达式。



2. 正则表达式在 JavaScript中的使用场景：

* **验证表单**：用户名表单只能输入英文字母、数字或者下划线， 昵称输入框中可以输入中文(`匹配`)
  * 比如用户名: /^[a-z0-9_-]{3,16}$/
* **过滤**掉页面内容中的一些**敏感词**(`替换`)，或从**字符串中获取我们想要的特定部分**(`提取`)等

![1676079666366](http://images.newstar.net.cn/sally-imgs1676079666366.png) 



​               ![](http://images.newstar.net.cn/sally-imgsimage-20231212100802033.png) 



> **结论：** 
>
> 1. 正则表达式 是一种字符串匹配的`模式`（规则）
> 2. 正则表达式作用：主要做表单验证(`匹配`)、过滤敏感词(`替换`)、字符串中获取我们想要的部分(`提取`)





### 语法

JavaScript 中定义正则表达式的语法有两种，我们先学习其中比较简单的方法

#### 定义正则表达式

* 定义规则语法：

~~~JavaScript
const 变量名 =  /表达式/
~~~

> **分析：**
>
> 1. 其中` /   / `是正则表达式字面量 
> 2. 正则表达式也是`对象 `

\- 举例说明：

```javascript
<script>
const str = '我们在学习前端，希望学习前端能高薪毕业'
// 正则表达式使用：
// 1. 定义规则
const reg = /前端/
</script>
```





#### 检测查找是否匹配

* 使用正则

  * `test()方法`   用来查看正则表达式与指定的字符串是否匹配
  * 如果正则表达式与指定的字符串匹配 ，返回`true`，否则`false`

* 语法：

  ```javascript
  regObj.test(被检测的字符串)
  ```

  分析：前面regObj是定义的规则，后面test是被检查(先有规则，才能检查)

  

  \- 举例说明：

  ```javascript
  <script>
  const str = '我们在学习前端，希望学习前端能高薪毕业'
  // 正则表达式使用：
  // 1. 定义规则
  const reg = /前端/
  
  // 2. 是否匹配
  console.log(reg.test(str))  // true
  
  </script>
  </body>
  ```

  分析:reg.test(str)指的是str里到底有没有 前端这两个字，因为前面定义了规则为前端，那后面字符串包含这两字

  



#### 检索（查找）符合规则的字符串

* `exec()` 方法 在一个指定字符串中执行一个搜索匹配

* 如果匹配成功，exec() 方法返回一个数组，否则返回null

* **语法：**

  ```javascript
  regObj.exec(被检测字符串)
  ```

  \- 举例说明：

  ```javascript
  <script>
  const str = '我们在学习前端，希望学习前端能高薪毕业'
  // 正则表达式使用：
  // 1. 定义规则
  const reg = /前端/
  
  // 2. 是否匹配
  // exec()
  console.log(reg.exec(str))  // 返回数组
  
  </script>
  </body>
  ```





#### test方法和exec方法的区别

1. test方法 用于判断是否有符合规则的字符串，返回的是布尔值 找到返回true，否则false
2. exec方法用于检索（查找）符合规则的字符串，找到返回数组，否则为 null







### 元字符

* **普通字符:**

  1. 大多数的字符仅能够描述它们本身，这些字符称作普通字符，例如所有的字母和数字。
  2. 普通字符只能够匹配字符串中与它们相同的字符。 

  * 比如，规定用户只能输入英文26个英文字母，普通字符的话  /[abcdefghijklmnopqrstuvwxyz]/

* **元字符(特殊字符）**：

  1. 是一些具有特殊含义的字符，可以极大提高了灵活性和强大的匹配功能。

  * 比如，规定用户只能输入英文26个英文字母，换成元字符写法： /[a-z]/  更简洁灵活

* 参考文档：[MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Guide/Regular_Expressions)、[正则测试工具](http://tool.oschina.net/regex)





#### 元字符分类

##### 边界符

1. `表示位置，开头和结尾，必须用什么开头，用什么结尾`
2. 正则表达式中的边界符（位置符）用来`提示字符所处的位置`，主要有两个字符

![1676080081650](http://images.newstar.net.cn/sally-imgs1676080081650.png)

> **注：** ^ 和 $ 在一起，表示必须是精确匹配。



\- 举例说明：

```javascript
// 例1 匹配开头的位置 ^
console.log(/^哈/.test('哈')) // true
console.log(/^哈/.test('哈哈')) // true
console.log(/^哈/.test('二哈')) // flase
// 例1
const reg = /^web/
console.log(reg.test('web前端'))  // true
console.log(reg.test('前端web'))  // false
console.log(reg.test('前端web学习'))  // false
console.log(reg.test('we'))  // false

// 例2 精确匹配 ^ $
console.log(/^哈$/.test('哈')) // true  只有这种情况为true 否则全是false
// 例2
const reg2 = /^web$/
console.log(reg2.test('web前端'))  //  false
console.log(reg2.test('前端web'))  // false
console.log(reg2.test('前端web学习'))  // false
console.log(reg2.test('we'))  // false 
console.log(reg2.test('web'))  // true
console.log(reg2.test('webweb'))  // flase 

// 例3 匹配结束的位置 $
console.log(/^哈$/.test('哈哈')) // false
console.log(/^哈$/.test('二哈')) // false
// 例3
const reg1 = /web$/
console.log(reg1.test('web前端'))  //  false
console.log(reg1.test('前端web'))  // true
console.log(reg1.test('前端web学习'))  // false
console.log(reg1.test('we'))  // false  

```







##### 量词

1. 表示`重复次数`
2. 量词用来 `设定某个模式出现的次数`

![1676080185383](http://images.newstar.net.cn/sally-imgs1676080185383.png) 

 **注：**`逗号左右两侧千万不要出现空格`



> **总结：**
>
> 1. \+ 表示重复至少 1 次 (类似 >=1 次)
> 2. ? 表示重复 0 次或1次 (类似 0 || 1次)
> 3. \* 表示重复 0 次或多次 (类似 >=0次)
> 4. `{n}`写几，就必须出现几次
> 5. {n,}  (类似 >=n次)
> 6. {m, n} 表示重复 m 到 n 次  (类似 ≤ n && ≥ m)

\- 举例说明：

```javascript
<body>
<script>
// 元字符之量词
// 1. * 重复次数 >= 0 次
const reg1 = /^w*$/
console.log(reg1.test(''))  // true
console.log(reg1.test('w'))  // true
console.log(reg1.test('ww'))  // true
console.log('-----------------------')

// 2. + 重复次数 >= 1 次
const reg2 = /^w+$/
console.log(reg2.test(''))  // false
console.log(reg2.test('w'))  // true
console.log(reg2.test('ww'))  // true
console.log('-----------------------')

// 3. ? 重复次数  0 || 1 
const reg3 = /^w?$/
console.log(reg3.test(''))  // true
console.log(reg3.test('w'))  // true
console.log(reg3.test('ww'))  // false
console.log('-----------------------')


// 4. {n} 重复 n 次
const reg4 = /^w{3}$/
console.log(reg4.test(''))  // false
console.log(reg4.test('w'))  // flase
console.log(reg4.test('ww'))  // false
console.log(reg4.test('www'))  // true
console.log(reg4.test('wwww'))  // false
console.log('-----------------------')

// 5. {n,} 重复次数 >= n 
const reg5 = /^w{2,}$/
console.log(reg5.test(''))  // false
console.log(reg5.test('w'))  // false
console.log(reg5.test('ww'))  // true
console.log(reg5.test('www'))  // true
console.log('-----------------------')

// 6. {m,n}  重复次数 >=m && <= n  ，大于等于2 或小于等于4次
const reg6 = /^w{2,4}$/
console.log(reg6.test('w'))  // false
console.log(reg6.test('ww'))  // true
console.log(reg6.test('www'))  // true
console.log(reg6.test('wwww'))  // true
console.log(reg6.test('wwwww'))  // false

// 7. 注意事项： 逗号两侧千万不要加空格否则会匹配失败

</script>
```



##### 字符类

* `[ ]` 匹配字符集合

* 后面的字符串只要包含 abc 中任意`一个字符`，都返回 true 

```javascript
// 字符类   [abc]  只选1个
console.log(/^[abc]$/.test('a'))  // true
console.log(/^[abc]$/.test('b'))  // true
console.log(/^[abc]$/.test('c'))  // true
console.log(/^[abc]$/.test('ab'))  // false //有精确匹配
console.log(/^[abc]{2}$/.test('ab'))  // true 加量词，重复两次
console.log('------------------')
// 字符类   [a-z]  只选1个
console.log(/^[A-Z]$/.test('p'))  // false
console.log(/^[A-Z]$/.test('P'))  // true
console.log(/^[0-9]$/.test(2))  // true
console.log(/^[a-zA-Z0-9]$/.test(2))  // true
console.log(/^[a-zA-Z0-9]$/.test('p'))  // true
console.log(/^[a-zA-Z0-9]$/.test('P'))  // true
console.log('------------------')
```





##### 范围 

表示字符的范围，定义的规则限定在某个范围，比如只能是英文字母，或者数字等等，用表示范围

![1676080296168](http://images.newstar.net.cn/sally-imgs1676080296168.png) 



1. `[ ]` 里面加上 - `连字符`,表示一个范围

```javascript
 console.log(/^[a-z]$/.test('c'))  // true
```

>**注：**
>
>* [a-z] **表示** `a 到 z` **26个英文字母都可以**
>* [a-zA-Z] 表示大小写都可以
>* [0-9] 表示 0~9 的数字都可以

\- 举例说明：

![image-20231213213929268](http://images.newstar.net.cn/sally-imgsimage-20231213213929268.png) 

> **解析：**
>
> * [1-9]表示第一个数为数字1-9中的一个。[0-9]{4，}表示第二个数开始0-9任意一个数都行且重复次数≥4
> * 因为QQ号有多位数的，而QQ号是从10000开始的，0000最少也是4位,加上第一位数就是5位数(`花括号只重复离的最近的次数`)



2. `[ ]` 里面加上` ^ 取反`符号

* 表示 "除了" 的意思，比如 [ ^a-z ] 匹配除了小写字母以外的字符(除了小字母其余都行)



3. ` 点 . `匹配除换行符之外的任何单个字符(除了换行其余都行)

   

   

4. `预定义`类：指的是`某些常见模式的简写方式`，区分字母和数字(大字母都是取反)

   ![1676080353637](http://images.newstar.net.cn/sally-imgs1676080353637.png)

   \- 举例说明：

     ```javascript
   日期格式: ^\d{4}-\d{1,2}-\d{1,2}$
     ```

   解析：日期2023-12-14：  \d{4}是0-9的数字，出现4次，2023- ；\d{1,2}是0-9的数字，出现1-2次，如1-或12-







### 修饰符

1. 修饰符约束正则执行的某些细节行为，如是否区分大小写、是否支持多行匹配等
2. 语法：

```javascript
/表达式/修饰符
```



#### 修饰符-i

i 是单词 ignore 的缩写，正则匹配时字母不区分大小写

```javascript
<script>
console.log(/^java$/.test('java')) // true
console.log(/^java$/.test('JAVA')) // false

// 加修饰符i 不区分大小写
console.log(/^java$/i.test('JAVA')) // true
console.log(/^java$/i.test('Java')) // true

</script>
```



#### 修饰符-g

g 是单词 全局的 global 的缩写，匹配所有满足正则表达式的结果(查找时全局查找)

```javascript
<script>
const str = '欢迎大家学习前端，相信大家一定能学好前端，都成为前端大神'

// replace 返回值是替换完毕的字符串
// const strEnd = str.replace(/前端/, 'web') 只能替换一个

// 修饰符 g 全部替换
const strEnd = str.replace(/前端/g, 'web')
console.log(strEnd) 
</script>
```



#### 替换 replace方法

* replace 替换方法，可以完成字符的替换

*  **语法：**

```javascript
字符串.replace(/正则表达式/, '替换的文字')
```

\- 举例说明：

```javascript
<script>
// 需求：把java和Java替换为 前端
const str = 'java是一门编程语言， 学完JAVA工资很高'
// const re = str.replace(/java|JAVA/g, '前端') // 只写g替换的是小写的，要用| 或者后面跟ig
const re = str.replace(/java/ig, '前端') 
console.log(re)  // 前端是一门编程语言， 学完前端工资很高
</script>
```

> **结论：** `|` 等同于 `或` 的意思



