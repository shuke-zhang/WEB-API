 #                                                          webAPI第二天

##  定时器

###  开启定时器

1. 基本语法 ： setInterval(函数，时间）=> 参数一是函数，参数二是以ms毫秒为单位 1000毫秒 = 1 秒

2. ~~~js
   // 第一种方法 函数直接写在定时器里面
           setInterval(function () {
               console.log('这是第一种方法');
   
           }, 1000)
   
           // 第二种方法  先声明一个函数
           // 函数不能加括号，如果加了括号就会立即执行
           const fn = function () {
               console.log('这是第二种方法');
   
           }
           setInterval(fn, 1000)
   ~~~

3. setInterval('fn()',1000) => 不推荐这么写

###  关闭定时器

1. 基本语法：我们可以用一个变量来接收定时器的返回值，发现是个数字。清空定时器我们只需要把这个返回值清空即可  ===>  clearInterval（接收定时器返回值的变量）

2. ~~~js
    用上面封装的函数来开启定时器
   let timerId = setInterval(fn, 1000)
           // 我们用一个变量来接受定时器的返回值
           // 打印返回的结果时，发现是一个数字
           console.log(`这是一个定时器返回值${timerId}`);
   		// 此时我们可以关闭第一个定时器
   		clearInterval(timerId)
   ~~~

3. 一般情况下，关闭定时器我们都会添加判断条件

4. 当关闭定时器之后，我们再满足某些条件时又可以开启定时器  ===>   timer3 = setInterval(fn, 1000)

5. 为什么用变量接受定时器时要用 let 而不是const呢？ =>  定时器需要关闭，或者存在多次开启定时器的情况下，存在变量数值的变化 所以用let

6. 拓展小知识点 ===> 未避免出现特殊情况，我们封装函数写在定时器前面

7. ~~~js
   //  将定时器内的函数 封装写在定时器的下面
   // 1. 函数声明，用function声明的函数，会提升到当前作用域的最顶层
           function cb() {
               console.log(123)
           }
           setInterval(cb, 1000)
   
   
           // 2. 表达式定义的函数，用const声明的不会提升，用var声明的变量会提升，赋值不会提升
           var foo = function () {
               console.log(888)
           }
           setInterval(foo, 1000)
   
           // 3. 建议： 我们函数的定义写在定时器的前面
   ~~~

   ###  用户协议倒计时小案列

   ~~~js
   <body>
       <textarea name="" id="" cols="30" rows="10">
           用户注册协议
           欢迎注册成为京东用户！在您注册过程中，您需要完成我们的注册流程并通过点击同意的形式在线签署以下协议，请您务必仔细阅读、充分理解协议中的条款内容后再点击同意（尤其是以粗体或下划线标识的条款，因为这些条款可能会明确您应履行的义务或对您的权利有所限制）。
           【请您注意】如果您不同意以下协议全部或任何条款约定，请您停止注册。您停止注册后将仅可以浏览我们的商品信息但无法享受我们的产品或服务。如您按照注册流程提示填写信息，阅读并点击同意上述协议且完成全部注册流程后，即表示您已充分阅读、理解并接受协议的全部内容，并表明您同意我们可以依据协议内容来处理您的个人信息，并同意我们将您的订单信息共享给为完成此订单所必须的第三方合作方（详情查看
       </textarea>
       <br>
       <button class="btn" disabled>我已经阅读用户协议(5)</button>
       <script>
           // 第一步： 获取这个按钮
           const btn = document.querySelector('.btn')
           // 第二步； 声明一个可以变化的变量，用作倒计时
           let i = 5
           // 第三步； 打开一个定时器，让里面的内容隔着一秒来变化
           let timer = setInterval(function () {
               i--
               // 使用模板字符串来式每次的内容变化
               btn.innerHTML = `我已经阅读用户协议(${i})`
               // 添加判断条件，当i=0的时候打开按钮，定时器关闭
               if (i === 0) {
                   // 关闭定时器
                   clearInterval(timer)
                   // 修改按钮内容
                   btn.innerHTML = '同意'
                   // 打开按钮
                   btn.disabled = false
               }
           }, 1000)
       </script>
   </body>
   ~~~

   ![image-20221008111638382](assets/image-20221008111638382.png)===>	![image-20221008111729993](assets/image-20221008111729993.png)

  ##  事件监听

   ###  事件绑定

1. 基本语法：事件源.addEventListener ('事件动作',函数)

~~~js
<body>
    <button>点击</button>
    <script>
        // 需求： 点击按钮，弹出一个警告框
        const btn = document.querySelector('button')
        const fn = function () {
            alert('点击成功')
        }
        //  click => 点击
        //  语法: 事件源.addEventListener ('事件动作',函数)
        btn.addEventListener('click', fn)             
    </script>
~~~

2. 事件监听有三要素

   - 事件源 ===>  给谁绑定事件 => btn
   - 件类型 ===>   绑定的是什么事件 => click 点击事件
   - 事件处理程序 ===> 解释为我们需要做什么 => 函数

3. 这个函数一开始不执行，当我们事件触发的时候才执行。这个函数也叫做回调函数，==> 回头再调用的函数,把一个函数作为参数，传入到另一个函数中。

4. 广告取消小案列

   ~~~js
   <script>
           // 需求 点击右上角叉叉关闭整个盒子
           // 分析： 点击时 ，给大盒子添加一个样式，display = 'none'，就可以直接消除大盒子了
           // 第一步： 获取这个元素,还有获取大盒子
           const closeBtn = document.querySelector('.box1')
           const box = document.querySelector('.box')
           // 第二步： 绑定事件监听
           closeBtn.addEventListener('click', function () {
               box.style.display = 'none'
           })
       </script>
   ~~~

     点击右上角叉叉就可以关闭整个盒子![image-20221008113745946](assets/image-20221008113745946.png)

   ###  事件类型

####  鼠标事件===>   鼠标触发

1.  click ===> 鼠标点击
2.  mouseenter ===> 鼠标经过
3.  mouseleave ===>  鼠标离开
4.  contextmenu ===> 禁用右键菜单
5.  selectstart ===> 禁用选中
6.  浏览器设置里面还可以禁用js，以达到可以赋值或者右键菜单

####  焦点事件 ===>   表单获得光标

1. focus ===>   或得焦点
2. blur   ===>   失去焦点

####  键盘事件 ===>   键盘触发

1. keydown   ===>   键盘按下触发
2. keyup   ===>   键盘抬起触发

####  文本事件 ===>   表单输入触发

1. input   ===>   用户输入事件 实时更新状态
1. change 事件 当输入的内容发生改变，且键盘按下回车键或者鼠标失去焦点的时候才会触发回调函数

###  事件监听方式onclick

1. 还是比较推荐 addEventListener
2. onclick  同一个元素，绑定同一个事件的时候，后一个事件会覆盖前一个
3. 从语法来看 对像.onclick = 函数 ===>   = 可以理解为赋值，当对同一个对象多次绑定同一事件时，后面的会覆盖前面的
4. addEventListener 在对同一个对象多次绑定时，多个事件都可以生效

~~~js
<script>
        // 所以 以后推荐addEventListener来设置事件的监听
        const btn = document.querySelector('button')

        // old的方式 ： 可以理解为赋值，后一个会覆盖前一个事件
        // 缺陷： 同一个元素，绑定同一个事件的时候，后一个事件会覆盖前一个
        btn.onclick = function () {
            console.log('这是老方法，后面的会覆盖前面的1');

        }

        btn.onclick = function () {
            console.log('这是老方法，后面的会覆盖前面的2');

        }


    //     btn.addEventListener('click', function () {
    //         console.log('这是新方法，可以同时打印1');

    //     })
    //     btn.('click', function () {
    //         console.log('这是新方法，可以同时打印2');

    //     })

    </script>
~~~

###  鼠标经过离开事件

1. 鼠标经过： 对象源.addEventListener('mouseenter',函数）
2. 鼠标离开： 对象源.addEventListener('mouseleave',函数）

~~~js
<script>
        // 获取元素
        const box = document.querySelector('.box')
        // 设置事件
        box.addEventListener('mouseenter', function () {
            console.log('这是鼠标经过');
            box.innerHTML = '来了'
            box.style.backgroundColor = 'red';
        })
        box.addEventListener('mouseleave', function () {
            console.log('这是鼠标离开');
            box.style.backgroundColor = 'skyblue';
            box.innerHTML = null
        })
    </script>
~~~

###  焦点事件

1. 获得焦点： 对象源.addEventListener('focus',函数）
2. 失去焦点： 对象源.addEventListener('blur',函数）
3. 配合input框使用

~~~js
 <script>
        const ipt = document.querySelector('input')
        ipt.addEventListener('focus', function () {
            console.log('这是获得焦点');

        })
        ipt.addEventListener('blur', function () {
            console.log('这是失去焦点');

        })
    </script>
~~~

###  键盘事件

1. 键盘按下： 对象源： .addEventListener('keydown',函数）
2. 键盘抬起： 对象源： .addEventListener('keyup',函数）
3. 所有按键都会生效键盘事件，不管这个按键有没有字符 
4. keydown比我们文字输入到input框要提前一点, 这个回调函数会先执行，然后文字再落入到input框中
       比如按下一个1 它会先输出 键盘按下了 当我再按下一次1之后，它才会打印上一次我按下的值

~~~js
<script>
        // 1. keydown 这个事件的触发，
        // 1. keydown比我们文字输入到input框要提前一点, 这个回调函数会先执行，然后文字再落入到input框中
        // 比如按下一个1 它会先输出 键盘按下了 当我再按下一次1之后，它才会打印上一次我按下的值
        // 2. keydown如果一直按住，会一直执行
         const ipt = document.querySelector('input')
         ipt.addEventListener('keydown', function () {
             console.log('键盘按下了');
             console.log(ipt.value);
         })
         ipt.addEventListener('keyup', function () {
            console.log('键盘抬起了');
            console.log(ipt.value);


        // })
~~~

###  表单输入事件

1. 对象源.addEventListener('input',函数）
1. console.log(ipt.value.length);可以得到输入的值的长度

~~~js
 // 表单输入事件
        ipt.addEventListener('input', function () {
            console.log('表单输入了');
            console.log(ipt.value);
            console.log(ipt.value.length);

        })
~~~

##  随机点名小案列 => BUG版本

1. BUG ===>   当点击开始按钮两次或两次以上时，点击结束按钮并不能结束
2. BUG分析： 由于多次点击开始，点击事件就生效了很多次，同样就会返回很多值，此时如果点击结束，只能结束一次的点击事件，并不能全部结束。

~~~js
<script>
        // 声明一个姓名的数组
        const arr = ['张三', '李四', '王二麻子', '大聪明', '二傻子']
        let timer
        // // 声明一个随机数，作为寻找数组的下标
        // const i = Math.floor(Math.random() * arr.length)
        // console.log(arr[i])
        // 获取需要修改的标签

        const person = document.querySelector('.qs')
        // 可以成功
        // person.innerHTML = arr[i]
        // 给开始按钮添加事件监听
        // 获取开始按钮
        const start = document.querySelector('.start')
        // 添加点击事件
        start.addEventListener('click', function () {
            // 因为每次点击都需要改变随机数，所有随机数放在点击事件里面
            // const i = Math.floor(Math.random() * arr.length)
            // person.innerHTML = arr[i]
            // 添加定时器效果

            timer = setInterval(function () {
                // 声明一个随机数，作为寻找数组的下标
                const i = Math.floor(Math.random() * arr.length)
                person.innerHTML = arr[i]
            }, 100)
        })

        // 结束按钮
        // 获取按钮
        const end = document.querySelector('.end')
        // 给按钮添加点击事件
        end.addEventListener('click', function () {
            // 当发生点击事件时，定时器效果暂停，又因为作用域 所以应该先在外面声明变量，再在开始按钮里面赋值
            // 由于我们把定时器返回值用变量timer接受了，所以我们直接清除timer即可
            clearInterval(timer)       
        })
    </script>
~~~

##  随机点名修复BUG => clearInterval清除定时

1. 在发生每一次点击事件的时候我们都清除一个定时器，确保在点击结束按钮时只有一个定时器效果

~~~js
<script>
        // 声明一个姓名的数组
        const arr = ['张三', '李四', '王二麻子', '大聪明', '二傻子']

        let timer
        const person = document.querySelector('.qs')
        // 开始按钮
        const start = document.querySelector('.start')
        start.addEventListener('click', function () {
            // 清除bug
			clearInterval(timer) 
            timer = setInterval(function () {
                const i = Math.floor(Math.random() * arr.length)
                person.innerHTML = arr[i]
            }, 100)
        })

        // 结束按钮       
        const end = document.querySelector('.end')        
        end.addEventListener('click', function () {            
            clearInterval(timer)       
        })
    </script>
~~~

##  随机点名修复BUG => flag状态亲判定

1. 利用flag 的状态 true  false 来判断是否返回return   
2. 由于点击事件是在函数内，所以可以通过此方法判断是否执行代码
3. 思路具体分析：  ===>   让代码只存在一个定时器
4. 第一步 :  先命名一个变量 let flag = true，
5. 第二步： 在定时事件之前添加一个判断效果，判断flag是不是等于false，如果满足则不执行下面代码return，如果不满足就说明flag的值是true就执行下面的定时器
6. 第三步： 在发生第一次点击事件之后把false赋值给flag flag = false
7. 由于第一次定时器发生之后 flag 的值变成了 false ，根据第二步的判断代码 ，当发生点击时就不会执行定时器效果了
8. 第四步： 在结束按钮点击事件时  flag = true  这样在结束之后，又可以继续点击开始了！

~~~js
<script>
        // 声明一个姓名的数组
        const arr = ['张三', '李四', '王二麻子', '大聪明', '二傻子']
        let timer
        // 修复双击开始按钮时不能结束的bug
        // 使用flag来修复
        let flag = true

        const person = document.querySelector('.qs')
        // 获取开始按钮
        const start = document.querySelector('.start')
        // 添加点击事件
        start.addEventListener('click', function () {

            // 修复bug => 当点击事件发生后，flag由true变成了false
            // 我们可以添加判断条件，使得当flag的值发生改变时，返回函数，不执行下面代码
            if (flag === false) {
                return
            }


            timer = setInterval(function () {
                const i = Math.floor(Math.random() * arr.length)
                person.innerHTML = arr[i]
            }, 100)
            flag = false
        })


        // 结束按钮
        const end = document.querySelector('.end')
        // 给按钮添加点击事件
        end.addEventListener('click', function () {
            clearInterval(timer)
            // 由于我们上面设置了flag = false，所以我们在结束之后想要再次开始随机就不可以
            // 我们在这就可以恢复他的数值，使点击事件可以继续执行
            flag = true
        })
    </script>
~~~

##  随机点名修复BUG => timer修复 跟flag差不多

1.  利用 timer 修复bug分析
2. 我们先在外面声明了一个并没有赋值的变量 timer
3. 此时这个变量timer是没有值的，在经过第一个点击事件之后，它的值被赋值，变成了 1 
4. 如果此时又发生了一次点击，那么值就会变成 2 
5.  我们可以增加一个判断条件,当timer 大于1时就返回return ,不能继续执行点击事件的代码了
6.   然后,我们在结束之后再将0或者null undefined等值赋值给timer ,这样我们又可以继续执行点击事件了 


~~~js
<script>
       
        const arr = ['张三', '李四', '王二麻子', '大聪明', '二傻子', '老大', '老二', '老三', '老四']
        let timer

        // 开始按钮
        const person = document.querySelector('.qs')

        const start = document.querySelector('.start')
        start.addEventListener('click', function () {
            if (timer >= 1) return


            timer = setInterval(function () {
                const i = Math.floor(Math.random() * arr.length)
                person.innerHTML = arr[i]
            }, 100)
        })

        // 结束按钮
        const end = document.querySelector('.end')
        end.addEventListener('click', function () {

            clearInterval(timer)
            timer = undefined

        })
    </script>
~~~

##  随机点名修复BUG => 禁用按钮

1. 利用按钮属性disabled 的状态来修复BUG
2. 在发生第一次点击事件之后，直接生效禁用属性，使按钮禁用，不能再点击
3. 在点击结束按钮之后，改变禁用属性，让其不生效，这样又可以继续点击开始按钮了

~~~js
<script>
        // 数据数组
        const arr = ['张三', '李四', '王二麻子', '大聪明', '二傻子']
        const person = document.querySelector('.qs')
        person.innerHTML

        let timer
        // 1. 左侧按钮
        const start = document.querySelector('.start')


        start.addEventListener('click', function () {
            // 当发生第一次点击事件之后 禁用按钮 按钮就不给点了
            start.disabled = true
            timer = setInterval(function () {
                let i = Math.floor(Math.random() * arr.length)
                person.innerHTML = arr[i]
            }, 50)

        })

        // 2. 右侧按钮
        const end = document.querySelector('.end')


        end.addEventListener('click', function () {
            // 当点击了结束按钮之后，开始按钮要继续可以点
            start.disabled = false
            clearInterval(timer)
        })
    </script>
</body>
~~~

##  随机点名修复BUG => 数组（不推荐）

1. 用一个数组存上每一个定时器的标志，关闭的时候循环遍历，把每一个定时器都关了
2. 先在点击事件之前命名一个空的数组
3. 在每次点击定时器生效之后，将返回的值新增给这个空数组，不管点了几次都新增给这个数组
4. 因为我们把定时器的值给了数组，所以在点击结束按钮的时候，把这个数组循环遍历一遍都删了
5. 不管点击了多少次，我们都删多少次。这样就可以消除BUG，但是不推荐

~~~js
<script>
        // 数据数组
        const arr = ['马超', '黄忠', '赵云', '关羽', '张飞']
        const person = document.querySelector('.qs')
        let arr1 = []

        // 由于函数有局部作用域的原因，所以当结束按钮发生点击事件时它找不到开始按钮的定时器
        // 所以我们要在外面先给定时器设置一个变量，然后再在开始按钮里面赋值
        let timer
        // 1. 左侧按钮
        // 获取左侧按钮
        const start = document.querySelector('.start')
        // 给它添加一个事件
        start.addEventListener('click', function () {

            timer = setInterval(function () {
                let i = Math.floor(Math.random() * arr.length)
                person.innerHTML = arr[i]
            }, 100)
            console.log(timer);
            // 清除双击开始无法暂停bug 思路2
            arr1.push(timer)
        })
        console.log(arr1);

        // 2. 右侧按钮
        // 当点击时直接清除定时器即可
        const end = document.querySelector('.end')
        end.addEventListener('click', function () {
            // 利用这种方法此时清除的就是数组了，因为前面我们把timer赋值给数组了
            for (let i = 0; i < arr1.length; i++) {
                clearInterval(arr1[i])
            }


        })
        // 2. 用一个数组存上每一个定时器的标志，关闭的时候循环遍历，把每一个定时器都关了 不是很推荐
    </script>
~~~

##  随机点名改进版 => 每次点名之后删除

1. 在每次点名时，在点击结束按钮之后删除随机到的那个数，让程序不能重复点击到那个人
2. 点名只剩下最后一个之后，即数组的长度等于 1 之后，禁用按钮，让其不能继续点击按钮

~~~js
 <script>
        // 改进 需求： 每次随机点名之后删除那个数
        // 数据数组
        const arr = ['马超', '黄忠', '赵云', '关羽', '张飞']
        const person = document.querySelector('.qs')
        let i
        let timer
        // 1. 左侧按钮
        const start = document.querySelector('.start')
        start.addEventListener('click', function () {
            // 清除双击开始时结束不了的bug
            clearInterval(timer)
            timer = setInterval(function () {
                i = Math.floor(Math.random() * arr.length)
                person.innerHTML = arr[i]
            }, 100)
            // 添加判断条件 当 arr的长度等于1时禁用按钮
            if (arr.length === 1) {
                // start.disabled = true
                // end.disabled = true
                // 代码可以简写
                start.disabled = end.disabled = true
            }
        })
        // 2. 右侧按钮
        const end = document.querySelector('.end')
        end.addEventListener('click', function () {
            // 当随机到哪个数时删除那个数，但是由于作用域的原因，所以我们得在函数外面声明一个变量 i
            // 然后再在函数里面去给  i 赋值随机数  这样 在结束按钮这里才能找到这个i
            arr.splice(i, 1)
            // 打印看看
            console.log(arr);

            clearInterval(timer)
        })
    </script>
~~~

##  点击轮播图切换版本

1. 注释很详细

~~~js
// 需求： 利用点击事件完成轮播图的变化
        // 分析：设定一个变量，在每次完成点击事件之后 i++
        // 获取需要更改的三个元素
        const img = document.querySelector('.slider-wrapper img')
        const p = document.querySelector('.slider-footer p')
        const footer = document.querySelector('.slider-footer')
        // 设定一个变量
        let i = 0
        console.log(arr[i])

        // 右侧按钮
        const right = document.querySelector('.next')
        // 给按钮添加点击事件
        right.addEventListener('click', function () {
            // i 跟数组的下标一样，所以在每次点击自后 i++ 就可以实现数组内容的更换
            i++

            // 循环，当 i 多次点击 到数组长度之后 让 i = 0 实现循环
            if (i >= arr.length) {
                i = 0
            }
            // 调用函数

            render()

        })

        // 左侧按钮
        const left = document.querySelector('.prev')
        // 给按钮添加点击事件
        left.addEventListener('click', function () {
            // i 跟数组的下标一样，所以在每次点击自后 i++ 就可以实现数组内容的更换
            i--

            // 循环，简写 三元表达式
            // i < 0 ? i = arr.length - 1 : i = i
            i = i < 0 ? arr.length - 1 : i
            // 调用函数
            render()

        })

        // 可以封装一个函数，让左侧按钮跟右侧按钮的公共样式直接用就行
        // 可以变量封装一个匿名函数，也可以直接给函数命名
        function render() {
            img.src = arr[i].url
            p.innerHTML = arr[i].title
            footer.style.backgroundColor = arr[i].color
            //li 的格式的改变，先清除 所有 active ，然后再在每个点击的顺序上添加上 li
            // 获取

            // document.querySelector('.slider-indicator .active').classList.remove('active')
            // document.querySelector(`.slider-indicator li:nth-child(${i + 1})`).classList.add('active')
            // 可以使用变量来接受所获取的元素，这样更好理解
            const xiao = document.querySelector('.slider-indicator .active')
            xiao.classList.remove('active')
            // 添加
            const tian = document.querySelector(`.slider-indicator li:nth-child(${i + 1})`)
            tian.classList.add('active')
        }


        // 添加定时器，让轮播图实现自动播放
        let timerID = setInterval(function () {
            // js原生提供给我们的，自动触发点击事件，直接使用就可以
            right.click()
        }, 1000)
        // 添加鼠标事件监听，鼠标经过大盒子时关闭定时器，鼠标在大盒子外开启定时器
        // 获取最大盒子
        const box = document.querySelector('.slider')
        box.addEventListener('mouseenter', function () {
            // 当鼠标经过大盒子时 清空定时器返回来的值
            clearInterval(timerID)
        })
        // 当鼠标离开时 定时器又重新开始
        box.addEventListener('mouseleave', function () {
            timerID = setInterval(function () {
                // js原生提供给我们的，自动触发点击事件，直接使用就可以
                right.click()
            }, 1000)
        })

~~~

##  全选反选案列

1. 需求：用户点击全选，则下面复选框全部选择，取消全选则全部取消,文字对应变化
2. 点击下面三个小方框，全部选中时，全选按钮选中，文字变化为取消
3. 三个小方框中有一个没有选中则全选方框不会被选中文字变为全选

~~~js
<script>
        // 获取按钮
        const all = document.querySelector('#checkAll')
        const cks = document.querySelectorAll('.ck')
        const span = document.querySelector('.all')
        // 添加点击事件
        all.addEventListener('click', function () {
            // checked 跟表单禁用按钮一样，都可以用布尔值表示状态
            // console.log(all.checked)
            // 获取全部ck过来的是个伪数组，当更改全选按钮时，让他们随着改变
            // 就可以遍历数组来改变
            for (let i = 0; i < cks.length; i++) {
                cks[i].checked = all.checked
            }
            // 优化：all.checked  可以不用直接写true 因为if 真则执行 第一行  false则执行下面的
            // if(判断条件是true还是false){
            // 如果是真则执行这串代码
            // } else {
            // 如果是false则执行这句话
            // }
            //  0 '' null undefind NaN false 都为假  其余为真
            if (all.checked === true) {
                span.innerHTML = '取消'
            } else {
                span.innerHTML = '全选'
            }

        })




        // 利用for给伪数组里面绑定多个事件
        // 当点击其中一个小按钮的时候就需要遍历这三个按钮的状态，方便给全选按钮改变状态
        // 外层循环直接绑定数组里面的事件
        for (let i = 0; i < cks.length; i++) {
            cks[i].addEventListener('click', function () {
                // console.log('hj')
                // 判断 小按钮的状态
                for (let j = 0; j < cks.length; j++) {
                    if (cks[j].checked === false) {
                        // 只要有其中一个没有被选中，则大盒子按钮也不会被选中
                        all.checked = false
                        span.innerHTML = '全选'
                        // 如果有一个没有被选中直接退出函数，所以不用break
                        // 如果用了break则还是会执行外层循环的代码
                        return
                    }
                }
                // 如果三个
                all.checked = true
                span.innerHTML = '取消'
            })
        }

    </script>
~~~

![image-20221008170018553](assets/image-20221008170018553.png)







