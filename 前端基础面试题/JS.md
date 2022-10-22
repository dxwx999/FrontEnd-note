### 1、var、let、const的区别

1、var存在变量提升，而let和const没有(let和const存在暂时性死区)

2、作用域的限制，var声明的变量具备函数作用域的特点，在函数内部声明的变量只能在函数作用域内部使用，在函数外部不能访问。但是，在函数内部可以访问函数外部的全局作用域中的变量。而let和const受当前作用域的限制

3、重复声明，var声明变量可以重复，let和const不可以

4、const声明的是常量，并且不能更改，且一定要有初始值，否则会报错；不能更改，但是可以更改对象或者数组的内部属性

### 2、变量提升和函数提升

-   console.log(a);  //undifined

    var a = 1;   

-   for(var i = 0; i<=3; i++){

     setTimeout(()=>{

  ​    console.log(i);   // 4 4 4 4

     });

    }

-   for(leti = 0; i<=3; i++){

     setTimeout(()=>{

  ​    console.log(i);   // 0123

     });

    }

-   for(var i = 0; i<=3; i++){

     setTimeout(((function(){console.log(i);}))(i),1000) //立即执行函数0123

    }

- 注意:如果函数和变量重名则函数提升的优先级更高

### 3、JS的运行机制

##### 1、关于JavaScript

​	JavaScript是一门单线程语言，单线程就意味着，所有任务都需要排队，前一个任务结束才会执行下一个任务，如果前面任务耗费的时间很长，那么后面的任务就会一直等着，这样很明显会造成资源分配的浪费。

所以JavaScript语言设计者为了规避这个问题，把JavaScript这边所有的任务都分成两种，同步任务和异步任务

###### 同步任务：

- 在主线程上排队的任务，前一个任务执行完毕，才能执行下一个任务

###### 异步任务

- 不进入主线程，是进入任务队列的任务，只有任务队列通知主线程，某个异步任务可以执行了，任务才会进入主线程去执行

##### 2、JavaScript的事件循环(EventLoop)

###### 先执行同步操作，异步操作排在事件队列里的

- 先判断是同步还是异步任务，同步任务就进入主线程，异步任务就进入Event Table
- 异步任务在Event Table中注册事件，当满足触发条件时，就会被推入到Event Queue
- 同步任务进入主线程中执行，当主线程空闲时，才会去Event Queue中看是否有需要执行的异步任务，如果有，就推入主线程中执行

##### 3、宏任务和微任务

###### 异步任务分为:宏任务和微任务

那么说明是宏任务和微任务呢？

###### 宏任务:

setTimeout、setInterval、整体代码script

###### 微任务:

promise().then       promise为同步任务只有then是异步操作

##### 4、讲解

- 1、先执行同步任务，按照顺序一步步来
- 2、然后开始执行异步任务，异步任务开始执行时候，会将异步任务放入事件表格(EventTable)中，当满足了某些条件（比如这里的条件就是0ms和100ms）之后，就会从事件表格中注册到事件队列(EventQueue)，当第一步中的同步事件完成了，才会从事件队列中获取任务去执行

##### 5、总结

​	1、同步先执行，异步后执行

​	2、遇到new Promise 直接执行，then中的方法直接放入微任务队列中

​	3、遇到setTimeout放入宏任务队列中

​	4、执行顺序：同步->微任务(promise里面的then)->宏任务(setTimeout)

### 4、this指向问题

​	1、普通函数：谁调用它就指向谁

​	2、箭头函数：与外部作用域的指向相同

### 5、call、bind、apply三者的区别

##### 	共同点：

- 改变this指向

##### 	不同点：

- call和apply唯一的区别就是传参时，call按顺序传值，而apply需要用数组包起来传值

- bind和call以及apply的区别是bind无法立即执行，而call和apply是立即执行

    var a = 1;

    function fn1(){

     var a =2;

     console.log(this);

     console.log(this.a+a);

    }

    function fn2(){

     var a =10

     fn1()

    }

    fn2();

    var Fn3=function(){

     // this.a=3  //输出5

    }

    Fn3.prototype={

     a:4  //输出6

    }

    var fn =new Fn3();

    fn1.call(fn)

