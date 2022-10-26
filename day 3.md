#  web API 第三天

##  事件对象e.target

1. 事件对象： 当事件发生的时候，和这个事件相关的所有信息，都存在这个对象里，里面有很多属性 ==> 这个对象就是事件对象
2. 书写位置： 绑定事件的时候，回调函数的第一个参数（行参），简写为e（事件英文 => event 简写）
3. btn.addEventListener('click', function (*e*) {     })
4. e.type  事件类型 click keyup 比如点击事件则 type就是click
5. e.target  触发事件的元素，我们点的是谁，谁触发的这个事件 
6. e.target.tagName 触发事件元素的标签名，如我们给button绑定点击事件，则这个属性就会输出 BUTTON 是大写字母
7. className 类名 
8. nodeName 节点名
9. e.key   按的是哪个键，更推荐使用key来判断
10. e.keyCode ASIIC码，也可以判断我们按下的是哪个键，但是不推荐。部分浏览器已经取消改代码了但是为了老代码的兼容性，还可以用，这个不推荐
11. e.currentTarget 绑定事件的元素 ，元素里面的所有内容

 ##  回调函数

1. 回调函数： 把一个函数作为参数，传入到另一个函数中，这个函数就叫回调函数。===> 开始不执行，回头再调用的函数
2. 本质上：回调函数就是一个普通的函数，只是把它作为参数传到另一个函数里面了
3. 注意： 在回调函数里面不能加（） 如果加了，函数就会立即执行
4. 目前我们遇到的回调函数只有     **定时器**  和    **事件监听** 

 ##  this变量

1. this的指向 => 全局变量中，this指向的就是window   指向 ===> 理解为等于、代表

2. 目前分为几种 

3. 普通函数 function fn() {    console.log(this)  } 普通函数，指的就是window

4. 函数作为对象的方法调用 ===>   指向的就是对象

5. ~~~js
   const obj = {
               name: '练练',
               sing: function () {
                   console.log(this.name)
   
               }
           }
           // 相当于obj调用这个sing这个方法，sing里面的this就指向obj
           obj.sing()
   ~~~

6. 事件绑定的时候，this指向事件源 （绑定事件的元素）

7. 定时器里面 this 指向的就是 window   

8. this在定义的时候，不能确定它的指向，一定是调用执行的时候才能确定！！！
 ##  forEach

1. 语法：arr.forEach(fn)

2. 遍历数组，让数组的每个元素，都执行一遍这个fn

3. function可以接受两个参数function( el , i ),el =>数组里面的所有的元素, i => 数组中每个元素的索引,不省略的话，i则输出全部下标

   

## CSS 伪类选择器

~~~js
<script>
    // 需求，在选中input按钮，再点击button时，打印所有被选中的input框
    // 获取按钮
    const ipt = document.querySelectorAll('.ck')
    const btn = document.querySelector('button')

    btn.addEventListener('click', function () {
        //  .ck:checked   ===>  input框里面都有默认的checked ，但是她的属性不是.ck:checked
        // 只有在选中input时 input里面的属性checked才是.ck:checked 
        // 所以获取这个属性的时候就可以获取到input
        const btns = document.querySelectorAll('.ck:checked')
        console.log(btns)

    })
</script>
~~~

   ##  事件流

1. 事件流：指的是事件在执行过程中的流动路径

2. 三个阶段：1.捕获阶段：从外到内=> 2.处于目标阶段=> 3.事件冒泡阶段：从内到外

 ###  事件捕获

1. **useCapture* **==>是否使用捕获，它是一个boolean 可以是true或者false,默认不传就是false 

2. addEventListener('click', fn, useCapture)

3. document  ->  html -> body -> father -> son   ===> **从外到内**

4. ~~~js
    // 事件捕获：addEventListener第三参数为 true
           son.addEventListener('click', function () {
               console.log('我是子盒子,我被点击了')
           }, true)
      
           father.addEventListener('click', function () {
               console.log('我是父盒子, 我被点击了')
           }, true)
      
           body.addEventListener('click', function () {
               console.log('我是body, 我被点击了')
           }, true)
      
           html.addEventListener('click', function () {
               console.log('我是html, 我被点击了')
           }, true)
      
           document.addEventListener('click', function () {
               console.log('我是document, 我被点击了')
           }, true)
   ~~~

5. ![image-20221014150623040](assets/image-20221014150623040.png)

###  事件冒泡

1. 从最具体的元素（文档树中最深的节点）开始触发，然后向上传播至没有那么具体的元素（文档）
2. addEventListener的第三个参数，如果为false或者不传，表示事件冒泡
3. 事件冒泡： son ->  father -> body -> html -> document

 ###  阻止事件冒泡

1. 阻止事件冒泡， 阻止我们事件往上继续传播，并不会不会阻止代码的执行。

2. 语法：e.stopPropagation()   ===> 需要给事件函数添加 e

3. 注意：如果给相同事件源添加相同事件类型，e.stopPropagation，他并不会阻止第二个事件的执行

4. 另外一种写法 ：*e*.stopImmediatePropagation()，这种写法同样是阻止事件冒泡，同时不会阻止默认行为

5. 但是 如果给相同事件源添加相同事件类型，如果给第一个事件添加*e*.stopImmediatePropagation()，那么第二个事件就不会执行了，他会阻止代码的执行

 ###  阻止默认行为

1. 运用情况：a标签的默认行为,点击之后,会自动跳转,我们可以添加此代码给他禁止跳转
2. 语法： **e.preventDefault()** ===> 同样它不会阻止代码的执行

   ###  事件解绑

1. 当我们想要回调函数里面的代码只执行一次时，就可以使用事件解绑

2. 传统的方式 ===>  btn.onclick = null

3. 注意：会执行事件内的代码，但是只能执行一次事件

4. ~~~js
   btn.onclick = function(){
             console.log('点击了')
             btn.onclick = null // 事件解绑的代码，放到函数内部，函数内部代码先执行一次
             console.log('6666')
           }
   ~~~

5. 事件监听的方式

6. 必须利用声明式或者表达式来命名函数，匿名函数不会解绑事件，且这个代码需要写到函数里面

7. ~~~js
   const cb = function () {
               console.log('事件监听的方式')
               // 这是一种写法
               btn.removeEventListener('click', cb)
           }
           btn.addEventListener('click', cb)
           // 3. 如果事件监听，写的是匿名函数，没法解绑
           // 因为解绑的时候，需要传入函数名字，匿名就不知道解绑哪个函数了
           btn.addEventListener('click', function () { })
   ~~~

###  鼠标经过事件的两种方式

1. mouseenter / mosueleave ===> 没有事件冒泡
2. mouseover / mouseout===> 有事件冒泡

 ##  事件委托

1.  事件委托：把事件委托给别人，代为处理

2. 事件委托的原理； 利用事件的冒泡原理，将事件监听绑定在父元素上，通过父元素监听子元素的事件

3. 事件委托的作用 ； 减少事件注册的次数，提高程序的性能

4. 当我们使用了事件委托的方式注册事件，一般情况下，我们都需要去判断一下点击的是哪个元素===>所以我们需要传参e

5. e.target 触发事件的元素，e.target.nodeName 节点名字  ，e.target.tagName 事件源标签名，e.target.className 类名

6. e.currentTarget 绑定事件的元素 ===> 父元素

   

   




​      

   

   
