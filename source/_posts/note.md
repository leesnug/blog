---
title: 我的学习笔记
date: 2023-07-04 10:04:03
tags: html css javascript
---

# 一、html
备注： Windows 的文件系统使用反斜杠而不是正斜杠，例如：C:\Windows。这在 HTML 中并不重要——即使你在 Windows 系统上进行开发，你也应该在代码中使用正斜杠。

# 二、css
## 1.难点
### position和margin
- (1)子元素（无position时）margin尺寸为到父元素border or padding内侧的距离，子元素position尺寸为到父元素（已设为relative或absolute）border内侧距离。margin在position内部；margin值为百分数，百分数是相对于父元素内容盒子宽度而言的。

- (2)如果父级元素是绝对定位（absolute）或者没有设置，里面的绝对定位（absolute）自动以body定位。这句话是错的。

    正确的是：只要父级元素设了position并且不是static（默认既是static），那么设定了absolute的子元素即以此为包含块（最近的）。
    绝对定位（Absolute positioning）元素定位的参照物是其包含块，既相对于其包含块进行定位，不一定是其父元素。而且是相对于包含块的**border内侧**。
- (3)position: fixed，在连续媒体的情况下(continuous media)包含块是 viewport；在分页媒体(paged media)下的情况下包含块是分页区域(page area)。
 - (4)尺寸中的百分数。
   包含块内 所包含元素的 尺寸（width \ height \ padding \ margin）、位置绝对定位元素的偏移值（position: absolute \ fixed时的top \ bottom \ right \ left），若以百分比赋值，其计算值得基准为包含块的**content-box**边缘区域：
   
 > height / top / bottom 中的百分值的基准：包含块的 height 的值。(若包含块的height值会根据它的内容变化，且position: relative / static ，那么这些值的计算值为 auto。(暂时看不懂))
width / left / right / padding / margin 中百分值的基准：包含块的 width 属性的值。
### 多重样式优先级：
 
  | 类别                           | 权重值                  |
  | ------------------------------ | ----------------------- |
  | !important                     | Infinity(无限,最高级别) |
  | 行间样式                       | 1000                    |
  | id选择器                       | 100                     |
  | 类选择器/属性选择器/伪类选择器 | 10                      |
  | 标签选择器/伪元素选择器        | 1                       |
  | 通配符选择器                   | 0                       |
  | 通过继承获得的样式             | 没有权重                |
### 伪类、伪元素
### 元素定位
### 盒子

内部盒子margin的值是相对于上一个不为零的padding或border;未设置border和padding的盒子会跟随子元素优先保证padding和border的top值为零，外部盒子margin的值小于内部盒子，以内部盒子为准。

```
/* 应用于所有边 */
margin: 1em;
margin: -3px;

/* 上边下边 | 左边右边 */
margin: 5% auto;

/* 上边 | 左边右边 | 下边 */
margin: 1em auto 2em;

/* 上边 | 右边 | 下边 | 左边 */
margin: 2px 1em 0 auto;

/* 全局值 */
margin: inherit;
margin: initial;
margin: unset;
```