### 6、JS数据类型

- 基本数据类型：undifined,number,null,string,symbol,boolean(unnssb)
- 引用数据类型:   object,array,function(数组和函数也是属于对象)
- NaN是什么类型？number，但是不是一个具体的数字
- null和undifined的区别？
  - null转化为Number是0 （空指针转化为0）
  - undifined转化为Number是NaN
- Symbol可以设置一个独一无二的属性值，可以在Symbol中定义名称，无实际意义Symbol('test'),  不是构造函数不可以new，可以转成字符串和布尔值，不能转成数字



### 7、如何判断数据类型

- typeof
  - 缺点：在判断null和array和object都显示object
- Object.prototype.toString.call()
  - 可以正确显示数据类型

### 8、说说对Object .defineProperty的理解

- 添加属性

  -    let obj={}

      Object.defineProperty(obj,"a",

      {value:1,

      writable:true,     //可修改的

      enumerable:true,   //可枚举

      configurable:true}); //可配置的（添加了才可以删除）

      obj.a=2  //添加了writeable:true才可以修改

      delete obj.a;  //添加了configurable:true才可以删除

      console.log(obj);

      console.log(Object.keys(obj)); //添加了enumerable:true才可以枚举

  -   let obk={}

      Object.defineProperty(obk,'a',{

       get:function(){    //设置了get和set就无法设置value和writable

    ​    console.log('obk的a被获取了');

    ​    return 123;

       },

       set:function(){

    ​    console.log('obk的a被赋值了');

       }

      })

      obk.a='1'

      console.log(obk.a);

  -   let obj2={

       a:123

      }

      let des=Object.getOwnPropertyDescriptor(obj2,"a")  //平常定义的对象自带这四个属性

      console.log(des);

    - *{value: 123, writable: true, enumerable: true, configurable: true}*

    - 1. **configurable**: true
      2. **enumerable**: true
      3. **value**: 123
      4. **writable**: true
      5. [[Prototype]]: Object

### 9、数组去重的方法

-   const arr = [1,3,5,7,1,2,3,3,5,7]

    const newArr=arr.filter((it,index,list)=>list.indexOf(it)===index)

    console.log(newArr);

  - 第一种方法的原理就是获取到当前项的第一个索引，并且保存下来

-   const newArr1=[...new Set(arr)];

    console.log(newArr1);

  - 第二种方法的原理就是利用ES6新增的set集合方法自动去重

-   const  arr=[

     {name:'小红'},

     {name:'小明'},

     {name:'小红'},

     {name:'小红'}

    ]

    const obj={}

    const newArr=[]

    for(let i = 0;i<arr.length;i++){

     if(!obj[arr[i].name]){

  ​    newArr.push(arr[i])

  ​    obj[arr[i].name]=true

     }

    }

    console.log(newArr);  //

  1. **0**: {name: '小红'}
  2. **1**: {name: '小明'}
  3. **length**: 2

-   const  arr=[

     {name:'小红'},

     {name:'小明'},

     {name:'小红'},

     {name:'小红'}

    ]

    const obj={}

    const newArr=arr.reduce((pre,curr)=>{

     if(!obj[curr.name]){

  ​    obj[curr.name]=true

  ​    pre.push(curr)

     }

     return pre

    },[])

    console.log(newArr);



-   const  arr=[

     {name:'小红'},

     {name:'小明'},

     {name:'小红'},

     {name:'小红'}

    ]

    const obj={}

    const newArr=arr.reduce((pre,curr)=>{

     if(!obj[curr.name]){

  ​    obj[curr.name]=true

  ​    pre.push(curr)

     }

     return pre

    },[])

    console.log(newArr);



-   const arr1=[

     {id:1},

     {id:2},

     {id:3},

     {id:4}

    ]

    const arr2=[

     {id:3},

     {id:4}

    ]

    const isOther=(x,arr)=>{

     for(let i = 0;i<arr.length;i++){

  ​    if(x==arr[i].id){

  ​     return false

  ​    }

     }

     return true

    }

  

    const newArr=arr1.filter((it)=>isOther(it.id,arr2))

    console.log(newArr);

