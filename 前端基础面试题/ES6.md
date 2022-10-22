# ES6新特性

## 常量变量声明

### let变量声明以及 声明特性

```js
//声明变量
let a;
let b,c,d;
let e = 100;
let f=521,g='love',h=[]
```

##### 特性:

1. let变量声明不能重复

   ```js
   let a='c'	
   let a='b'❌
   ```

   

2. 块级作用域:全局,函数,eval

   ```js
   //例如:if else while for
   {let a='a'}
   console.log(a)❌
   ```

3. 不存在变量提升

   ```js
   console.log(song)    //undifined
   var song='song'
   
   console.log(song)
   let song='song' ❌  ///不存在变量提升
   ```

4.  不影响作用域链

   ```js
   {
       let school='尚硅谷';
       function(){
           console.log(school);  //虽然是块级作用域,但是不影响作用域链的效果,还是能输出尚硅谷
       }
   }
   ```

### const常量声明以及 声明特性

##### 特性:

- 1:一定要赋初始值

- 2:一般常量使用大写(潜规则)

  - const A=100

- 3:常量的值不能修改

- 4:块级作用域

- 5:对于数组和对象的元素修改,不算做对常量的修改,不会报错

  - ```JS
    const TEAM=['1','2','3','4']
    TEAM.push('5')  //const常量地址没有改变,所以不会报错
    ```

### 变量的解构赋值

##### es6允许按照一定模式从数组和对象中提取值,对变量进行赋值,这被称为解构赋值

```js
1.数组的解构
const F4=['a','b','c','d']
let [xiao,liu,zhao,song]=F4
console.log(xiao)       //a
console.log(liu)       //b
console.log(zhao)       //c
```

```
2.对象的解构
const zhao={
	name:'赵本山',
	age:'不详',
	xiaopin:function(){
		console.log("我可以演小品")
	}
};

let {name,age,xiaopin}=zhao;
console.log(name);
console.log(xiaopin);
console.log(age);

xiaopin(); //解构之后的方法可以正常调用
```

## 模板字符串

```js
//1,声明
let str=`我也是一个字符串`
console.log(str,typeof str);   //我也是一个字符串 string
//2,内容中可以直接出现换行符
let str1=`<ul>
            <li>沈腾</li>
            <li>沈腾</li>
            <li>沈腾</li>
            <li>沈腾</li>
           </ul>`
//3,变量拼接
let lovest='张三';
let out='${lovest}是我心目中最搞笑的人'
console.log(out) //张三是我心目中最搞笑的人
```

## 对象的简化写法

```js
//ES6 允许在大括号里面,直接写入变量和函数,作为对象的属性和方法
//这样的书写更加简洁

	let name='尚硅谷';
    let change=function(){
        console.log('我门可以改变你!')
    }
    
    const school={
        name,
        change,
        improve(){
            console.log("我们可以提高你的技能")
        }
    }
```

```js
let fn=(a,b)=>{
    return a+b;
}
//调用函数
let result=fn(1,2)
console.log(result) //3

//特性
//1,this是静态的,this始终指向声明时所在作用域下的this的值
function getName(){
    console.log(this.name)
}
let getName2=()=>{
    console.log(this.name)
}

//设置window 对象的name属性
window.name='尚硅谷';
const school={
    name:'ATGUIGU'
}

//直接调用
getName(); //尚硅谷
getName2(); //尚硅谷

//call方法调用
getName.call(school); //尚硅谷
getName2.call(school); //ATGUIGU
```

```js
//2,不能作为构造函数实例化对象
let Person=(name,age)=>{
    this.name=name;
    this.age=age;
}
let me =new Person('xiao',30) ❌ //箭头函数不能作为构造函数去实例化对象
```

```js
//3,不能使用arguments变量
let fn=()=>{
    console.log(arguments); ❌ //arguments用来保存实参,箭头函数中不可以
}
fn(1,2,3);  //arguments is not defined
```



```js
//4,箭头函数的简写
	//一,省略小括号,当形参有且只有一个的时候可以省略
	let add = n =>{
        return n+n;
    }
    console.log(add(9)); //18
	
	//二,省略花括号,当代码体只有一条语句的时候可以省略
	let pow = n => n * n
```

```js
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    #ad{
      width: 300px;
      height: 300px;
      background-color: aqua;
    }
  </style>
  <title>Document</title>
</head>
<body>
  <div id="ad"></div>
  <script>
    // //需求-1 点击div 2s后颜色变成粉色
    // //获取元素
    // let ad=document.getElementById('ad');
    // //绑定事件
    // ad.addEventListener('click',function(){
    //   //将this指向保存
    //   // let that=this;
    //   setTimeout(()=>{
    //     this.style.background='pink'
    //   },2000)
    // })

    const arr=[1,6,9,10,100,25]
    // const result=arr.filter(function(item){
    //   if(item%2===0){
    //     return true
    //   }else{
    //     return false
    //   }
    // });
    const result=arr.filter(item=>item%2===0)
    console.log(result);
  </script>
</body>
</html>
```

总结:

- 箭头函数适合与this无关的回调,定时器,数组的方法的回调
- 箭头函数不适合与this有关的回调,事件监听,对象的方法

##  函数参数的默认值设置

```js
//ES6允许给函数参数赋值初始值
    //1、形参初始值，具有默认值的参数，一般位置要靠后（潜规则）
   function add(a,b,c=10){
    return a+b+c;
   }
   let result = add(1,2);
   console.log(result);

   //2、与解构赋值结合使用
  //  function connect(options){
  //     let host=options.host;
  //     let username=options.username
  //  }
  function connect({host="127.0.0.1",username,password,port}){
    console.log(host); //未传值获得默认值
    console.log(password);
    console.log(username);
    console.log(port);

  }
   connect({
    // host:'localhost',
    username:'root',
    password:'root',
    port:3306
   })
```

