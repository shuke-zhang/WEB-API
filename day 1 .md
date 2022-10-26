#  webAPI第一天

##  splice删除数组元素

###  数据新增和删除的方式

1. 从数组最后一个元素或多个元素添加到数组最后的位置 ===> push，语法 ：arr .  push('新增数据1'，'新增数据2') ==> 返回的是新数组的长度

2. 将一个元素或者多个元素新增在数组的开头 ===> unshift, 语法 ：arr.unshift("我现在是新增的第一个", "我现在是新增的第二个") ==> 返回新数组的长度

3. 删除数组中最后一个元素 ===> pop ， 语法 ：数组名 . pop() ==> 返回的是被删除的元素

4. 删除数组中第一个元素 ===> shift ,   语法 ：数组名 .  shift() ==> 返回的是被删除的元素

5. 指定删除数组中某一个或多个元素 ===> splice ,   语法 ： 数组.splice("起始位置的下标","删除元素的个数" ) ==> 返回的是一个数组，数组里面包含着被删除的元素

   >1. 参数1 => 从哪儿开始删, 参数2 => 要删几个
   >
   >2. 如果不写参数2,就默认从起始位置删除到最后
   >
   >3. 如果用变量去接收返回值, 得到的是一个数组,数组里包含了被删除的元素的值

###  利用splice来新增元素

1. 同时也可以用splice来指定位置添加元素
2. 语法  ===>  arr.splice(起始位置，删除的个数，需要添加的元素)
3.  参数一表示需要添加的元素在原数组中的位置，  参数二一般填0，参数三直接填写需要添加的元素 需要用引号包裹起来

##  let和const命名的区别

1. 字面量： [] {} 只要看到这个就知道是什么， {} => 看到就知道是个对象 ， [] => 看到就知道是个数组

2.  基本数据类型的数值存放在栈里面，引用数据类型的数值是在堆里面

3. let 一般用于需要改变的变量命名，比如如果用到 for 循环时就使用 let ，const 用于不可更改的变量命名

4. const 声明的变量的值如果是引用类型，栈里面存的是地址， 指向堆空间中的数据。

5.  const arr = []       arr = [1, 2, 3]  这种写法不可以 ===>   数组栈里面存的是地址， 堆里面存放数据，平时输出的是利用栈里面的地址，去堆里面找相应的数据，上述写法相当于给arr重新赋值，所以栈里面的地址都改变了！而空数组其实在栈里面和堆里面都是占位置的，只是没有数值而已   。地址都改变了，此时就不能用const 用 let 更合理

6. const arr1 = [1, 2, 3]    arr1.push(4)    console.log(arr1); 这种写法可以，它只是新增了一个元素，相当于只是在堆里面新增数据，栈里面的地址并没有改变

7. 所以 ===>  如果声明数组对象，建议使用const , 当声明的值要发生改变的时候， 可以用 let

   

##  数据类型拓展

   ！！！ 这是面试题 => 一定记住 ！！！

   ###  基本数据类型

     	Number（数字类型）    String（字符串类型）    Boolean（布尔类型true 和false）    undefined （未定义类型）  
    
     	 null （空类型）    Symbol（符号类型）    BigInt（最大大数字）

   ###  引用类型(复杂类型) 

   ​	Object 只有一个就是对象

   ​	 Array / Function / Math  /  RegExp / Date / Error

   ###  存储

   ​	  Stack栈： 基本数据类型存在栈里面

   ​	 heap堆： 引用类型变量名存在栈里面，栈里面的值存的是地址，指向堆空间中的数据

   

###  检测数据类型！！！

####  typeof检测

1.  typeof 返回的数据类型时字符串的类型，比如检测一个数字 1 ，它返回的就是字符串类型的 Number
2. typeof 只能检测基本数据类型 检测数组只能检测出它属于对象