### 10、slice substr substring splice split用法

- ##### slice:

  -   const str="1234"

      const arr=[1,2,3,4]

      console.log(str.slice(0,2)); //12  表示从第一个索引开始截取到第二个索引(不包含第二个索引)

      console.log(arr.slice(0,2)); //[1,2] 表示从第一个索引开始截取到第二个索引(不包含第二个索引)

      console.log(str.slice(-2)); //34  只有一个索引且为负数表示倒着截取到结束

      console.log(str.slice(1)); //234  只有一个索引且为正数表示从索引处(包含索引)截取到结束

- ##### substr和substring

  -   console.log(str.substr(1,3));//234  第一个参数表示开始截取的位置，第二个参数表示截取的个数

      console.log(str.substring(1,3));//23 第一个参数表示开始截取的位置，第二个参数表示截取结束的位置(不包含)

- ##### splice

  -   const arr=[1,2,3,4]

  -  截取===单独第一个参数，表示截取参数后面所有的数

    -  const dur=arr.splice(2)

        console.log(dur);//34

        console.log(arr);//12  原数组被改变

  - 删除==第二个参数

    -   arr.splice(2,2) //第二个参数表示删除的个数

        console.log(arr);//12  原数组被删除

  - 增==第二个之后的参数都表示增，在第一个参数的索引值之前

    -   arr.splice(2) //第二个参数表示删除的个数

        console.log(arr);//122234  原数组被删除

- ##### split

  -   const str="1,2,3,4"

      const newStr=str.split(',')

      console.log(newStr); //['1','2','3','4']

- ##### 总结：

  - slice substr substring splice可以用来截取
  - split用来分割字符串成数组
  - slice可以对字符串和数组操作
  - substr substring只能对字符串操作
  - splice只能对数组，并且可以改变原数组的值，其他四个原数组不变



### 11、sort用法

- 默认排序—并不能得到想要的顺序

  -   //sort用法

      const arr1=["ab","a","bc","dd"]

      const arr2=[1,2,11,3]

      console.log(arr1.sort()); //a ab bc dd

      console.log(arr2.sort()); //1 11 2 3

    

  - 设置参数a-b 从小到大，b-a为从大到小  

    console.log(arr2.sort((a,b)=>{ //1 2 3 11

       return a-b

      })); 

  -   var objArr=[

       {name:'小明',

    ​    num:140

       },

       {name:'小明1',

    ​    num:40

       },

       {name:'小明2',

    ​    num:80

       }

      ]

      console.log(objArr.sort((a,b)=>{  //数组排序也可以同样使用，但是要确定要具体值

       return a.num-b.num

      }));

### 12、总结JS数组中自带的方法

 const arr=[11,2,3,4]; //使用数组

##### 1、toString

- 将数组转化为字符串

-   console.log(arr.toString());//11,2,3,4

##### 2、join

- 也是将数组变成字符串，但是可以自定义分隔符

-   const newArr=arr.join(',,')

    console.log(newArr);//11,,2,,3,,4

##### 3、sort

- 对数组进行排序

-   console.log(arr.sort((a,b)=>{  //[2, 3, 4, 11]

     return a-b  //从小到大排序

    }));

##### 4、reverse

- 把数组反转
- console.log(arr.reverse()); //[4, 3, 2, 11]

##### 5、push

- 在数组的末尾添加

-  arr.push(1,2,3,4)

   console.log(arr);//[11, 2, 3, 4, 1, 2, 3, 4]

##### 6、pop

- 从后往前删除数组最末尾的一个索引

-   arr.pop()

    arr.pop()

    console.log(arr);//[11, 2]

##### 7、shift

- 从前往后删除数组中第一个索引

-   arr.shift()

    arr.shift()

    console.log(arr);//[3, 4]

##### 8、concat

- 用于连接两个或多个数组，但是不改变原数组

