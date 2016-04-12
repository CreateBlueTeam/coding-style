#JS规范
提高代码的可读性，提高团队协作效率

#版本
1.0.0

#编码风格
避开一些低级错误，减少BUG隐患，提升可读性。

**缩进**

缩进为四个半角 `' '` ，或者 `Tab` 缩进，根据习惯，我们一般采用 `Tab` 键

**空格**
- 左括号与类名之间一个空格
- 冒号与属性之间一个空格
- 操作符前后一个空格
````js

//左括号与类名之间
function getName() {
    //coding here
}

//冒号与属性之间
var obj = { //操作符前后
    name: "johan",
    age: "22"
}

//操作符前后
var a = 30,
    count = 15 > (a-15) ? 15 : 0;
````

**空行**

在一段语义与另一段代码不相关、长段注释之前等，应用空行隔开。例如

- 在方法与方法之间
- 方法中的局部变量与第一条语句之间
- 方法内的逻辑片段之间
````js

//方法之间
function a() {
    //coding here
}

function b(){
    //coding here
}

//局部变量与第一条语句之间
function addSome(a,b) {
    var c = 5;

    return a + b + c;
}

//逻辑片段之间
function (a) {
    a += 5;

    if(a){
        //coding here
    }
}
````
**命名约定**
变量与函数使用驼峰大小写命名，命名承载一定的含义

**注释**
适当的添加注释，辅助表明代码执行工作原理

#变量

变量存在命名冲突、深耦合、变量泛滥等问题

**避免隐性全局变量**

任何变量，如果未经声明，就为全局对象所有。
````js

//缺失var声明
function obj() {
    name = 'johan';
    return name;
}

console.log(name); // 'johan'

//var声明的链式赋值
function variable() {
    var a = b = 1;
}

/*
 *  执行过程
 *  var a = (b = 1)
 *  生成全局变量 b 并赋值为 1
 *  再给局部变量a赋值 a = b
 */
console.log(b); // 1
````

隐性全局变量并非var声明的变量，而是全局对象的属性，可以通过 `delete` 操作符删除；但是var声明的变量不行，并在 `use 'strict'` EC5以上抛出错误；

**变量提升**

在 `JavaScript` 中，相同作用域中的变量都提前放置在执行上下文 `Execution Context` 中，在运行调用的时候赋值。所以我们把变量声明前置，可读性和维护。

**多变量声明**
````js
//变量声明
var a,b,c;

//变量赋值
var a = 15,
    b = 18,
    c = 20;
````
**全局变量的使用**

尽量避免全局变量，如需使用时采用单全局变量的方式开启项目。如各种类库的使用

````js
(function (win,doc,undefined) {
    var CBlue = {
        version : "1.0.0"
    }

    win.CBlue = CBlue;
})(window,document);
````

#UI松耦合

当修改一个组件的逻辑，而对另一个组件没有影响。

- 将JavaScript从css中抽离，如避免css表达式
- 将css从JavaScript中抽离，如避免使用JavaScript直接修改css,最佳方案操作css的ClassName
- 将JavaScript从HTML中抽离，尽量避免函数直接嵌套到HTML执行。
- 将HTML从JavaScript中抽离,如避免在JavaScript中拼接HTML结构。需要时使用模板引擎，如 `Vue.js` `React.js`

#错误处理

**何时抛错**

识别代码在特定的情况下可能导致的错误，思考过程中会预期出现的错误

**怎样抛错**

`try {}` 中的代码为可能引发错误； `catch() {}` 处理错误代码

````js
try {
    some();
} catch(e) {
    catchError(e);
}
````
`throw` 直接抛出错误，代码停止执行

````js
throw new Error("a is not a found");
````

#创建对象

**对象字面量**

- 对象包装在大括号中
- 逗号分隔属性和方法
- 用冒号分隔属性名和属性值

````js
var person = {
    name: 'johan',
    job: 'Front-End Dev'
}
````

模块基础写法
````js
var obj = (function (){
    var name = 'johan',
        job = 'Front-End Dev';

    return {
        getName: function () {
            return name;
        }
    }
})();
````

**构造函数**

- 创建一个对象并且this变量引用该对象，并继承该对象的原型
- 属性和方法被加到this引用的对象中
- 隐式返回新对象
- 构造函数首字母大写

````js
function Obj() {

    //公有属性
    this.name = 'johan';
    this.job = 'Front-End Dev';

    //共有方法
    this.getName = function () {
        return this.name;
    }
}

//调用方式
var obj = new Obj();
obj.getName(); //'johan'
````

**原型模式**

每个构造函数都有一个原型 `prototype` , 原型对象包含一个指向构造函数的指针 `constructor` ,这个指针指向一个可以由特定类型的所有实例共享的属性和方法;
````js
function Obj() {
    //coding here
}

Obj.prototype = {
    name: 'johan',
    age: '22',
    getName: function () {
        return this.name;
    }
}

var obj = new Obj();
alert( obj.constructor == Obj ); //false

````

重写整个原型切断了与原型之间的联系，实例的指针仅仅指向了原型，而不是构造函数，需要通过手动改写 `constructor` 

````js
function Obj() {
    //coding here
}

Obj.prototype = {
    constructor : Obj,
    name: 'johan',
    age: '22',
    getName: function () {
        return this.name;
    }
}

var obj = new Obj();
alert( obj.constructor == Obj ); //true
````

**模块模式**

- 模块化
- 可复用
- 松耦合
- 区分公有方法和私有方法
````js
var test =  (function (obj) {
    var testNode = document.getElementById("test");

    obj.setHtml = function (txt){
        testNode.innerHTML = txt;
    }

})(test || {});

test.setHtml("Hello World");

````

保护私有对象和属性

````js
var test = (function () {
    var testNode = document.getElementById("test"),
        
        setHtml = function (txt){
            testNode.innerHTML = txt;
        }

    //设置公共调用方法
    return {
        setHtml: setHtml
    }
})();
````
还有迭代模式、工厂模式等
待续...