~~~ js
// typeof 返回的数据类型时字符串的类型，比如检测一个数字 1 ，它返回的就是字符串类型的 Number
        typeof null // Object 这个一个bug null是数字000 开头，而对象也是 000 所以会显示Object
        typeof typeof 1 // string 返回的是一个字符串类型的 'number'
        typeof true // 'bolean'

        // typeof 只能检测基本数据类型 检测数组只能检测出它属于对象 
        typeof [1, 2, 3] // 'Object'
        typeof {}  // 'Object'  
        typeof function () { }  // 'Object'
~~~

####  A  instanceof  B 检测引用数据类型

1. 语法：需要检测的数值  instanceof  数据类型

~~~js
console.log([1, 2, 3,] instanceof Array);
        console.log({} instanceof Object);
        console.log(function () { } instanceof Function);
        // 用这个检测基本数据类型是都会显示false
        console.log('下面是测试');

        console.log(1 instanceof Number);
        console.log('1' instanceof String);
        console.log(true instanceof Boolean);
~~~

控制台输出打印结果 ===> ![image-20221006200053865](assets/image-20221006200053865-1665062386038-14.png)



> 1. 返回的值是true或者false 检测引用数据类型
> 2. 用这个检测基本数据类型是都会显示false
> 3. 判断是不是 首字母需要大写 数组是 Array

####  Object.prototype.toString.call() 完美检测数据（两种都可以检测）

1. 语法： Object.prototype.toString.call( 需要检测的数值)

~~~js
console.log(Object.prototype.toString.call(1)) // Number
        console.log(Object.prototype.toString.call(true)) //  Boolean
        console.log(Object.prototype.toString.call([1, 2, 3])) // Array
        console.log(Object.prototype.toString.call({}))  // Object
        console.log(Object.prototype.toString.call(function () { })) // Function
        console.log(Object.prototype.toString.call(null))  // Null
        console.log(Object.prototype.toString.call(undefined)) // Undefined
~~~



控制台输出打印结果 ===> ![image-20221019203717018](assets/image-20221019203717018.png)



####  数组专用检测方法Array.isArray() 

1. 语法 ： Array.isArray(需要检测的数值)
2. 描述： 如果对象是 [`Array`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array)，则返回 `true`，否则为 `false`。

~~~js
Array.isArray([1, 2, 3]);  // true
Array.isArray({foo: 123}); // false
Array.isArray('foobar');   // false
Array.isArray(undefined);  // false
~~~

##  WebAPI的认识

文档： document， 一个页面就是一个文档
元素： element  页面上所有的标签都叫做元素
节点： node 页面上所有的内容都叫节点  元素节点  文本节点 属性节点 注释节点
document -> 它是一个页面里面的顶级对象

DOM：document object model  文档对象模型   把我们的页面当作一个对象来看待
BOM：browser object model  把我们的浏览器当作一个对象来看待

API： appliation programming interface  应用程序编程接口  ==> 理解为方法。

## 获取元素

###  document.querySelector 获取第一个元素

1. 只能获取到第一个元素，如果存在多个相同标签，它也只会获取第一个
2. 返回的就是第一个元素，需要用引号包裹，否则的话就是一个变量了
3. 在用类名或者ID来获取时需要加上   .   #  与css选择器是一样的
4.  打印一个对象的所有属性和方法 dir    ===>  console.dir(res);
           

~~~js
<body>
    <div class="box">123</div>
    <div class="box">abc</div>
    <p id="nav">导航栏</p>
    <ul class="nav">
        <li>测试1</li>
        <li>测试2</li>
        <li>测试3</li>
    </ul>
    <script>
        // 获取元素  document.querySelector (选择器)
        // 获取匹配的第一个元素
        // 返回值： 匹配的第一个元素/对象
        // 需要用引号包裹，否则的话就是一个变量了
        // 用类名或者ID来选择时需要加上   .   #  与css选择器是一样的
        const res = document.querySelector('div')
        console.log(res);
        console.log(typeof res); // object
        // 打印一个对象的所有属性和方法 dir
        console.dir(res);
        // 采用类名来获取元素 css选择器一致
        const box = document.querySelector('.box')
        console.log(box);
        // 采用id来获取元素
        const nav = document.querySelector('#nav')
        console.log(nav);
        // ul中第一个li标签
        const li = document.querySelector('ul li')
        console.log(li);  
    </script>