-   const arr=[11,2,3,4];

    const arr2=[5,1,2,67];

    console.log(arr.concat(arr2)); //[11, 2, 3, 4, 5, 1, 2, 67]

    console.log(arr);//[11, 2, 3, 4]

    console.log(arr2);//[5, 1, 2, 67]

    console.log(arr.push(...arr2)); //[11, 2, 3, 4, 5, 1, 2, 67] //push也可以连接两个数组但是会改变原数组

##### 9、slice(start,end)

- 截取数组中的元素，不改变原数组，从start开始，截取到end(不包含end)

-   console.log(arr.slice(1,3));//[2,3]

    console.log(arr);[11,2,3,4] //不改变原数组

##### 10、splice(start,delcount,insert...)

- 对数组进行增删改查，会改变原数组

-   console.log(arr.splice(1)); //[2,3,4] //从start截取到最后

    console.log(arr); //[11] 会改变原数组

-   console.log(arr.splice(1,2)); //[2,3] 从start截取delcount个数

    console.log(arr); //[11,4]

-   arr.splice(1,0,3,3,5,6) //从start的前面插入insert的值，截取的位数为0，不截取，单纯插入

    console.log(arr); //[11, 3, 3, 5, 6, 2, 3, 4] 

##### 11、indexOf和lastIndexOf

- 得到首次出现的索引和最后出现的索引

-   const arr=[11,2,3,4,11];

    console.log(arr.indexOf(11));//0

    console.log(arr.lastIndexOf(11));//4

##### 12、every

- 判断数组中每一个元素是否满足条件，全都满足则返回true

-   const arr=[11,2,3,4,11];

    const flag=arr.every((it)=>{

     return it>0

    })

    console.log(flag);//true

##### 13、some

- 判断数组中是否存在元素满足条件，有则返回true，否则false

-   const arr=[11,2,3,4,11];

    const flag=arr.some((it)=>{

     return it===12

    })

    console.log(flag); //false

##### 14、filter

-   const arr=[11,2,3,4,11];

    const newArr=arr.filter((it)=>{

     return it===11

    })

    console.log(newArr); //[11, 11]

##### 15、map

- 对数组中的每一项进行加工，也可以转成对象

-   const arr=[11,2,3,4,11];

    const obj=arr.map((it)=>{

     return{

  ​    num:it

     }

    })

    console.log(obj);

### 13、深入讲解reduce

- 累加器,pre表示上一个返回值，curr表示当前项，index表示当前索引，最后的0为初始值

-   //累加器

    const arr=[11,2,3,4,11];

    const sum=arr.reduce((pre,curr,index)=>{

     return pre+curr

    },0)
    
    console.log(sum);  //31
    
-    //筛选最大值

     const arr=[11,2,3,4,15];

     const max=arr.reduce((pre,curr,index)=>{

  ​    return Math.max(pre,curr)

     })

     console.log(max); //15

-    //数组去重

     const arr=[11,2,3,4,15,2,15,3];

     const newArr=arr.reduce((pre,curr,index)=>{

  ​    pre.indexOf(curr)===-1 && pre.push(curr);

  ​    return pre;

     },[])

     console.log(newArr);//[11,2,3,4,15]

- //二维数组转一维数组、 多维转一维用递归

  ​	const arr2=[[1,2],[3,4],[5,6],[7,8]]

     const newArr=arr2.reduce((pre,curr,index)=>{

  ​    return pre.concat(curr);

     },[]) 

     console.log(newArr);//[1, 2, 3, 4, 5, 6, 7, 8]	

- ##### 总结：当你需要将前面数组项遍历产生的结果与当前遍历项进行运算，这时候就可以使用reduce 

### 14、箭头函数

- ES6允许使用=>来定义函数,左边一个参数()可以省略,右边一句表达式{}可以省略，返回对象需要用()括起来

- ##### 注意点：

  - 箭头函数是匿名函数，没有自己的this,arguments
  - 可以用展开运算符解构取到，arguments的值(...xxx)=>{xxx}
  - 箭头的指向和父级指向相同，无法用bind，call，apply改变

