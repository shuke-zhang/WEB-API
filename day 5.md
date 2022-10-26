#  web API第五天

##  实例化日期对象

###  构造对象

1. 构造对象： 默认首字母大写

2. 构造函数，一定要通过new来调用，如果没有 new ，那么则输出 undefined

3. 可以重复多次调用

4. ~~~js
   function Star(*name*, *age*) {
      this.name = *name*
      this.age = *age*
      *// 这儿的 this 指向的是我们函数所创建的对象*
      *// console.log(this)*
     }
   ~~~

##  实例化日期对象

1. 实例化， 通过构造函数创建对象的过程就叫做实例化 。 实例：实际的，具体的例子（对象）
2. 获取当前时间对象`const date = new Date()` ===>  数据类型是：object
3. 获取指定事件对象`const date2 = new Date('2022-10-13 09:09:36')`
4. ![image-20221012195252417](assets/image-20221012195252417.png)

##  常见的日期对象方法

1.  年 ===> `date.getFullYear()`

2.  月 ===> `date.getMonth() + 1`   取值范围是 0~11。 0表示一月份，以此类推 ，所以得到当前月份的话 需要加1

3. 日 ===> `date.getDate()`

4. 星期几 ===> `date.getDay()`    取值范围是 0~6  ，0表示星期日，1表示星期一，以此类推

5. 小时 ===> `date.getHours()`

6. 分 ===> `date.getMinutes`

7. 秒 ===> `getSeconds`

8. 获取文字的 星期几

9. ~~~js
   const arr = ['星期天', '星期一', '星期二', '星期三', '星期四', '星期五', '星期六']
       // 获取当前日期对象
       const date2 = new Date()
       // 获取当前日期的星期几 取值是0~6
       const i = date2.getDay()
      //将获取到的星期几作为下标，获取数组中的相应元素，就可以得到文字星期几
       const res = arr[i]
       console.log(res)
   ~~~

 ##  date.toLocaleString()来获取时间

1. 语法规范：先获取时间对象，`const date = new Date()`===> `date.toLocaleString()`

2. 这样就可以获取到当前的时间，但是格式是固定的 ===> 2022/10/12 20:14:05

3. 获取当前时间，每一秒都添加案例

4. ~~~js
   //  先获取div这个盒子
       const div = document.querySelector('div')
       // 获取日期对象
       const date = new Date()
       div.innerHTML = date.toLocaleString()
       // 添加定时器
       setInterval(function () {
   
         // 由于这个日期对象获取的是当前的时间，所以要每次都需要获取一下
         const date = new Date()
         div.innerHTML = date.toLocaleString()
       }, 1000)
   ~~~

   

##  利用JS直接获取时间

1. 利用js文件来获得时间

   实际开发：先导入一个JS文件，然后直接书写

     // moment.js  https://momentjs.bootcss.+.com/

     // day.js  https://dayjs.fenxianglu.cn/ ===> 实际开发中更推荐使用这个网站

     console.log(dayjs().format('YYYY/MM/DD HH:mm:ss'))

     // 需要注意字母的大小写，否则会报错

     const res1 = dayjs().format('YYYY-MM-DD HH-mm-ss')

     const res2 = dayjs().format('YYYY/MM/DD HH/mm/ss')

     const res3 = dayjs().format('YYYY/MM/DD HH-mm-ss')

     const res4 = dayjs().format('YYYY/MM-DD HH-mm/ss')

     console.log(res1)

     console.log(res2)

     console.log(res3)

     console.log(res4)

##  时间戳

1. 定义：从当前时间开始到1970/01/01 00:00:00点的毫秒数

###  date.getTime()获取时间

1. 在获取时间对象之后，直接书写date.getTime()
2. 只能获取当前时间，不能传参

###  +new Date()===>更推荐

1. 在获取时间对象之后，直接书写  +new Date()
2. 括号内可以指定时间，比如+new Date('2022-10-20 08:00:00')===> 1970/01/01 00:00:00到2022-10-20 08:00:00之间的毫秒数

###  Date.now()获取时间

1. 只能获取当前时间
2. 在获取时间对象之后，直接书写 Date.now()

###  利用+new Date() 计算时间差

~~~js
const now = +new Date() // 当前时间到1970/01/01 00:00:00点的毫秒数
    const future = +new Date('2022-10-20 08:00:00')
    // 这样就可以得到两个时间之间的毫秒数
    console.log(future - now)
