## DOM继承(结构)树

![image-20220630102553277](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220630102553277.png)

![image-20220704092823978](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220704092823978.png)

domTree重新排列叫做 reflow重排，后面的操作都会使它重排，非常影响程序的时间。程序应该尽量避免重排，但是修改颜色等重绘影响就比较小。

![image-20220630103226419](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220630103226419.png)

##### *第三点：比如div里面一个span标签，外面一个span标签，可以用div.getElementsByTagNames('span')[0]来选择div里面的span标签**



![image-20220630111001407](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220630111001407.png)

#### 						![image-20220630111148383](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220630111148383.png)

#### 	插：div.insertBefore(a,b)    相当于在div标签里面的b标签前面插入a标签



![image-20220630141527812](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220630141527812.png)



## JS定时器

![](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220630152314388.png)

### ①setInterval：----定时循环器  循环执行

![image-20220630152523638](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220630152523638.png)

#### 每隔1000毫秒执行一次function函数，但是time的值只会识别一次，之后修改属性的值，time的值不会被改变 



### ②clearInterval：

![image-20220630153505529](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220630153505529.png)

#### setInterval的返回值timer是他的唯一标识(数字1-正无穷，一个计时器就为1)



### ③setTimeout：------定时器，只执行一次

![image-20220630153907680](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220630153907680.png)



### ④clearTimeout：

![image-20220630154101461](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220630154101461.png)

#### 		这里的timer值机制和上面的setInterval一样，但是两个的唯一标识值不会出现重复的情况



### 注意：上面的四个方法都是window上的方法，他们的内部函数的this指向都为window



## DOM基本操作(有印象即可，后期可调用)

![image-20220630160128411](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220630160128411.png)



## 获取窗口属性

![image-20220701103257829](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220701103257829.png)

![image-20220701103327783](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220701103327783.png)

![image-20220701103409062](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220701103409062.png)

### 不常用

#### domEle：表示的是获取的标签元素的值 ：例：var div = document.getElementsByTagName('div')[0];       div.getBoundingClientRect();



![image-20220701104045265](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220701104045265.png)

#### 求出来的 div.offsetWidth和div.offsetHeight等都是视觉的宽高(如果用padding来修改视觉大小，该返回值也会变大)

![image-20220701104658169](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220701104658169.png)



## 脚本化CSS

![image-20220701143215211](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220701143215211.png)

#### div.style 只显示取出div的行间样式style

![image-20220701143450402](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220701143450402.png)

#### 如果getComputedStyle里面不写null，则可以选择该ele元素的伪元素 可以写after等来得到伪元素的样式

![image-20220701143947829](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220701143947829.png)

#### currentStyle是IE特有属性，了解即可

## 封装兼容：

![image-20220701144116980](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220701144116980.png)

#### 该方法可以通过传入元素及其你所想得到的属性，计算出你所要的结果(主要解决的是兼容性问题)



## 事件

![image-20220701153050868](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220701153050868.png)

#### addEventListener可以为同一个绑定多个处理函数(必须为不同处理函数)，以下函数可行，因为这两个函数内容一样但是他的地址不一样，不是一个函数。

#### 但是attachEvent可以实现多次 若事件type为click则为 attachEvent('onclick',function(){})

![image-20220701154320472](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220701154320472.png)



![image-20220701174110498](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220701174110498.png)

#### 第三类让this指向dom元素本身可以用外部函数.call来改变this指向，如下图

![image-20220701174525520](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220701174525520.png)

# 封装兼容：(常用)

![image-20220701191357263](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220701191357263.png)





## 解除事件的方法：

![image-20220701191548860](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220701191548860.png)

![image-20220701191645204](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220701191645204.png)



## 事件处理模型：

![image-20220701192029101](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220701192029101.png)



![image-20220701193151976](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220701193151976.png)

## 封装：

![image-20220701193435921](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220701193435921.png)



### 防止右键出菜单的事件

![image-20220701193639837](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220701193639837.png)



## 封装右键菜单

![image-20220701193852166](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220701193852166.png)

