## sparseInt

![image-20220627153502116](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220627153502116.png)

#### 将demo的值以16进制转化为10进制



## typeof(): 会显示括号里面的数据类型

![image-20220627153932765](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220627153932765.png)



![image-20220627153719892](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220627153719892.png)





## 预编译：

![](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220627192515959.png)

## call/apply

![image-20220627154108480](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220627154108480.png)

![image-20220627154157951](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220627154157951.png)

![image-20220627154255447](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220627154255447.png)

![image-20220627154311823](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220627154311823.png)



## 可以连用方法的方法：

![image-20220627150423516](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220627150423516.png)



## 字符串拼接：

![image-20220627150552073](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220627150552073.png)



## :triangular_flag_on_post:遍历对象方法：for(var b in a)

### :triangular_flag_on_post:遍历属性名：

![image-20220627192556356](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220627192556356.png)



### :triangular_flag_on_post:遍历属性值：

![image-20220627192802952](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220627192802952.png)



#### 上图的值会打印五个undefined，得用下图的方法：因为返回的prop值为String类型，在下图中的底层来说就相当于console.log(obj[''name''])

![image-20220627193606955](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220627193606955.png)

#### 图片遍历拿出来的值连 obj的原型 --proto--的值也会拿出来，若不想要--proto--的值则需用到下图：

![image-20220628091620868](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220628091620868.png)

#### hasOwnProperty:里面传入的是对象的字符串属性，如果该属性为obj传入prop内的属性，则会返回true，如果为原型链的属性，则会返回false



### :triangular_flag_on_post:instanceof:

![image-20220628093127486](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220628093127486.png)

#### 例如： 

#### person instanceof Person   ——> true

#### person instanceof Object ——>true



### :triangular_flag_on_post:区别数组[]和对象{}的三种方法:

**①[].constructor  == Array     {}.constructor == Object**

**②[] instanceof Array ==true    {} instanceof Array ==false**

**③Object.protorype.toString.call([]) ——>[object Array]**  

**var obj =={}     Object.protorype.toString.call(obj)——>[object Object]**



### arguments:



#### ①arguments.callee:结果就等于test本身，结果打印出来就等于test函数的内容

![image-20220628141956353](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220628141956353.png)

![image-20220628142053128](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220628142053128.png)



#### 作用：实现立即执行函数中的阶乘

![image-20220628142547330](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220628142547330.png)



#### ②caller：不是arguments 的方法，是每个函数都有的方法，它的结果为谁调用这个函数的函数内容

![image-20220628143009893](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220628143009893.png)

![image-20220628143028988](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220628143028988.png)



### 类数组：

#### push原理：

![image-20220628192845522](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220628192845522.png)

![image-20220628192919703](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220628192919703.png)
