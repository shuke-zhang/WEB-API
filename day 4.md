#  web API第四天

##  自定义属性汇总

1. 获取对象属性===> 语法：对象.属性名，如果想要获取类型，对象.className
2. 获取自定义属性===> 1. 对象.dataset.id ，2. 对象.dataset.['id'] , 3. 对象.getAttribute('data-id')
3. 获取元素的属性 ===> 语法：对象 . getAttribute('属性值')，该方法可以获取自定义属性但不推荐，且获取类名时直接书写class即可
4. 添加对象的属性 ===> 语法：对象.setAttribute(属性名, 属性值)===> 同样可以设置自定义属性 对象.setAttribute(data-id, '1'),其他属性也都可以设置
5. 移除元素中的属性 ===> 语法： 对象.removeAttribute(属性名)
6. **如果属性是data-形式的自定属性，建议以dataset来获取！！！**

##  页面滚动事件

1. scroll ===> 页面滚动的事件

2. 语法： 事件源.addEventListener('scroll', function ( ) {  }  )

3. 页面被卷去的头部：document.documentElement.scrollTop ===> scrollTop 被卷去的头部，同时可以作用于对象 ===>用于监听对象被卷去的头部

4. 另外一种页面被卷去的头部写法：window.pageYOffset

5. 对象.offsetTop   获取元素距离最近一级定位父元素的距离，如果父元素都没有定位,获取的就是它离body的距离

6. 对象.offsetLeft 获取的是对象元素左边的距离

7. offsetWidth / offsetHeight  动态获取元素的大小（宽高）===> offsetWidth = width + padding + border

8. offsetWidth和clientWidth的区别， 这个包含border ,clientWidth ==> 不包含border

      

##  立即执行函数

1. 第一种写法：(function(){})() ===>  (function(行参){运行内容})(实参)

2. 第二种写法：(function(){}()) ===>  (function(行参){运行内容}(实参))

3. 注意：多个立即执行函数，我们需要分号隔开，立即执行函数的前面，需要加分号。

4. 作用：可以创建独立空间（作用域）。里面变量不会对外面造成影响，可以将功能代码分模块的编写

5. 如果一个变量没有用var let const 声明，那么它会变成全局变量，挂载到window上，挂载  相当于这个变量成为了window的一个属性

6. 真正会导致上下行解析出问题的情况有 5 个： 小括号，方括号，正则开头的斜杠，加号，减号=> // () [] / + -

7. 一行开头是小括号或者方括号的时候加上分号就可以了，其他时候全部不需要

   ​    

##  获取元素视口的位置

1. getBoundingClientRect() 返回的是一个对象，里面有很多属性
2. div.getBoundingClientRect().x ===> 获取元素距离视口的x轴的距离
3. div.getBoundingClientRect().y ===> 获取元素距离视口的y轴的距离

##  属性选择器

1. 可以利用属性选择器来获取元素

~~~js
 <input type="password">
    <input type="text">
    <input type="text" data-name="andy">
    <input type="text" data-id="1">
    <script>

        // 属性选择器 
        // 1.[]里面加上属性名
        const input = document.querySelector('input[type="password"]')
        console.log(input)

        // 2. []方括号里面属性的引号，可以省略 (如果属性值是字符串形的数字，不能省略)
        const ipt = document.querySelector('input[type=text]')
        // const ipt2 = document.querySelector('[data-id=0]') // Error
        console.log(ipt)

        // 3. 可以直接写属性选择器，前面的标签可以省略
        const ipt3 = document.querySelector('[data-name=andy]')
        console.log(ipt3)


        // 4. 不写属性值，也可以
        const ipt4 = document.querySelector('[data-id]')
        console.log(ipt4)

    // console.log(ipt2)
    </script>
~~~

![image-20221019202835183](assets/image-20221019202835183.png)





