### 15、闭包应用场景：防抖和节流

##### 1、闭包的特点：

- (1)函数嵌套函数
- (2)内部函数引用外部函数变量，内部函数对象创建了，此时形成了闭包
- 

​	

### 16、Promise

#### 1、Promise.all,promise.allsettled,promise.any,promise.race的区别

- Promise.all用于多个promise实例，只有参数里面所有的promise都是成功的，才会触发成功，一旦有一个返回失败，或者异常就会触发失败(.catch)====全部成功结束，一起返回

  - ```js
        const p1 =()=>{
          return  new Promise((resolve,reject)=>{
          setTimeout(()=>{
            reject("p1失败")
            throw new Error
          },3000)
        })
        }
        const p2 =()=>{
         return  new Promise((resolve,reject)=>{
          resolve("p2")
        })
        } 
    
        Promise.all([p1(),p2()])
          .then((res)=>{console.log(res);})
          .catch((err)=>{console.log(err);})
    ```

- Promise.allsettled用于多个promise实例，等所有promise都已经确定状态，返回一个promise(不管成功状态还是失败状态)========全部结束，一起返回(不论成功失败)



- promise.any接收一个promise对象集合，当其中一个promise成功，就返回成功的那个，只返回首先成功的，谁先成功谁先返回，如果没有成功则返回AggregateError: All promises were rejected==========只要成功，立马返回

  - ```js
        const p1 =()=>{
          return  new Promise((resolve,reject)=>{
          setTimeout(()=>{
            reject("p1失败")
            // throw new Error
          },3000)
        })
        }
        const p2 =()=>{
         return  new Promise((resolve,reject)=>{
          reject("p2")
        })
        } 
    
        Promise.any([p1(),p2()])
          .then((res)=>{console.log(res);})
          .catch((err)=>{console.log(err);})  //AggregateError: All promises were rejected
    ```

- Promise.race接收一个promise对象集合,当执行完毕就返回，不管成功还是失败

  - ```js
       const p1 =()=>{
          return  new Promise((resolve,reject)=>{
          setTimeout(()=>{
            reject("p1失败")
            // throw new Error
          },3000)
        })
        }
        const p2 =()=>{
         return  new Promise((resolve,reject)=>{
          reject("p2")
        })
        } 
          
        Promise.race([p1(),p2()])
          .then((res)=>{console.log(res);}) 
          .catch((err)=>{console.log(err);})   //p2
    ```

  - 



#### 2、promise的三种状态

- pending,fulfilled,rejected

  - pending->fulfilled

  - pending->rejected

  - 1、promise对象不受外界影响，一旦状态改变就不会再次改变

  - 2、没有抛出异常(throw new Error())，虽然也会执行catch中的语句但是promise的状态仍然为fulfilled

  - 3、只要执行的语句中抛出了异常，那么promiseState就会变成rejected

  - ```js
        const p1 = new Promise((resolve,reject)=>{
          resolve("成功")
        })
        .then((res) =>{
          console.log(res); //promiseState:rejected
          throw new Error()
        })
        .catch((err)=>{
          console.log(err+'err');  //promiseState:fulfilled
        })
        console.log(p1);
    ```

  - 



### 17、async和await的用法

```js
function request(num){
      return new Promise((resolve,reject)=>{
        setTimeout(()=>{
          resolve(num*3)
        },2000)
      })
    }
    //用同步的方式来执行异步操作,虽然操作还是异步,但是执行方式看起来像异步
    async function fn(){
      const res=await request(1);//await会等待执行完后再进行下一步
      const res1=await request(res)
      await setTimeout(()=>{
         console.log('124');
      },0)
      console.log('1'); 
      console.log(res1);
    }
    fn()


    // 回调地狱
    // request(1).then((res)=>{
    //   request(res).then((res)=>{
    //     console.log(res);
    //   })
    // })
```