</body>
~~~

控制台输出打印结果 ===> ![image-20221006201718942](assets/image-20221006201718942.png)



###  document.querySelectorAll 获取全部元素

1.  她返回的是一个伪数组：有索引下标 有长度 但是没有方法 比如 pop push等
2. 返回的就是第一个元素，需要用引号包裹，否则的话就是一个变量了
3. 在用类名或者ID来获取时需要加上   .   #  与css选择器是一样的

~~~js
<body>
    <div class="box">123</div>
    <div class="box">abc</div>
    <p id="nav">导航栏</p>
    <ul class="nav">
        <li>测试1</li>
        <li>测试2</li>
        <li>测试3</li>
    </ul>
    <script>       
        console.log('匹配多个');
        //  匹配多个 document.querySelectorAll
        // 她返回的是一个伪数组：有索引下标 有长度 但是没有方法 比如 pop push等
        const res1 = document.querySelectorAll('div')
        console.log(res1);
        console.log('--------------');
        // 获取全部li
        const li2 = document.querySelectorAll('.nav li')
        console.log(li2);
        // 获取全部div
        const div3 = document.querySelectorAll('div')
        console.log(div3);
        // 利用id来选择
        const ceshi = document.querySelectorAll('#nav')
        console.log(ceshi);            
    </script>
</body>
~~~

控制台输出打印结果 ===> ![image-20221006202105722](assets/image-20221006202105722.png)





4. 小练习： 控制台输出三个li

   ~~~ js
     const lis = document.querySelectorAll('.nav li')
   
   
   
      for (let i = 0; i < lis.length; i++) {
   
         console.log(lis[i])
   
       }
   
   ~~~

   控制台输出打印结果 ===> ![image-20221006202536437](assets/image-20221006202536437-1665062364573-8.png)

 ##  获取DOM元素的其他方法（了解）

###  其他方法获取方式



1. 通过这种方法不需要写  .  # 等符号
2. Elements代表复数，返回的也是个伪数组

   ~~~js
   <body>
       <div id="box"></div>
       <p>1</p>
       <p>2</p>
       <span class="nav"></span>
       <span class="nav"></span>
   
   // 前面的方法
           // const boxq = document.querySelector('#box')
           // 解释为  By 通过  Id
           const boxq = document.getElementById('box')
           console.log(boxq);
   
           // 也可以通过类名来直接获取 ClassName 类名
           //  Elements 复数，也是代表全部，获取到的也是一个伪数组
           const spans = document.getElementsByClassName('nav')
           console.log(spans);
   
           // 通过标签名
           const p2 = document.getElementsByTagName('p')
           console.log(p2);
   </body>
   ~~~

控制台输出打印结果 ===> ![image-20221006203148817](assets/image-20221006203148817.png)

###  两个特殊的元素body、html

~~~js
// 两个特殊的元素
        // 1. body  ===> document.body
        // const body = document.querySelector('body')
        // console.log(body);
        // 可以直接这样写
        console.log(document.body);
        console.log('----------------------------------------');

        // 2.html ===> document.documentElement
        // const html2 = document.querySelector('html')
        // console.log(html2);
        // 直接这样写
        console.log(document.documentElement);
~~~

控制台输出打印结果 ===> ![image-20221006203107362](assets/image-20221006203107362.png)

##  修改对象内容

1. 语法： 对象.innerText = 值         对象.innerHTML = 值

~~~js
<body>
    <script>
        // 1. 获取元素
        const box = document.querySelector('.box')
        console.log(box)
        // 2. 修改内容

        // innerText
        // 2.1 获取对象的内容 对象.innerText
        console.log(box.innerText)
        // 2.2 修改内容  对象.innerText = 值
        box.innerText = '我是修改后的内容'

        // innerHTML
        // 2.1 获取对象的内容 对象.innerHTML
        // console.log(box.innerHTML)
        // 2.2 修改内容  对象.innerHTML = 值
        // box.innerHTML = '大家饿了嘛'

        // 3. innerText 和 innerHTML区别
        box.innerText = '<strong>我是内容</strong>'  // 不能解析html标签
        box.innerHTML = '<strong>我是内容</strong>'  // 可以解析html标签
    </script>