#### 一个函数的返回值无法完成return false的结果



### 防止a标签点击跳转和刷新功能：

![image-20220702090638939](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220702090638939.png)



## 事件源对象

![image-20220702092305598](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220702092305598.png)

#### 类似于你的wrapper盒子上有一个box盒子，你点击box盒子也会冒泡让wrapper盒子的事件发生，且事件中有一个源对象属性，所以target返回的值是点击的最初对象的值，所以点击box会返回box为源对象。一些元素要往父级里面加很多元素，而且子元素要有点击事件，这样如果把点击事件绑定在子元中，耗时多而且不灵活，就可以把事件绑定在父元素中然后用父元素.target事件，这样即使点击子元素也会冒泡到父元素执行父元素事件，找到相应的子元素对象。



### 封装事件源对象：

![image-20220702092758283](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220702092758283.png)

#### 这里的event语句是兼容其他浏览器的event对象



### 事件委托：

![image-20220702093143264](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220702093143264.png)

![image-20220702093202718](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220702093202718.png)



## 事件分类：

![image-20220702093832794](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220702093832794.png)



![image-20220702095929934](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220702095929934.png)



#### e.button事件 结果为 0 1 2 分别未为鼠标左键 鼠标中间  鼠标右键，可以用   .onmousedown和 .onmouseup事件来执行（注意：onclick不行）





### 键盘事件：

![image-20220702104200888](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220702104200888.png)



#### keydown主要来监测一些键盘的应用类按键类似shift等

#### keypress主要来监测一些字符类按键，如果字符用down会不准，可以在press事件中的charCode来检测键盘的相应字符。

![image-20220702105909322](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220702105909322.png)

#### String.fromCharCode可以把相应的ASCII码转化为字符



### 文本事件：

![image-20220702110029821](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220702110029821.png)



#### elm.oninput：返回值为文本框的内容（只要文本框的内容发生改变就会触发）

#### elm.onchange:只有当改变后失去文本框焦点才会触发

#### 其他两个事件能做到类似于placeholder的效果



![](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220702110706338.png)





## JSON

![image-20220704093042463](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220704093042463.png)



## 异步加载

![image-20220704093314725](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220704093314725.png)



![image-20220704093258720](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220704093258720.png) 

![image-20220704094244043](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220704094244043.png)

```javascript

<script type="text/javascript" async="async" src="tools.js"></script>
```



#### 第三种方法使用最广泛

![image-20220704095221633](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220704095221633.png)



#### 当需要及时调用js中的函数时，直接调用函数可能会因为还未下载完js就已经执行方法导致报错，可以用下图的方法等到下载完js时才执行函数(此方法兼容行十分好除了IE)

![image-20220704095841663](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220704095841663.png)

#### IE的方法

![image-20220704103836221](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220704103836221.png)

#### 兼容包装：

![image-20220704104346480](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220704104346480.png)

![image-20220704104755233](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220704104755233.png)

#### src放在事件后是因为防止速度过快导致在执行函数前js就已经下载完成了，导致下面的函数无法确认readyState的值是否改变而无法调用函数。

#### 图二不直接使用test的原因是：你还没下载成功js直接写js代码里面的test()，会导致无法编译，用函数的方法可以等到上面函数执行时获取到function（）{}里面的test。

### 如果js的代码规范的话，下面的方法更优：

![image-20220704105158709](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220704105158709.png)



## JS时间线

![image-20220704110540391](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220704110540391.png)

# 正则表达式

![image-20220704144959471](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220704144959471.png)

![image-20220704145017956](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220704145017956.png)

![image-20220704145348490](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220704145348490.png)

![image-20220704192523510](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220704192523510.png)

![image-20220704192544248](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220704192544248.png)

![image-20220704192553598](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220704192553598.png)

![image-20220704192605244](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220704192605244.png)

![image-20220705093046607](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220705093046607.png)

#### a（？=b）表示a后面跟着的是b且搜索的结果不包含b进入

![image-20220705093143312](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220705093143312.png)

#### a(？！b)表示a后面没有跟着的是b且搜索的结果不包含b进入