```js
    // let wtf=fetch('http://119.3.122.177/jquery-3.5.1.min.js').then((text)=>{
    //   console.log(text);
    // })
    // console.log(wtf);

    // async function f(){
    //   const response = await fetch('http://119.3.122.177/jquery-3.5.1.min.js');
    //   const json = await response.text()
    //   console.log(json);
    // }
    // f()


    async function f(){
      const promiseA = fetch('http://119.3.122.177/jquery-3.5.1.min.js')
      const promiseB = fetch('http://119.3.122.177:3000/check/music?id=33894312')
      const [a,b]= await Promise.all([promiseA,promiseB])
      const json=await b.json()
      const text=await a.text()
      console.log(json);
      console.log(text);
    }
    f()
```

### 18、map、for、forEach、for...in、for...of的用法

- map

  - ```js
        //map的使用方法，把数组修改成自己想要的数据类型
        //举例，可以将后端调用过来的数据修改成自己想要的格式
        const arr = [1,2,3]
        const newArr = arr.map((it)=>{
          return  {num:it}
        })
        console.log(newArr);/* 0: {num: 1}
                               1: {num: 2}
                               2: {num: 3} */
        console.log(arr);   // [1, 2, 3]
    ```

- forEach

  - ```js
        //和for一样，但是不能用break、continue中断循环，但是可以用return返回控制，for不行
    	//for可以控制开始循环的索引,forEach必须从0开始
        const arr=[1,2,3]
        arr.forEach((it,index,list)=>{
          if(it==2){
            return;
          }
          console.log(it,index,list);   //1 0  [1, 2, 3]
                                        //3 2  [1, 2, 3]
        })
    ```

- for...in

  - ```js
       //for...in一般用于遍历对象或者数组中的键名和索引值
          	//for in 是获取到可枚举的对象(包括原型链上的属性)
          	const obj={
          num1:1,
          num2:2,
          num3:3,
          num4:4
        }
          
        for (let key in obj){
          console.log(key);//num1 num2 num3 num4
        }
    ```

- for...of

  - ```js
         //for of用于遍历数组中的键值  for in用于遍历对象或者数组中的索引值，键名
      	const arr=[1,24,51,1,24,412]
        for(let key of arr){
          console.log(key); /*1
                              24
                              51
                              1
                              24
                              412 */
        
        }
    ```



### 19、事件冒泡和事件代理(委托)

- 事件冒泡

  - ```js
      <div onclick="fatherFun(event)">
        <div onclick="childFun(event)">测试</div>
      </div>
      
      <script>
        function fatherFun(){
          alert('父级事件触发了')
      
        }
        function childFun(e){  
          alert('子级事件触发了')
          console.log(e);
          e.cancelBubble=true   //第一种方法，支持ie，虽然ie已经不在了
          e.stopPropagation()   //标准方法
          // stopBubble(e)
        }
       
      </script>
    ```

- 事件委托

  - ```js
      <ul onclick="ulFun(event)">
        <li data-id="1">1</li>
        <li data-id="2">2</li>
        <li data-id="3">3</li>
        <li data-id="4">4</li>
      </ul>
      
      <script>
        function ulFun(e){
          console.log(e.srcElement.dataset.id);  //ie
          console.log(e.target.dataset.id);  //火狐    chrome两种都支持
        }
      </script>
    ```

### 20、sessionStorage、localStorage、cokkie的区别

- 相同点:都存储在客户端

- 不同点:

  - 1、存储时间不同：

    - localStorage(本地存储)存储持久的数据，浏览器关闭，数据也会一直存在，除非手动删除
    - sessionStorage(会话存储)浏览器关闭就会删除 数据
    - cookie过期时间之前一直有效，即使窗口关闭也有效

  - 2、存储大小不同

    - localStorage、sessionStorage存储大小是5M或者更大
    - cookie存储大小是4k或者更大
    - 不同浏览器存储大小不同

  - 3、数据与服务器之间的交换方式

    - cookie的数据会自动传递到服务器，服务器端也可以写cookie到客户端

    - localStorage、sessionStorage不会自动把数据传递给服务器，仅在本地保存

    - 同个网站中所有的页面共享一套 cookie

    - ```js
      ```