## rest参数

```js
//ES6引用rest参数,用于获取函数的实参,用来代替arguments
//ES5获取实参的方式
function date(){
  console.log(arguments); //Arguments(3) ['白芷', '阿娇', '思慧', callee: ƒ, Symbol(Symbol.iterator): ƒ]
}
date('白芷','阿娇','思慧')
//ES6获取实参的方式
function date1(...args){
  console.log(args); //(3) ['白芷', '阿娇', '思慧'] 返回的是数组，所以很多方法可以使用，例如：filter、some、every、map
}
date1('白芷','阿娇','思慧')
```

## 扩展运算符

```js
//扩展运算符
  //1、数组的合并
  const kuaizi=['王太利','肖央']
  const fenghuang=['曾毅','玲花']
  const together=[...kuaizi,...fenghuang]
  console.log(together); //['王太利', '肖央', '曾毅', '玲花']


   //2、数组的克隆
   const sanzhihua=['E','G','M'];
   const sanyecao=[...sanzhihua];
   console.log(sanyecao);


   //3、将伪数组转换为真正的数组
   const divs=document.querySelectorAll('div');
   console.log(divs);
   const divArr=[...divs]
   console.log(divArr);
```

## Symbol

```js
//1、Symbol不是构造函数，不能使用new关键字，否则异常
//2、Symbol()括号中的内容表示Symbol描述，只是为了方便开发中给辨识，并不是Symbol的值
//3、每一个Symbol类型数据都独一无二，不能划等号
//4、Symbol不能和其他值参与运算
//5、Symbol类型的属性无法被Object.keys遍历到

//1、作用定义常量，使得不重复
//2、在对象中作为属性 到保护隐私的作用
  var obj={
    name:'zhangsan',
    age:18,
    gender:'男',
    [Symbol('password')]:'123456'
  }  

  console.log(obj);
  var str=JSON.stringify(obj)
  console.log(str);  //{"name":"zhangsan","age":18,"gender":"男"}
```

## 迭代器

```js
  const xiyou=['唐僧','孙悟空','猪八戒','沙僧']
  for(let v of xiyou){
    console.log(v);
  }
  console.log(xiyou);
/*   唐僧
 孙悟空
 猪八戒
 沙僧 */
```

## 生成器

```js
 //异步编程：文件操作 网路操作(ajax,request) 数据库操作
//1s后控制台输出111 2s后控制台输出222 3s后输出333

function one(){
    setTimeout(()=>{
      console.log('111');
      iterator.next()
    },1000)
  }

  function two(){
    setTimeout(()=>{
      console.log('222');
      iterator.next()
    },2000)
  }

  function three(){
    setTimeout(()=>{
      console.log('333');
      iterator.next()
    },3000)
  }

  function * ge(){
    yield one();
    yield two();
    yield three();
  }

  //调用生成器函数
  let iterator=ge();
  iterator.next();
```



```js
 //模拟获取 用户数据   订单数据  商品数据
  function getUsers(){
    setTimeout(() => {
      let data='用户数据'
      iterator.next(data)
    }, 1000);
  }

  function getOrders(){
    setTimeout(() => {
      let data='订单数据'
      iterator.next(data)
    }, 1000);
  }

  function getGoods(){
    setTimeout(() => {
      let data='商品数据'
      iterator.next(data)
    }, 1000);
  }


  function * gen(){
    let users=yield getUsers();
    console.log(users);
    let orders=yield getOrders();
    console.log(orders);
    let goods=yield getGoods();
    console.log(goods);
  }

  //调用生成器函数
  let iterator=gen();
  iterator.next();
```

## Promise

```js
//Promise封装读取文件
const fs=require('fs')


// fs.readFile('./01.txt',(err,data)=>{
//   //如果失败，则抛出错误
//   if(err) throw err;
//   console.log(data.toString());
// })

const p = new Promise((resolve,reject)=>{
  fs.readFile('./01.txt',(err,data)=>{
    //读取失败
    if(err) reject(err);
    //读取成功
    resolve(data)
  })
})


p.then(value=>{console.log(value.toString());},err=>{console.log('读取失败');})
```

```js
//Promise封装ajax
    const p = new Promise((resolve,reject)=>{
 
    //接口地址 https://api.apiopen.top/getJoke
    //1、创建对象
    const xhr=new XMLHttpRequest();

    //2、初始化
    xhr.open("GET",'http://39.101.74.59:3000/artist/songs?id=6452')

    //3、发送
    xhr.send();

    //4、绑定事件，处理响应结果
    xhr.onreadystatechange=function(){
      //判断
      if(xhr.readyState===4){
        //判断响应状态码200-299
        if(xhr.status>=200&&xhr.status<300){
          //表示成功
          resolve(xhr.response)
        }else{
          //如果失败
          reject(xhr.status);
        }
      }
    }   
  })
    p.then(value=>{console.log(value);},err=>{console.log(err);})
```

## Set

##### ES6提供了新的数据结构Set(集合)，它类似于数组，但成员的值都是唯一的，集合实现了iterator接口，所以可以使用扩展运算符和for of 进行遍历，集合的属性和方法：

1. size  返回集合的元素个数
2. add  增加一个新元素，返回当前集合
3. delete 删除元素，返回boolean值
4. has 检测集合中缩放包含某个元素，返回boolean值
5. clear清空集合

```js
    //声明一个set
    let s = new Set();
    let s2=new Set(['1','2','3','4','2','1'])
    console.log(s2.delete('2'));
    console.log(s2);
    console.log(s2.has('1'));
```

```js
	
```