</body>
~~~

###  innerText和innerHTML的区别

1.   innerText => 不能识别标签，会直接连带着标签输出

~~~js
box.innerText = '<strong>我是内容</strong>'  // 不能解析html标签
~~~

页面打印效果 ===> ![image-20221006203805582](assets/image-20221006203805582.png)

2. innerHTML => 可以识别标签，能够产生标签内的效果

~~~ js
 box.innerHTML = '<strong>我是内容</strong>'  // 可以解析html标签
~~~

页面打印效果 ===>  ![image-20221006203931593](assets/image-20221006203931593.png)



##  随机抽奖案列

1. 需求： 当页面刷新时，一等奖、二等奖、三等奖里面的姓名随机显示
1. 注意，在取三个随机数时，由于一等奖已经有了，所以一等奖姓名将不能出现在二等奖和三等奖中，就要删除元素
1. 需要在抽出一等奖之后再取二等奖的随机数，所以二等奖的随机数要放在一等奖删除数组后面
1. 当执行到一等奖时数组内有四个元素， 执行到二等奖时 数组内有三个元素 ， 执行到三等奖时数组内有两个元素

~~~js
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>年会抽奖</title>
    <style>
        .wrapper {
            width: 840px;
            height: 420px;
            background: url(./images/bg01.jpg) no-repeat center / cover;
            padding: 100px 250px;
            box-sizing: border-box;
        }
    </style>
</head>

<body>
    <div class="wrapper">
        <strong>传智教育年会抽奖</strong>
        <h1>一等奖：<span id="one">???</span></h1>
        <h3>二等奖：<span id="two">???</span></h3>
        <h5>三等奖：<span id="three">???</span></h5>
    </div>
    <script>
        //  1.声明一个数组
        const arr = ['周杰伦', '刘德华', '周星驰', '练练老师', '张学友']
        //  2. 随机取数组中的一个元素
        const i = Math.floor(Math.random() * arr.length)
        // 打印输出结果是否正确
        // console.log(i);
        // 3.获取DOM元素
        const one = document.querySelector('#one')

        // console.log(one);
        // 4. 修改元素内的内容够
        one.innerHTML = arr[i]
        // 为保证每个名字只出现一次，所以需要删除随机出现的那个元素
        arr.splice(i, 1)
        console.log(arr);
        // 二等奖
        const j = Math.floor(Math.random() * arr.length)
        const two = document.querySelector('#two')
        two.innerHTML = arr[j]
        arr.splice(j, 1)

        // 三等奖
        const k = Math.floor(Math.random() * arr.length)
        const three = document.querySelector('#three')
        three.innerHTML = arr[k]
        arr.splice(k, 1)

        // 总结
        //  1. 随机取数组中的一个元素下标
        //  2.
        //  3.
        //  4. 

    </script>
</body>

</html>
~~~

效果图![image-20221006204144652](assets/image-20221006204144652.png)

##  页面刷新随机展示图片

1. 当页面刷新时，图片会随机改变

~~~js
<body>
    <img src="./images/1.webp" alt="">
    <script>
        // 需求： 当页面刷新时自动随机换图片
        // 1.封装一个函数取随机数
        function getNum(min, max) {
            return Math.floor(Math.random() * (max - min + 1)) + 1
        }
        const i = getNum(1, 6)
        console.log(i);
        // 2. 获取这个元素
        const img = document.querySelector('img')
        // 3. 利用模板字符串更改
        img.src = `./images/${i}.webp`
    </script>
</body>
~~~



##  通过style操作样式

###  基本语法