## 2.函数
transform:matrix()
![](https://oss.enjoytoday.cn/wp-content/uploads/2022/11/image-146.png)

## 3.属性继承
！Important>行内样式>ID选择器>类选择器>标签>通配符>继承>浏览器默认属性
权重我个人觉得只是前端学科自己定义的，由4位数组成，但不会有进位，可以说是有严格的等级制度，类似于古代封建制度，优先级在前的选择器，权重永远比其后的选择器高（就算其无限增加也一样）。
一，可以被继承的css属性
1.字体系列属性:font、font-family、font-weight、font-size、fontstyle;
2.文本系列属性:
2.1）内联元素：color、line-height、word-spacing（设置单词之间的间距）、letter-spacing（设置文本字符间距）、 text-transform(用于设置文本的大小写：uppercase所有字符强制转为大写，lowercase转小写，capitalize首字符强制转为大写);
2.2）块级元素：text-indent、text-align;
3.元素可见性：visibility
4.表格布局属性：caption-side（标题位置）、border-collapse（设置边框分离还是合并）、border-spacing（边框分离状态下设置边框间距）、empty-cells（定义如何渲染无可视内容的单元格边框和背景）、table-layout（定义用于布局单元格行和列的算法）;
5.列表布局属性：list-style
二，不可以被继承的css属性
1.display：规定元素应该生成的框的类型；
2.文本属性：vertical-align、text-decoration(用于设置文本的修饰线外观包括上/下划线，管穿线，删除线，闪烁 );
3.盒子模型的属性：width、height、margin、border、padding;
4.背景属性：background、background-color、background-image;
5.定位属性：float、clear、position、top、right、bottom、left、min-width、min-height、maxwidth、max-height、overflow、clip;

## 4.选择器
[CSS 属性选择器 ~=, |=, ^=, $=, *= 的区别](https://www.runoob.com/note/34568)
## 5.屏幕尺寸和浏览器适配

我们收到的设计稿只有一份，是物体分辨率，为了更清晰的像素。需要前端开发工程师手动除以设备像素比进行css布局。为了一份设计稿满足多设备，再布局时需要注意使用：

- 百分比
- 弹性盒布局
- rem布局
## 6.flex 和grid
grid二维布局，flex一维布局。
注意，设为Flex布局以后，子元素的float、clear和vertical-align属性将失效。

# 三、JavaScript
## 1.作用域
let在块级作用域上有效，不能变量提升。
var在函数内部时作用域在函数内部，其余均为全局变量，可变量提升。

## 2.递归
 注意内存使用，运行速度。


## 3.闭包
（1）目的：本质上是把函数内部的局部函数提升为全局函数，这样得到的全局函数便拥有无法在外部更改的"私有全局变量"。<BR>
（2）方法：可通过return返回局部函数或赋值给全局变量（常赋值给window属性）。
## 4.关于promise对象、异步函数async和await运算符
(注：下列代码中VM开头的为浏览器控制台输出结果)<BR>
1.await只能在async里面有效，后面可跟promise对象（"await promise对象"的值为promise对象处理成功resolve返回值），也可以不跟promise对象。注意await后面跟非promise对象时，await后面代码立即执行，await下一行代码最后执行，如下：
```
async function a(){  
  await console.log("1");  
  console.log("2");
}
a();
console.log("3");
console.log(a());//a()执行结果为promise对象，其属性有pending,fulfilled,rejected 。

VM10:2 1
VM10:6 3
VM10:2 1
VM10:7 Promise {<pending>}
2VM10:3 2
```
2.async函数执行的结果是promise对象，return的值传递给该promise对象的then方法的参数。注意return后面跟promise对象、非promise对象以及await的区别。<br>
（1）return后跟字符串，返回字符串：
```
async function helloAsync(){
    return "字符串";//等效于：return await "字符串";
  }

console.log(helloAsync());
 
helloAsync().then(res=>{
   console.log(res); 
})

VM14:5 Promise {<fulfilled>: '字符串'}
VM14:8 字符串
```
（2）return后面跟promise对象，返回resolve值：
``` 
function testAwait(){
   return new Promise((resolve) => {
       setTimeout(function(){
          console.log("testAwait");
          resolve("成功");
       }, 4000);
   });
}
async function helloAsync(){
   return await testAwait();
 }
helloAsync().then(res=>{console.log(res)});
Promise {<pending>}

VM326:4 testAwait
VM326:12 成功
```
（3）return后面跟await：代码1和代码3输出结果相同，代码2输出await后面的整个函数定义。
```
//代码1
async function a(event, context)  {
    return await (function test(){
          return new Promise((resolve, reject) => {
          // 在 3 秒后返回结果给调用方（小程序 / 其他云函数）
             setTimeout(() => {
                resolve(2+3)
                }, 3000)
          })  
    })();
}
//代码2
async function a(event, context)  {
    return await function test(){
          return new Promise((resolve, reject) => {
          // 在 3 秒后返回结果给调用方（小程序 / 其他云函数）
             setTimeout(() => {
                resolve(2+3)
                }, 3000)
          })  
    };
}
//代码3
async function a(event, context)  {
    return new Promise((resolve, reject) => {
          // 在 3 秒后返回结果给调用方（小程序 / 其他云函数）
            setTimeout(() => {
                resolve(2+3)
                }, 3000)
          })  
}
```
(4)try...catch捕捉异常：
## 5.函数

1.以函数声明的方法定义的函数，函数名是必须的，而函数表达式的函数名是可选的。

2.以函数声明的方法定义的函数可以在函数声明前调用，而函数表达式的函数只能在声明之后调用。

3.以函数声明的方法定义的函数并不是真正的声明，它们仅仅可以出现在全局中或者嵌套在其他的函数中，但是它们不能出现在循环、条件或者try/catch/finally中，而函数表达式可以在任何地方声明。换句话说，函数声明不是一个完整的语句，所以不能出现在if-else，for循环，try/catch/finally语句以及with语句中。

4.表达式中函数名只能在函数内部调用。

### this指向（难点）
面向对象语言中 this 表示当前对象的一个引用。

但在 JavaScript 中 this 不是固定不变的，它会随着执行环境的改变而改变。

- 在方法中，this 表示该方法所属的对象。
- 如果单独使用，this 表示全局对象。
- 在函数中，在严格模式下，this 是未定义的(undefined)。
- 在函数中，this 表示全局对象。
- 在事件中，this 表示接收事件的元素。
- 类似 call(), bind()()和 apply() 方法可以将 this 引用到任何对象。
(箭头函数有区别,注意点：没有 this、super、arguments 和 new.target 绑定。
https://www.runoob.com/w3cnote/es6-function.html)
(1)①普通函数this指向执行时绑定对象。注意：非严格模式下，回调函数执行时在全局作用域，this指向window。严格模式下this为undefined。

②箭头函数this指向定义时外层对象（不是定义时所在对象，举例:对象的方法中this指向window）。箭头函数不能使用new创建对象，即不能做构造函数。


### addEventListener
所以为了兼容所有的浏览器，我们可以定义一个函数：当有 addEventListener 时调用，没有的时候调用 attachEvent。
```
/*
 * 参数：
 *     obj：要绑定事件的对象
 *     eventStr：事件(注意：这里不要on)
 *      callback：回调函数
 */
 window.onload = function () {//若script标签在HTML元素之前，obj为null。
    var obj = document.getElementById("myBt");
    obj.addEventListenerNew("click", myFunction);
};
function addEventListenerNew(obj , eventStr , callback){
    if(obj.addEventListener){
        //大部分浏览器
        obj.addEventListener(eventStr , function(){
            //在匿名函数中调用回调函数
            callback.call(obj);
        } , false);
    }else{
        //IE8及以下
        obj.attachEvent("on"+eventStr , function(){
            //在匿名函数中调用回调函数
            callback.call(obj);
        });
    }
} 
```
实例：
```
<!DOCTYPE html>
<html>
<head>
    <meta charset="utf-8">
    <title>菜鸟教程(runoob.com)</title>
    <script>
        var p1 = 5;
        var p2 = 7;
        var arr = [2, 3, myFunction];//arr[2](p1, p2)执行时this指向arr;
        window.onload = function () {//dom加载了才能使用获取元素和使用addEventListener;
            var obj = document.getElementById("myBtn");
            console.log(obj);
            obj.addEventListener("click", function () {
                myFunction(p1, p2);//函数执行时this指向定义时所在对象；
            });
        }

        function myFunction(a, b) {
            var result = a * b;
            this.name = result;
            console.log(this);
            document.getElementById("demo").innerHTML = result;
        }
    </script>
</head>

<body>
    <p>实例演示了在使用 addEventListener() 方法时如何传递参数。</p>
    <p>点击按钮执行计算。</p>
    <button id="myBtn">点我</button>
    <p id="demo"></p>
</body>

</html>
```

## 6.es6

### （1）难点
对象和类中函数不需要写function关键字。

class,Map,Set前面需要new,Symbol前面不要用new。

4 种不应该使用箭头函数的情况[https://mp.weixin.qq.com/s?__biz=MjM5MDA2MTI1MA==&mid=2649130050&idx=2&sn=f568bd23973607f5c00d357170accf87&chksm=be58a3ef892f2af9c8f72dae3ea0b433da0d440f9dede897be48002a04b2d8a01e555b1bd056&scene=27]()

归纳为一句话：箭头函数中this指向和普通函数不同。

### （2）ES6 引入了模块化
ES6 引入了模块化，其设计思想是在编译时就能确定模块的依赖关系，以及输入和输出的变量。

ES6 的模块化分为导出（export） @与导入（import）两个模块。

特点
ES6 的模块自动开启严格模式，不管你有没有在模块头部加上 use strict;。

模块中可以导入和导出各种类型的变量，如函数，对象，字符串，数字，布尔值，类等。

每个模块都有自己的上下文，每一个模块内声明的变量都是局部变量，不会污染全局作用域。

每一个模块只加载一次（是单例的）， 若再去加载同目录下同文件，直接从内存中读取。

> **Node 模块与 ES6 模块的对比**
分别了解了 Node 模块跟 ES6 模块以后，我们对它们进行更加深入的分析与对比。通过上文知道它们的语法是不一样的，使用的 API 不同。
Node 模块导出是一个对象，而 ES6 模块是多个 API 导出。
Node 模块是动态导入，可以写在任何地方。ES6 模块是静态导入，只能写在顶层（import 会被变量提升）。
ES6 模块使用 import 被导入的变量是只读的，不能被赋值，其次被导入的变量是引用传递，与原变量是绑定的，如果被改变了，其它导入该模块的地方也会受到影响。而 Node 模块导入的是值的浅拷贝。

作者：LvLin
链接：https://juejin.cn/post/6975512335603466276
来源：稀土掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
## Node
### npm
#### package.json
main - main 字段指定了程序的主入口文件，require('moduleName') 就会加载这个文件。这个字段的默认值是模块根目录下面的 index.js。
# 四、Typescript
## 变量声明
### TypeScript 遵循强类型。
泛型方法:是在调用方法的时候指明泛型的具体类型 。
var [变量名] : [类型];//默认初始值为 undefined，但不能把undefined赋值给变量名。
var [变量名];//默认初始值为 undefined，能把undefined赋值给变量名。
TypeScript 并不总是可以正确推断变量类型。

类型断言是编译时的一种方法，非运行时的转换。

```
var str = '1' 
var str2:number = <number> <any> str   //str、str2 是 string 类型
console.log(str2)
```
### 元组

元组类型用来表示已知元素数量和类型的数组，各元素的类型不必相同，**对应位置的类型需要相同**。

example:
let x: [string, number];let x=["runboon",23];

## 函数
在 TypeScript 函数里，如果我们定义了参数，则我们必须传入这些参数，除非将这些参数设置为可选，可选参数使用问号标识 ？。
Lambda 函数也称之为箭头函数。

# 五、微信小程序学习
## 1.总述 
### JavaScript调试
小程序服务端包括数据库、储存和云函数等。小程序开发者工具中包含小程序miniprogram和云函数cloudfunctions两个文件夹。云函数必须上传部署才能调试运行。开启云函数本地调节，可直接在本地运行，无需上传部署。服务端JavaScript（即云函数）运行情况可在云函数本地调节工具控制台中查看；客户端JavaScript运行情况可在小程序开发者工具控制台中查看。
## 2.业务逻辑
整个过程最难的是参数的传递和前后端的交互逻辑。form表单页中的index.js最复杂。




# 六、git
### 提交版本
现在我们已经添加了这些文件，我们希望它们能够真正被保存在Git仓库。

为此，我们将它们提交到仓库。
```
git commit -m "Adding files"
```
如果您不使用-m，会出现编辑器来让你写自己的注释信息。

当我们修改了很多文件，而不想每一个都add，想commit自动来提交本地修改，我们可以使用-a标识。
```
git commit -a -m "Changed some files"
```
git commit 命令的-a选项可将所有被修改或者已删除的且已经被git管理的文档提交到仓库中。

<p style="color:red">千万注意，-a不会造成新文件被提交，只能修改。"git add ."之后才可以提交</p>

### 通过https连接不上github

fatal: unable to access 'https://github.com/leesnug/leesnug.github.io.git/': SSL certificate problem: unable to get local issuer certificate

这是由于当你通过HTTPS访问Git远程仓库的时候，如果服务器上的SSL证书未经过第三方机构认证，git就会报错。原因是因为未知的没有签署过的证书意味着可能存在很大的风险。解决办法就是通过下面的命令将git中的sslverify关掉：
```
git config --global http.sslverify false
```
或者使用ssh连接。


beforeCreate
created
beforeMount
mounted
beforeUpdate
updated
beforeUnmount
unmounted
errorCaptured

# 七、Vue3
## 1.Proxy和Reflect
Vue.createApp().mount()实际上是生成一个Proxy对象。

### js和html数据双向绑定
```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <p>
        <span>年龄：</span>
        <input type="text" id="age" value="13">
    </p>
</body>
<script>
    const spanAge = document.getElementById("age");
    let user = {
        age:spanAge.value
    }
    let newuser = new Proxy(user,{
        set(target, key, value){
            if (key === "age" && isNaN(value)) {
                throw Error("age字段必须为Number类型");
            }
            spanAge.value = value;
            return Reflect.set(target, key, value);
        }
    })
    spanAge.onblur = function(){
        newuser.age = document.getElementById("age").value;
            console.log(user);
        }
        console.log(user)
</script>
</html>
```
## 2.v-model
在文本区域 textarea 插值是不起作用，需要使用 v-model 来代替。
复选框绑定的数据可以为逻辑值，也可以为一个数组。
对于单选按钮，复选框及选择框的选项，v-model 绑定的值通常是静态字符串 (对于复选框也可以是布尔值)。

