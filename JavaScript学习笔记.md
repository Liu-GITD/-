













# 狂神 JavaScript

# 	

# 1，数据类型

## 1.1字符串

### 1、正常字符串用单引号或双引号包裹

### 2、注意转义字\

### 3、多行字符串编写

```javascript
//tab 键上面那个
var msg = `
sad
asdef
rg`
```

### 4、模板字符串

```javascript
//tab 键上面那个
let name="lxq"
let msg=`你好呀，${name}`
```

### 5、字符串长度

```javascript
str.length
```



### 6、字符串的可变性，不可变！

```javascript
var student = "student";
student[0]=1;
console.log(student);//结果还是student
```



### 7、大小写转换

```javascript
student.toUpperCase()//注意这里是方法而不是属性了

student.tolowerCase()
```



### 8、student.indexOf('t')

获取下标





### 9、substring(1,3)

左闭右开截取字符串





## 1.2比较运算符

```
= 
== 等于（类型不一定一样，值一样，就为true）
=== 绝对等于（类型一样，值一样，才为true）
```

这是JS的一个缺陷，坚持不要用==

须知

- NaN===NaN 	结果为false因为这个与所有数不相等，包括自己
- 只能通过isNaN来判断是否为NaN



​	1/3和1-2/3是不相等的，要判断则需要使用Math.abs(1/3-(1-2/3)<0.000001) 这个就是true

## 1.3数组

```javascript
var arr = [1,2,3,"asd",null,true]//没有要求必须是同一类型
```

### 1、长度

```
arr.lenght
```

### 2、indexOf 

通过元素获得下标索引



### 3、slice()

类似于字符串中的substring

slice(3)从第三个截取到最后，返回新数组

slice(1,3)左闭右开



### 4、push() pop()

尾部操作



### 5、unshift(),shift()

理解为头部的入栈出栈操作

### 6、元素反转

arr.reverse()

### 7、拼接

arr.concat([1,2,3])//arr后面拼接123，并没有改变arr，只是返回新的数组











## 1.4对象

对象用大括号括起来，数组中括号。

若干个键值对



JavaScript中所有键都是字符串，值是任意对象

```javascript
var person = {
    name:"lxq",
    age:123,
    class:1
}
```

### 1、赋值

```javascript
person.name="abc"
```

### 2、使用不存在的对象属性，不会报错，而是undefined

```javascript
person.haha
undefined
```



### 3、动态增减属性

```javascript
delete person.name
true
person.haha="haha"
```





### 4、判断属性是否在对象中 'xxx' in xxx

```javascript
'age' in person
true
age in person//报错


```



### 5、继承问题

```javascript
'toString' in person
true
//因为这是继承了父类
//用hasOwnProperty()可以判断自身是否拥有某属性
person.hasOwnProperty('toString')
false
```





## 1.5流程控制



### forEach循环

```javascript
var age = [12,31,12,424,53]

age.forEach(function(value){
    console.log(value)
})
```





### for..in循环

```javascript
//for (var index in object){}
//遍历数组的时候才是索引
for(var num in age){
    console.log(age[num])
}
```

### for..of循环

```javascript
for(var num of arr){
    console.log(num)
}//遍历数组

for(var num of map){
    console.log(num)
}//遍历map

for(var num of set){
    console.log(num)
}//遍历set都可以直接用num
```



## 1.6严格检查模式

把'use strict'写在js代码的第一行





## 1.7Map和Set



### ES6的新特性

Map:

```javascript
var map = new Map([['tom',100],['jack',99],['john',98]]);
var name = map.get('tom');
map.set('admin',100);
map.delete('tom')
//似乎可以理解为键值对
```



Set:无序不重复的集合，会去重

```javascript
var set = new set([1,2,3,4,5,5,5,5])//只保留一个5
set.add(6);
set.delete(1);
console.log(set.has(3));

```



# 2，函数



## 2.1 定义函数

### 1、参数问题

> 多个参数问题