1. 语法： 对象.style.属性 = 值
2. 这种书写方式是直接书写在行内式的![image-20221006204608227](assets/image-20221006204608227.png)
3. 在css中 带 - 的写在js中需要首字母大写，即小驼峰命名
4. console.log(box.style.width);  通过这种方法获取的样式只能获取标签的行内样式，不能获取到css里面的样式

~~~js
<style>
        .box {
            width: 200px;
            height: 200px;
            background-color: pink;
            margin: 100px auto;
            text-align: center;
        }
    </style>
</head>

<body>
    <div class="box">这是一句话</div>
    <script>
        // 获取元素
        const box = document.querySelector('.box')
        //  1. 获取样式
        // 注意： 通过这种方法获取的样式只能获取标签的行内样式，不能获取到css里面的样式
        console.log(box.style.width);

        // 设置样式 对象.style.属性 = 值
        // 注意：width height 都需要带单位
        // 这种方法修改的样式，是直接写在行内样式的，
        // 在css中 带 - 的需要首字母大写，即小驼峰命名
        box.style.width = '300px'
        box.style.height = '300px'
        box.style.borderRadius = '50%'
        box.style.lineHeight = '300px'
    </script>
</body>
~~~



###  随机更换背景图片小案列

1. 当页面刷新，随机更换body的背景图片

~~~js
<script>
        // 封装一个函数 
        const getRandom = function (n, m) {
            return Math.floor(Math.random() * (m - n + 1) + n)
        }
        const i = getRandom(1, 10)
        console.log(i);
        // 获取元素 由于是body 所以可以直接获取
        // document.body.style.backgroundImage = `url(./images/desktop_${i}.jpg)`
        // 同样可以分为两步来
        const body = document.body
        body.style.backgroundImage = `url(./images/desktop_${i}.jpg)`
    </script>
~~~



##  **通过className修改样式**

###  语法规范

1. 注意：通过这种方式来修改的类名会覆盖掉原有的类名，如果想要保留原有的。可以直接一起写出来
1. 通过style适合单个或少量的样式修改，className适合修改多个样式一起修改
1. className 可以先给多个样式命名一个函数，通过className来添加函数（但是不推荐）
1. className可以适用于清空类名 ===>    box.className = ''
   

~~~js
 <div class="box" style="width: 600px;">这是一句话</div>
    <script>
        const box = document.querySelector('.box')
        // box.style.width = '300px'
        // box.style.height = '300px'
        // box.style.borderRadius = '50%'
        // box.style.lineHeight = '300px'
        // 上面这种通过style来修改时，如果需要修改多个机会显得很繁琐
        // 所以我们可以通过className类名来设置
        // 注意：通过这种方式来修改的类名会覆盖掉原有的类名，如果想要保留原有的。可以直接一起写出来
        box.className = 'box active'

        // 实际应用场景
        //  1. style适合单个或少量的样式修改
        //  2. className适合修改多个样式一起修改
        //  3. className可以适用于清空类名
        // box.className = ''
    </script>
~~~

##  通过classList操作样式

###  语法规范

1. className来操作时会覆盖原有的类名
2. 操作多个 推荐使用classList ， 它不会覆盖原来的类名，只是单纯的追加或者移除或者切换
3. 追加类名   语法：元素.classList.add('类名')
4. 删除类名   语法：元素.classList.remove('类名')    remove =>去除
5. 切换类名   语法：元素.classList.toggle('类名')       toggle =>切换
6. 切换： 如果有这个类名，切换就是移除这个类名； 如果没有这个类名，就添加上这个类名

~~~js
// 3. classList里面类名不用加.  不加 .
        // 3.1 追加类名  元素.classList.add('类名')
        box.classList.add('ceshi')

        // 3.2 删除类名  元素.classList.remove('类名') remove ； 去除
        box.classList.remove('ceshi')

        // 3.3 切换类名 元素.classList.toggle('类名') toggle；切换
        // 切换： 如果有这个类名，切换就是移除这个类名； 如果没有这个类名，就添加上这个类名
        box.classList.toggle('ceshi')

        // 总结： 
        // 1. 单个 style
        // 2. className会覆盖原来类名
        // 3.多个 推荐使用classList ， 它不会覆盖原来的类名，只是单纯的追加或者移除或者切换
