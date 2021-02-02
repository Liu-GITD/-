# 一个滑动隐藏的面板

1.面板设置position absolute或者fixed，把它隐藏在屏幕外面

2.设置一个按钮用lable标签绑定在一个input checkbox上

3.

input[type=checkbox]:checked + aside {

   right: 0px;

  }

使得点击lable标签内容后让隐藏面板出来，在面板的css中设置transition: 0.6s all可调整出现时间

```html
<html lang="en-us"><head><meta http-equiv="Content-Type" content="text/html; charset=UTF-8">
	
	<title>Hidden info panel</title>

  <style>
    /* || Checkbox hack to control information box display */

    label[for="toggle"] {
      font-size: 3rem;
      position: absolute;
      top: 4px;
      right: 5px;
      z-index: 1;
      cursor: pointer;
    }

    input[type="checkbox"] {
       position: absolute;
       top: -100px;
    }

    /* information box styling */

    aside {
      background-color: #a60000;
      color: white;

      width: 340px;
      height: 100%;
      padding: 0 20px;

      position: fixed;
      top: 0;
      right: -370px;

      transition: 0.6s all;
    }

    /* Second part of the checkbox hack — the checked state */

    input[type=checkbox]:checked + aside {
      right: 0px;
    }
  </style>


<body>


  <label for="toggle">❔</label>
  <input type="checkbox" id="toggle">
  <aside>
    <h2>Information</h2>

    <p>Some very important information about your app:</p>

    <ol>
      <li>It has a really cool slide-out information box.</li>
      <li>This information box uses a combination of fixed positioning and a CSS transition for the smooth sliding.</li>
      <li>It also uses a cool technique called the <a href="https://css-tricks.com/the-checkbox-hack/">checkbox hack</a>.</li>
      <li>This allows you to create a nice "toggle on/toggle off" UI effect without using any JavaScript, which will work in IE9 and above (the smooth transition will work in IE10 and above.)</li>

    </ol>

  </aside>


</body></html>
```

> 领悟



![image-20210129174643737](C:\Users\78535\AppData\Roaming\Typora\typora-user-images\image-20210129174643737.png)

# Flex布局

```css
flex: 200px;
```

在 article 元素上设置的 flex: 200px 规则，意味着每个元素的宽度至少是200px；

```css
flex-wrap: wrap;
```

```css
flex-direction: column;//默认是row  可以加个-reverse
```

![image-20210129175305666](C:\Users\78535\AppData\Roaming\Typora\typora-user-images\image-20210129175305666.png)

![image-20210129175321071](C:\Users\78535\AppData\Roaming\Typora\typora-user-images\image-20210129175321071.png)



