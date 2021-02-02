# 1.Function 

## 	1、Function 构造器与函数声明之间的不同



![image-20210125203707873](C:\Users\78535\AppData\Roaming\Typora\typora-user-images\image-20210125203707873.png)





## 2、return相关

如果一个函数中没有使用return语句，则它默认返回`undefined`。

> **但是**

```javascript
 function abs(x){
            if(x>=0){
                return x;
            }else{
                return -x;
            };
        }//如果用 abs(),则返回NaN而不是undefined!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
```

## 3、参数相关

如果实参是一个包含原始值(数字，字符串，布尔值)的变量，则就算函数在内部改变了对应形参的值，返回后，该实参变量的值也不会改变。如果实参是一个对象引用，则对应形参会和该实参指向同一个对象。



## 4、定义相关



**函数声明过程在整个程序执行之前的预处理就完成了，所以只要在同一个作用域使用就可以直接调用且不管定义在调用前后位置**

![image-20210125220956857](C:\Users\78535\AppData\Roaming\Typora\typora-user-images\image-20210125220956857.png)



### 函数声明

![image-20210125221122076](C:\Users\78535\AppData\Roaming\Typora\typora-user-images\image-20210125221122076.png)

### 函数表达式

![image-20210125221156591](C:\Users\78535\AppData\Roaming\Typora\typora-user-images\image-20210125221156591.png)

![image-20210125221215661](C:\Users\78535\AppData\Roaming\Typora\typora-user-images\image-20210125221215661.png)







# 2.生成器Generator

## 1、使用场景

https://blog.csdn.net/weixin_43964148/article/details/106878215

## 2、仍然疑惑的

![image-20210126204628404](C:\Users\78535\AppData\Roaming\Typora\typora-user-images\image-20210126204628404.png)

![image-20210126204638393](C:\Users\78535\Desktop\image-20210126204638393.png)

有什么区别？

# 3.this

## 1、绑定规则

### 	1、默认绑定规则  

​		函数独立调用时

​		foo();

​		或者在全局标签中，this===window 即相应的全局对象

### 	2、隐式绑定规则

​		谁调用就指向谁

```javascript
var obj = {
    a:2,
    foo:function(){
        console.log(this);
    }
}
obj.foo();
```

![image-20210126214748410](C:\Users\78535\AppData\Roaming\Typora\typora-user-images\image-20210126214748410.png)



```javascript
var obj = {
    a:2,
    foo:function(){
        console.log(this);// 1
        function test(){
        	console.log(this);// 2
		
        }
        test();//这里相当于函数独立调用，所以是默认指向window  
    }
}
obj.foo();//1 和2指向的不是同一个this，函数执行时会产生一个this，虽然两个this可能会指向同一个对象，但不会相同

```



![image-20210126220257655](C:\Users\78535\AppData\Roaming\Typora\typora-user-images\image-20210126220257655.png)

```javascript
var a =0;
        function foo(){
            console.log(this);
        }

        function bar(fn){
            fn(obj);	//window
            var test = new fn();//foo
            fn.bind(obj)();
        }
        var obj={
            a:1,
            foo:foo
        }

        bar(obj.foo)
```







### 3、显示绑定规则

call apply bind

### 4、new绑定



new person()的this就是指向new的实例





## 2、优先级问题

1、https://www.bilibili.com/video/BV1NT4y1j7xH?p=2   20：00

**不懂**

# 4.闭包

> 当函数执行，导致函数被定义，并抛出，就产生闭包



```javascript
var obj = {
    a:2,
    foo:function(){
        console.log(this);// 1
        function test(){
        	console.log(this);// 2
		
        }
        return test;//抛出 
    }
}
obj.foo()();//2仍然指向window  因为obj.foo()执行完后返回一个test   相当于test(); 又是独立调用


var bar=obj.foo;
bar();
```

