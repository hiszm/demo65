

- [一、js数据类型](#一js数据类型)
- [二、数组增删改查](#二数组增删改查)
  - [增](#增)
  - [**删**](#删)
  - [**改**](#改)
  - [**查**](#查)
- [三、DOM数据结构 和常用的api](#三dom数据结构-和常用的api)
  - [DOM的结构](#dom的结构)
  - [常用语法](#常用语法)
  - [Oject增删改查](#oject增删改查)
- [四、js进行深层次的复制](#四js进行深层次的复制)
  - [浅复制](#浅复制)
  - [深度复制](#深度复制)
- [五、IE与W3C区别和参数，以及IE的even的区别](#五ie与w3c区别和参数以及ie的even的区别)
  - [两者区别](#两者区别)
  - [事件](#事件)
  - [事件的三个参数](#事件的三个参数)
- [六、原生JS实现事件委托](#六原生js实现事件委托)
  - [概念](#概念)
  - [实现](#实现)



作业一： https://github.com/hiszm/demo65/blob/main/README.md

作业二：https://hiszm.github.io/demo65/





### 一、js数据类型



```html 
<!-- 
typeof  123　　 //Number
typeof  'abc'　　//String
typeof  true    //Boolean
typeof  undefined  //Undefined
typeof  null    //Object
typeof  { }      //Object
typeof  [ ]      //Object
typeof  console.log()    //Function
 -->
<script>
console.log(typeof(123)) 
function getType(data){
    let type = typeof data;
    if(type !== "object"){
      return type
    }
    return Object.prototype.toString.call(data).replace(/^\[object (\S+)\]$/,'$1')
}
```



### 二、数组增删改查

> 注意坑： 删除的插入增加的时候数组前中后

#### 增

**1、push()**

可接收任意数量的参数，把它们逐个添加至数组末尾，并返回修改后数组的长度。例如：

```
var arr = [];
var len = arr.push(1);
console.log(arr); // [1]
console.log(len); // 1
len = arr.push(2,3);
console.log(arr); // [1,2,3]
console.log(len); // 3
```

**2、unshift()**

该方法与push()类似，也可接收任意数量的参数，只不过是将参数逐个添加至数组前端而已，同样返回新数组长度。咱们接着上面的例子：

```
var len = arr.unshift(0);
console.log(arr); // [0, 1, 2, 3]
console.log(len); // 4
len = arr.unshift(-2,-1);
console.log(arr);  // [-2, -1, 0, 1, 2, 3]
console.log(len);  // 6
```

**3、concat()**

该方法与push()方法有点类似，同样是将元素添加至数组末尾，只不过这个数组已经不是原来的那个数组了，而是其副本，所以concat()操作数组后会返回一个新的数组。具体用法如下：

① 不传参数，返回当前数组副本

② 传递一或多个数组，则该方法会将这些数组中的每一项都添加到结果数组中

③ 传递非数组参数，这些参数就会被直接添加到结果数组的末尾

继续接着上面的栗子：

```
var arr1 = arr.concat(4,[5,6]);
console.log(arr);  // [-2, -1, 0, 1, 2, 3]
console.log(arr1);  // [-2, -1, 0, 1, 2, 3, 4, 5, 6]
```

例子中一目了然，原数组保持不变，新数组后面添加了4、5、6三个元素。

**4、splice()**

前面的三个方法都具有很大局限性，因为不是添加到数组前就是数组后，而splice()就不一样了，它非常灵活和强大。灵活是因为它可以添加元素到数组的任意位置，强大是因为它除了可以添加元素之外还具有删除和替换元素的功能（这个后面会陆续讲到）。

splice()可以向数组指定位置添加任意数量的元素，需要传入至少3个参数： 起始位置、0（要删除的元素个数）和要添加的元素。

依然接着上面的例子继续：

```
arr.splice(3,0,0.2,0.4,0.6,0.8);
console.log(arr); // [-2, -1, 0, 0.2, 0.4, 0.6, 0.8, 1, 2, 3]
```

可以看出，splice()与push()和unshift()一样是直接在原数组上修改的。

#### **删**

**1、pop()**

与push()方法配合使用可以构成后进先出的栈，该方法可从数组末尾删除最后一项并返回该项。

接着上例：

```
var item = arr.pop();
console.log(item);  // 3
console.log(arr);  // [-2, -1, 0, 0.2, 0.4, 0.6, 0.8, 1, 2]
```

**2、shift()**

与push()方法配合使用可以构成先进先出的队列，该方法可删除数组第一项并返回该项。

继续接着上例：

```
var item = arr.shift();
console.log(item); // -2
console.log(arr); // [-1, 0, 0.2, 0.4, 0.6, 0.8, 1, 2]
```

**3、slice()**

该方法同concat()一样是返回一个新数组，不会影响原数组，只不过slice()是用来裁剪数组的，返回裁剪下来的数组，具体用法如下：

slice()方法可以接受一或两个参数，即要返回项的起始和结束位置。在只有一个参数的情况下，slice()方法返回从该参数指定位置开始到当前数组末尾的所有项。如果有两个参数，该方法返回起始和结束位置之间的项——但不包括结束位置的项。

咱们还是继续接着上面例子吧~~

```
var item = arr.shift();
console.log(item); // -2
console.log(arr); // [-1, 0, 0.2, 0.4, 0.6, 0.8, 1, 2]
```

**4、splice()**

好，继续讲这个“万能”的方法。

上面讲到，该方法在添加数组元素的时候需要传入3个以上参数，而其中第2个参数就是用于指定要删除元素的个数的，那时我们传的是数字0。那么，如果单单只需删除元素，我们就只需给splice()传入两个参数，第1个参数用于指定要删除的第一项的位置，第2个参数用于指定要删除元素的个数。

继续上例~~

```
arr.splice(2,4);
console.log(arr); // [-1, 0, 1, 2]
```

从索引项为2的位置开始删除4个元素，所以结果为 [-1, 0, 1, 2]。

#### **改**

这个其实最灵活的方式就是直接使用splice()这个强大的方法了，其实通过以上对该方法的了解，我们大致就能知道使用该方法修改数组元素的基本原理。

原理很简单，就是向指定位置插入任意数量的元素，且同时删除任意数量的元素。

依然继续上例~~

```
arr.splice(2,1,0.5,1,1.5);
console.log(arr);  // [-1, 0, 0.5, 1, 1.5, 2]
```



#### **查**

**indexOf()和lastIndexOf()**

这两个方法都接收两个参数：要查找的项和（可选的）表示查找起点位置的索引。其中，indexOf()从数组的开头（位置0）开始向后查找，lastIndexOf()方法则从数组的末尾开始向前查找。

例如：

```
var index = arr.indexOf(0);
console.log(index);  // 1
index = arr.indexOf(3,0);
console.log(index);  // -1

```

当找不到该元素时，返回 -1 ，lastIndexOf()方法同理





### 三、DOM数据结构 和常用的api

**增删改查-注意父子也即是前后**
#### DOM的结构

- 树结构，像获取子节点，获取父节点，都是树结构的操作。

![img](https://gitee.com/hiszm/img2021/raw/master/06/20210605142003.webp)



![img](https://gitee.com/hiszm/img2021/raw/master/06/20210605142025.webp)

#### 常用语法
**//1.定义对象： var const let**



```var Person = {
　　name: '张三',
　　birth,//等同于birth: birth
　　hello() { console.log('我的名字是', this.name); }// 等同于hello: function ()...
};
```



/**/2.对象的合并assign：**

**2.1.添加属性\**\**\**\**\**\**\**\**\**\**\**\**\**\**\**\**\**\**\***
```
var target = { a: 1 };//合并成： {a:1, b:2, c:3}，注：同名属性，则后面的属性会覆盖前面的属性。
var source1 = { b: 2 };
var source2 = { c: 3 };

Object.assign(target, source1, source2);
```

**2.2.添加方法\**\**\**\**\**\**\**\**\**\**\**\**\**\**\**\**\**\**\**\**\**\**\***

```
Object.assign(SomeClass.prototype, {
　　someMethod(arg1, arg2) {
　　　　···
　　},
　　anotherMethod() {
　　　　···
　　}
});
// 等同于下面的写法
SomeClass.prototype.someMethod = function (arg1, arg2) {
···
};
SomeClass.prototype.anotherMethod = function () {
···
};
```

**2.3.克隆对象\**\**\**\**\**\**\**\**\**\**\**\**\**\**\**\**\**\**\**\**\**\****


```

var obj1 = {a: {b: 1}};//obj1.a.b = 2;
var obj2 = Object.assign({}, obj1);//克隆对象obj1,得到：obj2.a.b=2

//只能克隆原始对象自身的值，不能克隆它继承的值。
class Point {
　　constructor(x, y) {
　　　　Object.assign(this, {x, y});
　　}
}
//解决方案
function clone(origin) {
　　let originProto = Object.getPrototypeOf(origin);
　　return Object.assign(Object.create(originProto), origin);
}
```
**2.4.合并多个对象**
```
const merge = (target, ...sources) => Object.assign(target, ...sources);
const merge = (...sources) => Object.assign({}, ...sources);
```
**2.5.为属性指定默认值,即2.1的扩展**
```
const DEFAULTS = {
　　logLevel: 0,
　　outputFormat: 'html'
};

function processContent(options) {
　　options = Object.assign({}, DEFAULTS, options);
　　console.log(options);
　　// ...
}

```
**【实践操作：】**
```
**//1.获取key value组合成数组:js ES6**
var obj = {
　　"name" : "zh",
　　"age" : 22,
}
**1.1.对象自身属性遍历**
for(var key in obj){
　　console.log(key); //键名
　　console.log(obj[key]); //键值
　　//if(obj.hasOwnProperty(key))

　　if (obj.hasOwnProperty(key) === true) {
　　　　console.log(obj[key])
　　}

}

const  keys = Object.keys(obj);
const  values = Object.values(obj);

**1.2.解构赋值**
let { x, y, ...z } = { x: 1, y: 2, a: 3, b: 4 };
x // 1
y // 2
z // { a: 3, b: 4 }

**1.3.扩展运算符**
let z = { a: 3, b: 4 };
let n = { ...z };
n // { a: 3, b: 4 }


**//2.取值判断问题**

**2.1.读取对象内部的某个属性，往往需要判断一下该对象是否存在**
const firstName = message && message.body && message.body.user && message.body.user.firstName) || 'default';

if(firstName){

}
**2.2.现在有一个提案，引入了“Null 传导运算符”**

const firstName = message?.body?.user?.firstName || 'default';

if(firstName){

}

```

#### Oject增删改查



1、定义（增）属性
1.1、使用冒号可以为对象定义属性：

> var obj = {name:'erha',age:18};    //冒号左侧是属性名，右侧是属性值。属性与属性之间通过逗号运算符进行分隔

1.2、可以通过 点运算符 在结构体外定义属性：

> var obj = {name:'erha',age:18};
> obj.gender = 2;      //定义对象的属性
> console.log(obj);    //{name:'erha',age:18,gender:2}



1.3、通过 Object.defineProperty() 方法定义对象属性：

先创建一个对象直接量 obj，然后使用 Object.defineProperty() 函数将数据属性添加到用户定义的 obj 对象中。定义属性 newDataProperty，值为101，可写，可枚举，可修改特性。

> var obj = {};
> Object.defineProperty(obj,"newDataproperty",{
>     value：101,
>     writable:true,
>     enumexable:true,
>     configurable:true
> });
> obj.newDataProperty = 102;
> document.write(obj.newDataProperty);    //102
>
> 

1.2、通过 Object.defineProperties() 方法定义对象的多个属性：

使用 Object.defineProperties() 函数将数据属性和访问器属性添加到用户定义的对象 obj 上。使用对象文本创建具有 newDataProperty 和 newAccessorProperty 描述符对象的 descriptors 对象。

> var obj = {};
> Object.defineProperties (obj,{
>     newDataProperty:{
>         value:101,
>         writable: true,
>         enumerable: true,
>         configurable: true
>     },
>     newAccessorProperty:{
>         set: function (x){
>             this.newaccpropvalue = x;
>         },
>         get: function ){
>             return this.newaccpropvalue;
>         },
>         enumerable; true,
>         configurable; true
>     }
> });
> obj.newAccessorProperty = 10;
> document.write(obj.nexAccessorProperty);    //10



2、访问（读）属性
2.1、通过 点运算符 可以访问对象属性：

> var obj = {name:'erha',age:18};
> console.log(obj.name);        //erha
> console.log(obj.['name']);    //erha

> let name = 'age';
> console.log(obj.[name]);      //18    因为此时name是变量，它的值是 'age'

> console.log(obj.__proto__);    //{constructor:...,toString:...}
> 注意：obj.name 等价于 obj['name']，而 obj.name 不等价于 obj[name]。因为点运算符后的 name 是字符串，而不是变量。

2.2、通过 Object.keys() 方法可访问对象的 私有属性：

> var obj = {name:'erha',age:18};
> console.log(Object.keys(obj));       //{'name','age'}
> console.log(Object.values(obj));     //{'erha',18}
> console.log(Object.entries(obj));    //{[name,'erha'],[age,18]}

> console.dir(obj);    //查看所有属性：{name:'erha',age:18,__proto__:......}



2.3、可以通过 obj.hasOwnProperty() 判断一个属性是否为对象的私有属性：

> var obj = {name:'erha',age:18};
> console.log(obj.hasOwnProperty('toString'));    //false，说明toString属性并不是obj的私有属性
> console.log('toString' in obj);    //true，这种 in 运算符不能分清属性是对象的私有属性还是原型上的属性

2.4、可以通过 Object.getPrototypeOf() 返回指定对象的原型

> function Pasta(grain,width){
>     this.grain = grain;
>     this.width = width;
> }
> var spaghetti = new Pasta("wheat",0.2);    //实例化一个Pasta函数对象，此时spaghetti的__proto__指向Pasta函数的原型
> var proto = Object.getPrototypeOf(spaghetti);
> document.write(proto === Pasta.prototype);    //true    只有函数对象有prototype属性

3、增加/赋值（写）属性
3.1、使用 点运算符 和 数组运算操作 直接赋值：

> var obj = {name:'erha',age:18};
> obj.name = hashiqi;      //设置对象的新值，将覆盖原来的值
> obj['age'] = 100;        //设置对象的新值，将覆盖原来的值

> let key = 'age';
> console.log(obj[key]);    //100





3.2、可以通过 Object.assign() 方法进行批量赋值：（ 改方法是 ES6 新增的 API ）

> var obj = {name:'erha',age:18};
> Object.assign(obj,{name:'keji',age:22,gender:1});

> console.log(obj);    //{name:'keji,age:'22',gender:1}



3.3、无法通过修改自身属性影响原型上的属性：

> var obj = {name:'erha',age:18};
> obj.toString = 123;    //这种方式只会修改自身属性，并不会影响obj原型上的toString属性

> //如果一定要修改或增加原型上的属性，可以通过如下方式
> obj.proto.toString='xxx';        //不推荐用__proto__
> Object.prototype.toString='xxx'; //一般不要修改原型，会引起很多问题





3.4、可以通过 Object.create() 方法直接指定对象的原型：（ 改方法是 ES6 新增的 API ）

> let common = {country:China,color:yellow};

> let person = {};
> person.__proto__ = common;    //不推荐

> let person = Object.create(common);    //这种方式会直接将person的原型指向到common
> person.name = 'lixiaolong';    //对person进行赋值
> person.age = '18';             //可以在create方法中对person直接赋值，但是value书写比较麻烦



4、删除（删）属性
4.1、将对象的某个属性值赋值为 undefined：

> var obj = {name:'erha',age:18};
> obj.name = undefined;      //将obj对象的name属性赋值为undefined
> console.log(obj);          //打印结果:{name:undefined,age:18}
> console.log('name' in obj);  //true，表示obj对象中仍然含有name属性，只是属性值为undefined
> console.log(obj.hasOwnProperty('name'));    //false    表示此时的obj不含有私有属性nameconsole.log(obj.name);     //undefined    注：不能通过这种方式判断obj是否含有name属性

4.2、使用 delete 运算符删除对象的某个属性：（delete  操作符不能直接删对象）

> var obj = {name:'erha',age:18};
> delete obj.name;       //删除obj对象的name属性，也可写成:delete obj['name']
> console.log(obj);      //打印结果:{age:18}
> console.log('name' in obj);  //false，表示obj对象中没有name属性
> console.log(obj.hasOwnProperty('name'));    //false    表示此时的obj不含有私有属性name

> console.log(obj.name);     //undefined    注：不能通过这种方式判断obj是否含有name属性

以上两种删除方式的区别是：当通过 delete 删除对象的属性之后，不是将该属性值设置为 undefined，而是从对象中彻底清除属性。注意：obj.name === undefined 不能断定 name 是否为 obj 的属性，可以通过：'name' in obj && obj.name === undefined；判断 name 是否为 obj 的属性。




### 四、js进行深层次的复制


#### 浅复制
- 区分类型的复制、复杂的数据类型进行递归检测

```html 
// 用jQuery进行对象复制

// 在可以使用jQuery的情况下，jQuery自带的extend方法可以用来实现对象的复制。



a = {k1:1, k2:2, k3:3};

b = {};

$.extend(b,a);



- 转json方法如下（仅适用json那样的对象或者数组，

//如果对象或者数组中有类似Date,

//Function这种是不适用的(推荐插件lodash的cloneDeep)）

const obj = {
  key1: 'value1',
  key2: 'value2',
  key3: ['index1'],
  key4: {
    subKey1: 'subValue1'
  }
}
const obj2 = JSON.parse(JSON.stringify(obj))

1 try {
2   const obj2 = JSON.parse(JSON.stringify(obj))
3 } catch (error) {
4   const obj2 = {}
5 }
```


#### 深度复制

1.下面的方法，是给Object的原型(prototype)添加深度复制方法(deep clone)。



```JS
Object.prototype.clone = function() {
    // Handle null or undefined or function
    if (null == this || "object" != typeof this)
        return this;
    // Handle the 3 simple types, Number and String and Boolean
    if(this instanceof Number || this instanceof String || this instanceof Boolean)
        return this.valueOf();
    // Handle Date
    if (this instanceof Date) {
        var copy = new Date();
        copy.setTime(this.getTime());
        return copy;
    }
    // Handle Array or Object
    if (this instanceof Object || this instanceof Array) {
        var copy = (this instanceof Array)?[]:{};
        for (var attr in this) {
            if (this.hasOwnProperty(attr))
                copy[attr] = this[attr]?this[attr].clone():this[attr];
        }
        return copy;
    }
    throw new Error("Unable to clone obj! Its type isn't supported.");
}
```

2 使用额外的工具函数实现，适用于大部分对象的深度复制(Deep Clone)。

```
function clone(obj) {
    // Handle the 3 simple types, and null or undefined or function
    if (null == obj || "object" != typeof obj) return obj;

    // Handle Date
    if (obj instanceof Date) {
        var copy = new Date();
        copy.setTime(obj.getTime());
        return copy;
    }
    // Handle Array or Object
    if (obj instanceof Array | obj instanceof Object) {
        var copy = (obj instanceof Array)?[]:{};
        for (var attr in obj) {
            if (obj.hasOwnProperty(attr))
              copy[attr] = clone(obj[attr]);
        }
        return copy;
    }
    throw new Error("Unable to clone obj! Its type isn't supported.");
}	
```



### 五、IE与W3C区别和参数，以及IE的even的区别

#### 两者区别

- js从根文档(html)开始遍历所有子节点，如果目标事件的父节点设置为捕获时触发，则执行该事件，直到目标被执行，然后再事件冒泡(设置为捕获时触发的事件不再被执行)。

- ie事件流:从目标事件被执行，然后再冒泡父节点的事件，直到根文档。



![img](https://gitee.com/hiszm/img2021/raw/master/06/20210605143302.png)

#### 事件

- javascript事件模型:

Dom0级模型
        又称为原始事件魔性, 在该模型中, 事件不会传播, 即没有事件流的概念. 事件绑定监听函数比较简单, 有两种方式

```
// 1. html代码中直接绑定
<input type = "button" onclick = "fun()">

// 2. 通过js代码指定属性值
var btn = document.getElementById('btn');
btn.onclick = fun;

// 移除监听函数
btn.onclick = null;
```



- IE事件模型
       IE事件模型有两个过程: 事件处理和事件冒泡

```
var btn = document.getElementById('.btn');
btn.attachEvent(‘onclick’, showMessage);
btn.detachEvent(‘onclick’, showMessage);
```








> 事件冒泡流
IE 的事件流叫做事件冒泡，即事件开始时由最具体的元素（文档中嵌套层次最深的那个节点）接收，然后逐级向上传播到较为不具体的节点（文档）。以下面的 HTML 页面为例。也就是说，click 事件首先在 div元素上发生，而这个元素就是我们单击的元素，然后 click 事件沿着 dom 树向上传播，在每一级节点都或发生，直至传播到 document 对象

#### 事件的三个参数

添加事件处理函数 addEventListener

参数 1 指定事件名称...click mouseover mouseout

参数 2 事件处理程序（匿名函数或者有名函数）

参数 3 true（捕获阶段发生） or false（冒泡阶段发生）





### 六、原生JS实现事件委托


#### 概念


> **它还有一个名字叫事件代理，JavaScript高级程序设计上讲：事件委托就是利用事件冒泡，只指定一个事件处理程序，就可以管理某一类型的所有事件。**


#### 实现

```html 
<ul id="ul">
        <li>0</li>
        <li>1</li>
        <li>2</li>
        <li>3</li>
        <li>4</li>
        <li>5</li>
    </ul>
    <button id="btn">点我添加一个li</button>
    
    
    
    // 事件委托具体实现
var ul = document.getElementById("ul");
    ul.onclick = function (event) {
        event = event || window.event;
        var target = event.target;
        // 获取目标元素
        if (target.nodeName == 'LI') {
            alert(target.innerHTML);
        }
    }
    // 为按钮绑定点击事件
    var btn = document.getElementById('btn');
    btn.onclick = function () {
        var li = document.createElement('li');
        // 新增li的内容为ul当前子元素的个数
        li.textContent = ul.children.length;
        ul.appendChild(li);
    }
```
![预览](https://gitee.com/hiszm/img2021/raw/master/06/20210605202523.png)