~~~

###  倒计时小案列

~~~js
<script>
    // 封装一个函数
    const time = function () {
      // 获取当前的时间戳
      const temp = +new Date()
      // 获取指定的时间戳  注意需要引号和事件格式
      const newTemp = +new Date('2022-10-13')
      // 获取时间差=> 或得的时间是毫秒 并且转换为秒数
      const res = (newTemp - temp) / 1000
      // 进行秒对于事件的转换 天 时 分 秒
      let d = parseInt(res / 60 / 60 / 24)
      let h = parseInt(res / 60 / 60 % 24)
      let m = parseInt(res / 60 % 60)
      let s = parseInt(res % 60)

      // 5. 补0
      d = d < 10 ? '0' + d : d
      h = h < 10 ? '0' + h : h
      m = m < 10 ? '0' + m : m
      s = s < 10 ? '0' + s : s

      // 6. 将天时分秒分别放到span标签中
      document.querySelector('#day').innerHTML = d
      document.querySelector('#hour').innerHTML = h
      document.querySelector('#minutes').innerHTML = m
      document.querySelector('#second').innerHTML = s

    }
    // 添加定时器效果
    time()
    setInterval(time, 1000)
  </script>
~~~

##  父节点

1. 节点： node ===> 页面上所有的内容都可以叫节点  元素节点/属性节点/文本节点/注释节点
2. 父节点 :node.parentNode  ===> 返回的是最近一级父元素节点.如果找不到则返回null
3. ` console.log(son.parentNode) `  son 的爸爸
4. `console.log(son.parentNode.parentNode) `   son  的爷爷

##  子节点

1. 子节点 ：node.childNodes===> (元素，文本，属性，注释)

2. node.childNodes  返回的是个伪数组，包含了所有节点，包含了文本节点  空格也属于文本节点

3. 节点类型 nodeType ===> 元素节点=1     文本节点=3     注释节点=8

4. 找到元素节点

5. ~~~js
    for (let i = 0; i < ul.childNodes.length; i++) {
         if (ul.childNodes[i].nodeType === 1) {
           console.log(ul.childNodes[i])
         }
       }
   ~~~

##  **子元素**节点（重要）

1. 语法规范：对象.children
2. 返回的是父节点下的所有子元素节点（只是第一级）返回的也是伪数组
3. 第一个子元素节点：node.children[0]
4. 最后一个子元素节点：node.children[ul.children.length - 1] ===> 属性选择器
5. 其他子元素节点用数组下标显示即可

##  子元素兄弟节点

1. 先获取到一个节点，此时我们可以获取到这个节点的上一个或者是下一个节点，兄弟关系
2. node.previousElementSibling ===>  前一个节点
3. node.nextElementSibling ===> 下一个节点

##  节点的增删

###  增加节点

1. document.createElement('新创建的标签名') ===>  只是一个空标签，里面没有内容
2. node.appendChild('要添加的元素') ===>  在父元素的子节点最后一个位置添加元素
3. 父元素.insertBefore(我们要插入的元素，插入的位置) ===> 可以指定位置添加，在参数二的前面添加

###  克隆节点

1. 语法规范： const dupNode = node.cloneN0de( ) ===>  只能复制标签，不能复制内容
2. 括号可以传参，默认是 false 表示只复制标签，不复制内容。true 表示即复制标签也复制内容
3. 应用：比如轮播图。把第一个复制到最后一个，以完成无缝衔接

###  删除节点

1. 语法：父元素.removeChild(要删除的节点)

2. 一般情况下删除的是父元素的某一个子节点

3. 要删除的节点只能是父元素的最近一层的节点 ， 亲儿子

4. 只能删除父元素的最近一层的子元素（节点）

   

##  移动端事件

   ~~~js
   <script>
       const div = document.querySelector('div')
   
       // 移动端的这几个事件，一定要记得切换 移动端的模式
       div.addEventListener('touchstart', function () {
         console.log('手指触摸到DOM元素了')
       })
   
       // 按住移动 touchmove  (mousemove===> 鼠标移动事件)
       div.addEventListener('touchmove', function () {
         console.log('手指在dom元素上移动')
       })
   
       // 手指在dom元素上抬起的时候触发
       div.addEventListener('touchend', function () {
         console.log('手指在dom元素上移开')
       })
     </script>
   ~~~



   













