# :star:有需求可查询api文档

## 一.获取dom元素

```js
<div class="mydiv"></div>

$('div')   $('.mydiv')
```

## 二.将jquery对象转化为dom对象使用dom方法

```js
<div class="mydiv"></div>

$('div')[0].style.display = 'none'
或者
$('div').get(0).style.display = 'none'
```



## :star:三.常用API

### 	jQuery选择器(隐式迭代)：

![image-20220722110508143](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220722110508143.png)

![image-20220722110726363](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220722110726363.png)

​	![image-20220722113144440](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220722113144440.png)

![image-20220722142420608](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220722142420608.png)

```js
<div class="mydiv"></div>
<div class="mydiv"></div>
<div class="mydiv"></div>
    <script>
       $('div').css("background-color",'red')
    </script>
```



#### :star:1.隐式迭代：

**jquery在用$('div')时会把div元素全部获取并且遍历一遍，所以用$('div').css('background','pink')会把所有的div背景变化,排他思想就运用了隐式迭代**

#### :star:2.排他思想：

```js
    <button>换背景</button>
    <button>换背景</button>
    <button>换背景</button>
    <script>
$('button').click(function(){
$(this).css('background-color','red')
$(this).siblings().css('backgroundColor',"")//分开写法
        
$(this).css('backgroundColor','red').siblings().css('backgroundColor',"")//链式写法
})
    </script>
```

排他思想通过siblings()方法和jquery中的隐式迭代来完成原生css js中繁琐的一些行为

## :star:四.jQuery的样式操作

### 1.操作css的方法

```js
 $('div').css('width');//返回的为div的宽值
 $('div').css('width','100px');//修改值,如果值为数字可以不用引号
 $(this).css({'width':"100px","height":'10px'})//修改多个数据
 $(this).css({
    width:"100px",
    height:200,
    "background-color":"skyblue"
    // backgroundColor:"skyblue"
    //复合属性要用小驼峰式
 })
```

如果css里面不修改相应的值，返回值就会是所选元素的相应值

### 2.添加类，删除类，切换类

**和原生js不一样，jquery对于类的操作不会覆盖掉dom元素原有的class属性**

```
$('div').addClass('newclass')//添加类一定不要加.
$('div').removeClass('newclass')//删除类
$('div').removeClass()//删除所有类
$('div').click(function(){
    $("div").toggleClass('newclass')
})//切换类，如果有这个类就删除，没有就添加
```

可用链式方法:

```
$('div').addClass('class').siblings().removeClass('class')
```



## 五.jQuery效果

###  1.show()和 hide()和toggle()

**和display:none的效果一样控制元素的显示和隐藏**

```js
$('div').show()   $('div').hide()  $('div').toggle()
toggle()用来判断是否隐藏，若没隐藏点击就隐藏，隐藏点击就显示
show([speed],[easing],[fn])//参数
1.参数都可以省略，无动画显示
2.speed:显示速度("slow","nomal","fast")或填毫秒数1000
3.easing:切换效果，默认"swing",可以用"linear"
3.fn:回调函数
hide()  toggle()同上
```



### 2.滑动效果 

```js
slideDown()、slideUp() 、sildeToggle()
参数和上面的一致，完成的效果就是类似于小米商城下拉框一致
```



### 3.事件切换 hover()

**如果hover内只写一个函数，那over和out都会调用这个函数**

```js
hover(over,out)
1.over:鼠标移入要触发的函数(相当于mouseenter)
2.out:鼠标移出触发的函数(mouseleave)

$('div>li').hover(function(){
	$(this).children('ul').sildeDown(200);
},function(){
	$(this).children('ul').sildeUp(200);
})//写两个函数

$('div>li').hover(function(){
    $(this).children('ul').slideToggle(200)
})//写一个函数
```



### :star:4.动画队列及其停止排队方法

#### 	①动画或效果队列

​	动画或者效果一旦触发就会执行，如果多次触发，就造成多个动画或者效果排队执行.（就像上面的hover情况连续多次滑动几个li会导致前面的li效果还么停止后面的就已经在加载了，stop()可以解决）

####   ②停止动画stop()

```js
$('div>li').hover(function(){
    $(this).children('ul').slideToggle(200)
})//效果队列有bug

$('div>li').hover(function(){
    $(this).children('ul').stop().slideToggle(200)
})//停止动画，如果stop写在后面就会导致动画不加载或者不移除
```



### 5.淡入淡出效果(也要借助stop停止动画)

fadeIn() 、fadeOut() 、fadeToggle 、**fadeTo()**

```
fadeIn()  fadeOut()  fadeToggle()//淡入淡出可以修改所选元素的透明度达到效果里面的参数和show()的一样


fadeTo(speed,opacity,[easing],[fn])
opacity:透明度，必填参数0-1之间
speed:速度，必填参数
```



### 	:star:6.自定义动画

```js
animate(params,[speed],[easing],[fu])

1.params:想要修改的样式属性，必须填，属性名可以不带引号，如果是符合属性则需要用小驼峰命名法

$('div').animate({
	left:100,
	top:200,
	opacity:0.5
},500)
```



## 六.jQuery属性操作

### 	1.获取、修改元素固有属性 prop( )

```js
<a href="www.baiddu.com"></a>

$(function(){
	$("a").prop("属性名href")//jquery获取元素固有属性值
	$("a").prop("title","aaa")//修改属性值
})

```



### 	2.获取、修改元素自定义属性 attr()

```js
<a href="www.baiddu.com" index="1"></a>

$(function(){
	$("a").attr("index")//获取
    $("a").attr("index",2)//修改
})
```



### 	3.数据缓存data( )

data里面存放的数据是放在元素内存内的，不会修改dom结构，页面刷新后存放的数据就会被移出

```js
<span>123</span>

$('span').data("uname","andy")//在span元素中存放uname数据可以获取h5的data属性
```



## 七、jQuery内容文本值

```js
1.html()
$('div').html()//显示该元素的内容
$('div').html("124")//修改元素内容

2.text()//文本内容
$('div').text()
$('div').text("123")//修改文本内容

3.val()
$('input').val()//获取表单内容
$('input').var("123")//修改表单内容

```



## 八、jQuery元素操作

### 	:star:1.遍历元素

```js
$('div').each(function(index,domEle){})
1.each()方法遍历匹配的每一个元素，主要用DOM处理。
2.里面的回调函数有两个参数:index是每个元素的索引号；domEle是每个DOM元素对象，不是jquery对象
3.所以想要使用jquery方法，需要给这个DOM元素转换为jquery对象$(domEle)


$.each($('div'),function(index,domEle){})
1.$.each()可以用于遍历任何对象，主要用于数据处理，比如对象 数组
```