~~~

##  表单元素

###  语法规范

1. input  textarea  表单元素
2. 获取input的值  input.value 
3. 设置input的值 input.value  = 值
4. disabled禁用按钮属性

~~~ js
<body>
    <!-- <input type="text" class="inp"> -->
    <input type="checkbox" class="inp" checked>
    <!-- <input type="checkbox" checked> -->
    <!-- disabled禁用按钮 -->
    <button disabled>点击</button>
    <script>
        // 获取元素
        const input = document.querySelector('.inp')
        // 设置input的值value
        input.value = '修改了'

        // 如果我们此时获取这个值，用以前的方法
        console.log(input.innerHTML);
        // 此时就获取不到
        // 表单元素就需要用value值来获取
        console.log(input.value);


        // 修改input的type类型
        // radio单选框 checkbox多选框
        input.type = 'password'

        // ===============================
        // 有一些返回值是布尔类型  比如checked
        console.log(input.checked); // true

        const btn = document.querySelector('button')
        console.log(btn.disabled);
        console.log(typeof btn.disabled)


    </script>
~~~

##  自定义属性

1. 自己定义的属性，自定义属性必须以data-开头，规范，为了让我们一看到data-开头就知道这是个自定义属性

2. dataset 是一个对象，是将data- 去掉，把后面的部分存在这个对象里面

3. 当自定义属性出现两个- 以上时，我们在获取自定义属性时会以小驼峰来获取  ===> data-hm-me="66" 下面是打印

4. ![image-20221011181410023](assets/image-20221011181410023.png)

5. ~~~js
   // 对象.dataset中获取
           // 是将自定义属性都放在在dataset中的，它是一个对象所以也可以用对象的方法来获取属性
           // 两种方法，自定义属性里面是对象，所以也可以用对象的方法来获取属性
           console.log(box.dataset.id);
           console.log(box.dataset['id']);
   
           const a = document.querySelector('a')
           console.log(a.href);
           console.log(a['href']);
   
           // 当短横线出现两个及以上时,data-  后面的短横线自动会以小驼峰方式命名
           console.log(box.dataset.hmMe);
           console.log(box.dataset['heMe']);
   
   ~~~

 ##  获取元素所有属性

1. 语法：  console.dir(元素); ===>  比如获取元素box中的所有属性  console.dir(box); 
2. 其中 tagName = 'DIV'   会是一个大写的标签名，后面可以根据这个属性来判断

##  页面刷新堆积更换轮播图案列

~~~js
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>轮播图点击切换</title>
    <style>
        * {
            box-sizing: border-box;
        }

        .slider {
            width: 560px;
            height: 400px;
            overflow: hidden;
        }

        .slider-wrapper {
            width: 100%;
            height: 320px;
        }

        .slider-wrapper img {
            width: 100%;
            height: 100%;
            display: block;
        }

        .slider-footer {
            height: 80px;
            background-color: rgb(100, 67, 68);
            padding: 12px 12px 0 12px;
            position: relative;
        }

        .slider-footer .toggle {
            position: absolute;
            right: 0;
            top: 12px;
            display: flex;
        }

        .slider-footer .toggle button {
            margin-right: 12px;
            width: 28px;
            height: 28px;
            appearance: none;
            border: none;
            background: rgba(255, 255, 255, 0.1);
            color: #fff;
            border-radius: 4px;
            cursor: pointer;
        }

        .slider-footer .toggle button:hover {
            background: rgba(255, 255, 255, 0.2);
        }

        .slider-footer p {
            margin: 0;
            color: #fff;
            font-size: 18px;
            margin-bottom: 10px;
        }

        .slider-indicator {
            margin: 0;
            padding: 0;
            list-style: none;
            display: flex;
            align-items: center;
        }

        .slider-indicator li {
            width: 8px;
            height: 8px;
            margin: 4px;
            border-radius: 50%;
            background: #fff;
            opacity: 0.4;
            cursor: pointer;
        }

        .slider-indicator li.active {
            width: 12px;
            height: 12px;
            opacity: 1;

        }
    </style>