### 21、原型链



### 22、indexOf和includes用法

- indexOf(element)

  - 字符串或者数组中查找某个元素的位置，如果存在，则返回索引值，如果不存在则返回-1

- includes(element,start)

  - 字符串或者数组中是否存在某个元素，如果存在，则返回true，不存在则返回false，
  - start: 从左向右搜索，也可以是负数，表示从右到左过来的第几个，但是不改变搜索的方向，搜索方向还是从左到右

	- ```js
    <script>
      const str1 = '1afsjasasf'
      const arr1 = [1,2,3,4,5,6]
      console.log(str1.indexOf(1));  //0
      console.log(str1.indexOf('asa'));
    
      console.log(arr1.indexOf(1)); //0
      console.log(arr1.indexOf("b")); -1
    
      console.log(str1.includes(1)); //true
      console.log(str1.includes('afs')); //true
    
      console.log(str1.includes(1,'2')); //false
      console.log(str1.includes(1,'-2')); //true
    </script>
  ```
 ```js
      const obj1={
        a:1,
        b:undefined,
        arr:[1,2,4],
        fun: ()=>{},
      }
      const obj2=obj1
      obj2.a=2
      console.log(obj1,obj2); //{a: 2} {a: 2}  //正常情况下赋值为浅拷贝
  ```

### 23、JS中的几种继承方法



### 24、深拷贝和浅拷贝以及解决方案

- 第一种方法:

  - ```js
      /**
       * 深拷贝出现的前提:引用类型的数据(对象和数组)
       * 深拷贝和浅拷贝
       * 
       * 1、对象浅拷贝解决方案
       *  (1)obj1对象stringify=>字符串=>parse成新的对象=>赋值给obj2
       *	(2)JSON转换方法的缺点:数据类型为function或者数据值为undifined情况下无法复制			(3)但是深拷贝了二级属性（引用类型）
      */	
      
      const obj1={
        a:1,
        b:undefined,
        arr:[1,2,4],
        fun: ()=>{},
      }
      const obj2=JSON.parse(JSON.stringify(obj1))
      obj2.a=2
      console.log(obj1,obj2); //{a: 1, b: undefined, arr: Array(3), fun: ƒ} 
                              //{a: 2, arr: Array(3)}
    ```


- 第二种方法:

  - ```js
    //Object.assign方法
    //缺点，只能拷贝一级属性，二级以上属性(引用类型)就无法深拷贝，二级以上还是浅拷贝
        const obj2=Object.assign({},obj1)
        obj2.a=2
        obj2.arr[0]=3
        console.log(obj1,obj2); 
    ```

- 第三种方法:

  - ```js
    //扩展运算符方法
    //缺点，和Object.assign方法的缺点一样，无法深拷贝二级的引用类型
        const obj2={...obj1}
        obj2.a=2
        obj2.arr[0]=3
        console.log(obj1,obj2); 
    ```

- 第四种方法

  - ```js
     //开发中最常用的，递归方法，比较完美
    function CloneDeep(data){
          const newData=Array.isArray(data)?[]:{}
          for(let key in data ){
            if(data[key]&&typeof(data[key])==="object"){
              newData[key]=CloneDeep(data[key])
            }else{
              newData[key]=data[key]
            }
          }
          return newData
        }
    ```

- 数组的话

  - (1)JSON方法也和拷贝对象一样,不能深拷贝undifined和方法
  - (2)Object.assign方法和展开运算符也是一样的，只能一级引用，不能二级引用
  - (3)数组多一种，slice和concat也是只能一级引用，不能二级
  - (4)递归还是比较完美的解决方案

### 25、toString用法

- 1、把数据转成字符串
  - 不同类型的数据调用的toString方法都是该数据类型原型链上的toString方法
  - 把数值转化成对应进制的数字字符串
  - null、undifined没有原型链，所以没有toString方法
- 2、用来判断数据类型
- 3、隐式转换
  - 当作为判断条件出现，或者作为运算符的某一项时，toString会隐式转化