arguments包含了传进来的所有参数

```javascript
function abs(x){
    console.log(x);
}
abs(1,2,2,3,1,4)//x只会用到第一个参数，后面的可以用arguments来用，所有参数都以数组形式放在arguments中
```





ES6新特性

> rest

```javascript
function aaa(a,b,...rest){
    console.log(rest);//rest保存了除前两个参数外的所有传进来的参数
}
```

## 2.2变量作用域



var定义变量实际是有作用域的

假设再函数体中声明，则再函数体外不可使用

```javascript
function qj(){
    var x = 1;
    x = x+1;
}
x=x+1;//x is not defined
```



内部函数可以使用外部的成员，反之不行

```javascript
function a(){
    var x=1
    function b(){
        var y=x+1;//2
    }
    var z =y+1;//报错
}
```



内外重名时 函数查找变量时由内到外查找

```javascript
function a(){
    var x=1
    function b(){
        var x=2;
        console.log(x);
    }
    console.log(x);//1
    b();//2
}
```

> 提升作用域

```javascript
function qj(){
    var x='x'+y;
    console.log(x);
    var y='y';
}
```

![image-20210128112728654](C:\Users\78535\AppData\Roaming\Typora\typora-user-images\image-20210128112728654.png)

等价于

```javascript
function qj(){
    var y;
    var x='x'+y;
    console.log(x);
    y='y';
}
```



说明js引擎会提升声明，但不会提升变量的赋值

> 规范

由于我们所有的全局变量都会绑定在window上，所以当有多个js文件使用了相同全局变量名，就会发生冲突，

解决的方式：



```javascript
//唯一全局变量  把所有变量绑定在这里
var kuang{};

//定义全局变量
kuang.name='lxq';
kuang.add = function(){
    xxxx
}
//把自己的代码放入自己定义的唯一空间中
```

> 局部作用域let

```javascript

 for(let i=0;i<100;i++){
     console.log(i);
 }
 console.log(i)//i is not defined
}
```





## 2.3 方法

> 定义方法

方法就是把函数定义在对象内部

```javascript
var aaa = {
	a:3,
	b:function(){
        colsole.log();
    }
}

aaa.b();//调用，this指向aaa对象
```

# 

# 

# 百度学院作业：

## 1、实现十进制转换二进制