</head>

<body>
    <div class="slider">
        <div class="slider-wrapper">
            <img src="./images/slider01.jpg" alt="" />
        </div>
        <div class="slider-footer">
            <p>对人类来说会不会太超前了？</p>
            <ul class="slider-indicator">
                <li></li>
                <li></li>
                <li></li>
                <li></li>
                <li></li>
                <li></li>
                <li></li>
                <li></li>
            </ul>
            <div class="toggle">
                <button class="prev">&lt;</button>
                <button class="next">&gt;</button>
            </div>
        </div>
    </div>
    <script>
        // const arr = [1, 3]
        // arr[0]
        // 1. 初始数据
        const arr = [
            { url: './images/slider01.jpg', title: '对人类来说会不会太超前了？', color: 'rgb(100, 67, 68)' },
            { url: './images/slider02.jpg', title: '开启剑与雪的黑暗传说！', color: 'rgb(43, 35, 26)' },
            { url: './images/slider03.jpg', title: '真正的jo厨出现了！', color: 'rgb(36, 31, 33)' },
            { url: './images/slider04.jpg', title: '李玉刚：让世界通过B站看到东方大国文化', color: 'rgb(139, 98, 66)' },
            { url: './images/slider05.jpg', title: '快来分享你的寒假日常吧~', color: 'rgb(67, 90, 92)' },
            { url: './images/slider06.jpg', title: '哔哩哔哩小年YEAH', color: 'rgb(166, 131, 143)' },
            { url: './images/slider07.jpg', title: '一站式解决你的电脑配置问题！！！', color: 'rgb(53, 29, 25)' },
            { url: './images/slider08.jpg', title: '谁不想和小猫咪贴贴呢！', color: 'rgb(99, 72, 114)' },
        ]

        //  第一步；获取一个随机数，方便查找数组内的元素
        const i = Math.floor(Math.random() * arr.length)
        console.log(i);
        // 直接输出随机取到的这个数组
        console.log(arr[i]);
        console.log('------------------------');

        // 第二部；获取图片
        const img = document.querySelector('.slider-wrapper img')
        console.log(img);
        // 第三步: 修改图片的路径，利用刚刚随机取出来的arr[i]
        // 先通过国img查找她的地址属性src  然后修改成刚刚数组随机出来的对象，再通过对象查找相应的属性，随后更改即可
        img.src = arr[i].url
        //  修改下面背景色，由body和css得知 下边模块的背景色类名是 .slider-footer
        // 获取背景色
        console.log('------------------------');

        const footer = document.querySelector('.slider-footer')
        console.log(footer);
        footer.style.backgroundColor = arr[i].color
        console.log('------------------------');

        // 修改文字 innerHTML
        const p = document.querySelector('.slider-footer p')
        console.log(p);
        p.innerHTML = arr[i].title
        console.log('------------------------');

        // 如何修改li呢:nth -child(arr[i+1])  追加类名的方法 => 元素.classList.add('类名')
        // 第一种方法 
        // 利用css选择器nth来选择一个，由于 i 是 0~8 ，所以要去第一个li就应该在 i 的基础是哪个 + 1
        // 这样就可以直接获取随机的一个 li 
        // 然后我们再单独给这个随机的 li 追加类名即可
        const lis1 = document.querySelector(`.slider-indicator li:nth-child(${i + 1})`)
        lis1.classList.add('active')


        // 第二种方法
        // 先把全部li获取过来，获取过来的li是一个伪数组，有下标。 所以是跟arr数组的下标一样
        // 由于上面已经把下标随机数取出来了，所以可以直接lis[i] 然后直接给lis[i]追加类名即可
        // const lis = document.querySelectorAll('.slider-indicator li')
        // console.log(lis[i]);
        // lis[i].classList.add('active')
    </script>
</body>

</html>
~~~