(http://ife.baidu.com/course/detail/id/46)

```html
<body>
  <input id="dec-number" type="number" placeholder="输入一个十进制非负整数">
  <input id="bin-bit" type="number" placeholder="输入转化后二进制数字位数">
  <button id="trans-btn" onclick="dec2bin(document.getElementById('dec-number').value)">转化为二进制</button>
  <p id="result">运算结果</p>
  <script>
    function paddingZero(num,lenght){
      for(var i=0;i<lenght;i++){
        num="0"+num;
      }
      return num;
    }//在数前面补0
      
    function dec2bin(decNumber) {
      //var num=document.getElementById("dec-number").value;
      var num = decNumber;
      var bit = document.getElementById('bin-bit').value
      var i = 0;
      var k = 1;
      var j = 0;
      while ((num / 2) != 0) {
        i = i + k * (num % 2);
        num = parseInt(num / 2);
        k = k * 10;
        j++
      }
      console.log('j=='+j);
      if (bit < j) {
        console.log("位数太小")
        alert("位数太小")
        document.getElementById("result").innerHTML = decNumber + "的二进制形式为： " + i;
      } else {
        i=paddingZero(i,bit-j);
        document.getElementById("result").innerHTML = decNumber + "的二进制形式为： " + i;
      }
    }
// 实现党点击转化按钮时，将输入的十进制数字转化为二进制，并显示在result的p标签内
// 新的需求是，转化显示后的二进制数为bin-bit中输入的数字宽度，例如
// dec-number为5，bin-bit为5，则转化后数字为00101
// 如果bin-bit小于转化后的二进制本身位数，则使用原本的位数，如dec-number为5，bin-bit为2，
// 依然输出101，但同时在console中报个错
// Some coding

  </script>
</body>
```

> 收获

`document.getElementById("xxx").value	.innerHTML	.其他`

`parseInt在js中得到整形数`

`在数前面补0`

## 2、DOM操作

> 操作HTML标签元素

```javascript
document.querySelector("xxx")
```

现在用[`Document.createElement()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/createElement)创建一个新的段落

现在可以用[`Node.appendChild()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/appendChild)方法在后面追加新的段落

使用[`Document.createTextNode()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/createTextNode)创建一个文本节点

现在获取内部连接的段落的引用，并把文本节点绑定到这个节点上：

```javascript
var linkPara = document.querySelector('p');
linkPara.appendChild(text);
```

如果你想做一个副本并也把它添加进去，只能用[`Node.cloneNode()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Node/cloneNode) 方法来替代。

```javascript
var dupNode = node.cloneNode(deep); //deep可以是true or false
```







> 操作CSS样式



#### 1、方法1



```javascript
para.style.color = 'white';
para.style.backgroundColor = 'black';
```

 [`Element.setAttribute()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/setAttribute) 

```javascript
para.setAttribute('class', 'highlight');
```

#### 2、方法2

##### 		1先构建一个样式

```css
<style>
.highlight {
  color: white;
  background-color: black;
  padding: 10px;
  width: 250px;
  text-align: center;
}
</style>
```

##### 		2修改元素的class

​		 [`Element.setAttribute()`](https://developer.mozilla.org/zh-CN/docs/Web/API/Element/setAttribute) 

```javascript
para.setAttribute('class', 'highlight');
```

## 3、动态购物列表

https://developer.mozilla.org/zh-CN/docs/Learn/JavaScript/Client-side_web_APIs/Manipulating_documents#%E4%B8%BB%E5%8A%A8%E5%AD%A6%E4%B9%A0_%E4%B8%80%E4%B8%AA%E5%8A%A8%E6%80%81%E7%9A%84%E8%B4%AD%E7%89%A9%E5%8D%95

```html

<body>
  <h2>购物清单</h2>
  <div>
    <span>添加项目</span>
    <input id="newItem" type="text">
    <input type="button" value="add" onclick="add()">

  </div>
  <ul>

  </ul>



  <script>
    function add() {
      var item = document.getElementById("newItem").value;
      var li = document.createElement('li');
      var ul = document.querySelector('ul');
      li.innerHTML = item;
      var btn = document.createElement('button');
      btn.innerHTML = "delete";
      btn.id = item;
      btn.onclick = function () {
        ul.removeChild(li)
      };
      ul.appendChild(li);
      li.appendChild(btn);
    }
  </script>
</body>

```

> 收获

卡在了删除按钮那里，一开始想的是另外声明一个delete()，但出现btn.onclick =？？的传参问题

`还没想出解决办法。`

# 

# 

# 	Pink JavaScript

# 一、数据类型

> 目标

##### 说出五种简单数据类型

##### 使用typeof获取变量类型

##### 说出一两种转换为数值类型的方法

##### 说出一两种转换为字符型的方法

##### 什么是隐式转换





## 1、Number



## 2、String

在字符串中要使用单引号或者双引号，要" ' ' "配合使用

## 3、Boolean



## 4、Undefined,Null



```javascript
undefined+"xxx"//underfinedxxx
undefined+1 //NaN


null+"xxx"  //nullxxx
null+1  //1
```

## 5、判断数据类型

记住一个

```javascript
var aaa=null;
typeof aaa //object 而不是null
```

## 6、数据类型转换

### 6.1、转换为字符串

toString()

String()强制转换

加号拼接''       也叫隐式转换

### 6.2、转换为数字型

parseInt(String)

parseFloat(String)

Number()

隐式转换（用运算符 -  *  /）  '12'-0  就把字符串12变成数字型

### 6.3、转换为布尔型

Boolean()

