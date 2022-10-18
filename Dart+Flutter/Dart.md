## 一丶final 和 const 的区别

```json
final可以开始不赋值   只能赋值一次
final不仅有const的编译时常量的特征，最重要的时它的运行时常量，并且final时惰性初始化，即在运行时第一次使用前才初始化

```



## 二、Dart的数据类型详解

### 1.字符串类型

```dart
void main () {

  // 1.字符串的定义方式
  var str1 = 'this is str';
  var str2 = 'this is str';

  print(str1);
  print(str2);

  String str3 = 'this is str';
  print(str3);

  //此方法会保留输入字符串的格式（多行输入）
  String str4 = '''this is str
  this is str2
  ''';
  print(str4);
    
    
  //2.字符串的拼接
  String str = '你好';

  String str2 = 'zsw';

  print(str + str2);

  print("$str $str2");
  
}
```





### 2.数值类型

```dart
void main() {
  //1.int  （必须为整形）
  int a = 124;
  print(a);
  // 此处 a 为int类型，如果赋值 21.00 会报错
    
  //2.double（既可以是整形 也可以是浮点型）
  double b = 12.24;
  b = 12;
  print(b);
  // 此处b为 double类型  赋值 12 不报错
    
  //3.运算符
    
  // + - * / %
  var c  = a + b;
  print(c);	 
}
```





### 3.布尔类型

```dart
void main () {
  //1.bool

  bool flag = true;
  print(flag);

  //条件判断语句

  // if(a==b)  此处一个 = 为赋值  两个== 为判断
  var flag2 = true;
  if(flag2) {
    print("111");
  }
}
```





### 4.List（集合） 类型

```dart
void main () {
  
  //1. 第一种定义List方式

  var l1 = ["zhangsan",20,true]; 

  print(l1);//[zhangsan, 20, true]

  print(l1.length); //3

  print(l1.indexOf(20)); // 1

  print(l1[0]); // zhangsan




  //2. 第二种定义List方式(指定类型)

  var l2 = <String> ['zhangsan','zsw','ybq'] ;
  print(l2);


  //3. 第三种定义List(空数组，添加对象),(容量可变) 增加数据
  var l3 = [];
  l3.add('zsw');
  print(l3);


  //4. 第四种List创建方法 （新版本已经废弃）flutter2可用

  // var l5 = new List();

  
  //5.定义一个固定长度的集合
  var l6 = List.filled(2, "");//不指定类型一样会进行类型推导
  var l6 = List<String>.filled(2, ""); //指定类型
  l6[0] = 'ybq';
  l6[1] = 'zsw';
  // l6.add('value'); // 会报错
  // l6.length = 0 //修改集合长度 （报错）
  print(l6);

}
```





### 5.Map（字典）类型

```dart
 void main () {

  //1. 第一种定义 Maps 的方式
  var person = {
    "name": 'ybq', //key : value 形式  key必须要加 "key"
    "age": 20
  };

  print(person["name"]); //不能person.name
  print(person);


  //2. 第二种定义 Maps 的方式

  var p = new Map();

  p["name"] = 'zsw';
  p["age"]  = 21 ;

  print(p);
}
```





### 6.类型判断 （is关键词）

```dart
/**
 * Dart判断类型
 * 
 * is关键词来判断
 */

void main () {

  var str = 123;

  if(str is String) {
    print("str 是 String类型");
  }else {
    print("str是其他类型");
  }
}
```





## 三、运算符 条件判断 类型转换

![image-20221001152446072](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20221001152446072.png)

![image-20221001152800716](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20221001152800716.png)

> 注意  a/b 不会直接取整   要用~/来进行取整

![image-20221001153109657](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20221001153109657.png)

![image-20221001153544889](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20221001153544889.png)



`类型转化`：

```dart
void main () {
  //1.Number 转换为 String

  // Number 转为为 String 用 toString()
  // String 转换为 Number 用 int.parse()  double.parse()


  String str = '123';
  print(int.parse(str));

  int a = 113;
  print(a.toString());
}
```





## 四、for while  do..while break continue

```
基本等同于js
```





## 五、集合类型List Map Set详解  以及 forEach map where any every

![image-20221001155337384](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20221001155337384.png)

```dart
void main () {
  List myList = [1,2,3,3,2,1,5,6,3];
  print(myList.reversed); //(3, 6, 5, 1, 2, 3, 3, 2, 1)
  print(myList.reversed.toList()); //[3, 6, 5, 1, 2, 3, 3, 2, 1]
  print(myList); //[1, 2, 3, 3, 2, 1, 5, 6, 3]
}
// resersed方法不会影响原数组
```

![image-20221001160819801](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20221001160819801.png)





## 六、方法的定义 变量 方法作用域等

### 1.方法的定义  变量 方法作用域

![image-20221001161722758](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20221001161722758.png)

> 定义在main函数外面的方法为全局对象，全局可以调用，但是定义在函数内部的方法作用域为当前函数内



### 2.方法的传参  默认参数   可选参数

![image-20221001162256430](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20221001162256430.png)

![image-20221001162356683](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20221001162356683.png)

知道返回值类型的情况下尽量对于参数和返回值的类型进行约束

**可选参数   [  ]**

![image-20221001162459619](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20221001162459619.png)



**默认参数**

![image-20221001162556115](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20221001162556115.png)



**命名参数 { }** 

![image-20221001162657467](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20221001162657467.png)



**方法参数**

![image-20221001163018608](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20221001163018608.png)

![image-20221001162949675](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20221001162949675.png)



### :star:3.箭头函数  匿名函数  闭包

**箭头函数**

![image-20221001163322783](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20221001163322783.png)

> ## 箭头函数只能写一行



**匿名函数**

![image-20221001163709991](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20221001163709991.png)

**自执行方法(立即执行函数)**

![image-20221001163758558](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20221001163758558.png)

```dart
((){
print('111');
})();
```



**闭包**

![image-20221001163921471](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20221001163921471.png)



## 七、Dart中的类和对象

### 1.类的定义

![image-20221002145359576](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20221002145359576.png)

```dart
class Person {
  String name = 'zhangsan';
  int age = 23;

  getInfo() {
    print("${this.name} + ${this.age}");
  }

  void setAge(int age) {
    this.age = age;
  }
}

void main () {
  Person person = new Person();
  person.age = 21;
  person.getInfo();//zhangsan + 21

  person.setAge(20);
  person.getInfo();//zhangsan + 20

}
```



### 2.构造函数

```dart
class Person {
  late String name;//除了用late 还可以 String? name
  late int age;

  Person(String name,int age) {
    this.name = name;
    this.age = age;
  }// 或者 Person(this.name,this.age);这样就不用late了

  getInfo() {
    print("${this.name} + ${this.age}");
  }

}

void main () {
  Person p1 = new Person("zsw", 21);
  p1.getInfo();
}
```



### 3.命名构造函数

```dart
class Person {
  late String name;//除了用late 还可以 String? name
  late int age;

  Person(this.name,this.age);

  Person.now(){
    print("我是命名构造函数");
  }

  getInfo() {
    print("${this.name} + ${this.age}");
  }

}

void main () {
  Person p1 = new Person("zsw", 21);
  Person p2 = new Person.now();//我是命名构造函数
  p1.getInfo();//zsw + 21
}
```



### 4.类的模块化

![image-20221002152009306](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20221002152009306.png)



### 5.私有属性

![image-20221002152221350](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20221002152221350.png)

> 需要让属性私有化，前提是该属性的类以及是模块化即已经被抽离要调用私有属性的文件，而且需要专门的get方法进行获取私有属性(和java一样)



### 6.get   set

![image-20221002152613678](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20221002152613678.png)

//get方法，直接用调用属性的方式直接调用即可



![image-20221002152751441](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20221002152751441.png)

//set方法

### 7.实例化之前初始化参数

![image-20221002152855411](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20221002152855411.png)



## 八、类   静态成员   操作符  类的继承

### 1.静态成员 方法

```dart
/**
 * Dart中的静态成员
 * 1.使用static 关键词来实现类级别的变量和函数
 * 2.静态方法不能访问非静态成员，非静态成员能访问静态成员
 */

class Person {
  static String name = '张三';
  static void show() {
    print(name);
  }
}

main () {
  print(Person.name);
  Person.show();
}
```



### 2.对象操作符

```dart 
/**
 * Dart中的对象操作符
 * 
 * ? 条件运算符
 * as 类型转换
 * is 类型判断
 * .. 级联操作（重点）
 */

class Person {
  String name;
  num age;
  Person(this.name,this.age);
  void printInfo() {
    print("${this.name} --- ${this.age}");
  }
}

main() {
  Person ?p;
  p?.printInfo();//p为null就不执行

  Person p2 = new Person('name', 20);
  p2.printInfo();

  Person p3 = new Person('name', 20);
  if(p3 is Person) {
    print(111);
  }

  var p4;
  p4 = '';
  p4 = new Person('zsw', 20);
  p4.printInfo();
  (p4 as Person).printInfo(); //类型转换

  
  Person p5 = new Person('ybq', 21);
  p5..name="zsw"
    ..age = 18
    ..printInfo();
}
```



### 3.类的继承

![image-20221002155649030](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20221002155649030.png)

```dart
class Person {
   String name = '张三';
   int age = 20;
   Person(this.name,this.age);
   void show() {
    print(name);
  }
}

class Web extends Person {
  Web(super.name, super.age);
}

main() {
  Web w = new Web('name', 20);
  print(w.name);
}
```



### 4.覆写父类方法

> 建议在覆写的上面加上@override（不加也可以）

![image-20221002160859932](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20221002160859932.png)

## 



## 九、抽象类 多态 接口

### 1.抽象类

![image-20221002215110676](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20221002215110676.png)

```dart
abstract class Animal {
  eat(); //抽象方法
}

class Dog extends Animal{
  @override
  eat() {
    // TODO: implement eat
    throw UnimplementedError();
  }
  
}
```



### 2.多态

![image-20221002215514454](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20221002215514454.png)



### 3.接口(在dart没有interface，用abstract)

![image-20221002215724609](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20221002215724609.png)





## 十、一个类多个接口  dart的Mixins



### 1.一个类多个接口

```dart
class C implements A,B{}
```



### 2.Mixins(多继承)

![image-20221002223414282](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20221002223414282.png)

```dart
class A {
  String info = 'this is A';
  void printA(){
    print("A");
  }
}

class B {
  void printB(){
    print("B");
  }
}

class C with A,B{

} //extends无法实现多继承  只有将A B变为abstract才能实现多接口形式
  //但是用mixins的with可以完成类似多继承的功能

void main() {
  var c = new C();
  c.printA();//A
  c.printB();//B
  print(c.info);//this is A
}
```



## 十一、泛型   泛型方法   泛型类   泛型接口



### 1.泛型方法

![image-20221002234948819](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20221002234948819.png)

```dart
T getData<T> (T value) {
  return value;
} 

void main () {
  var p = getData<String>("ybq");
  print(p);
}
```





### 2.泛型类

```dart
class MyList<T> {
  List list = <T> [];

  void add(T value){
    this.list.add(value);
  }

  List getList() {
    return list;
  }
} 

main() {
  MyList l1 = new MyList<String>();
  l1.add("zsw");
  print(l1.getList());
}
```



### 3.泛型的接口

![image-20221003011359831](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20221003011359831.png)

```dart
abstract class Cache<T>{
  getByKey(String key);
  void setByKey(String key,T value);
}

class FileCache<T> implements Cache<T>{
  @override
  getByKey(String key) {
    // TODO: implement getByKey
    throw UnimplementedError();
  }

  @override
  void setByKey(String key, T value) {
    // TODO: implement setByKey
  }
  
}

main() {
  FileCache f = new FileCache<String>();
  f.setByKey('key', 'ybq');
}
```





## 十二、库  自定义库  系统库  第三方库

![image-20221003194344501](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20221003194344501.png)



### 1.自定义库

> 类似于Class外部封装再引用



### :star:2.系统库

```dart
import 'dart:math';

main() {
  print(min(10, 20));
}
```

系统库用来请求接口数据

![image-20221003194759575](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20221003194759575.png)



### 3.第三方库

![image-20221003194925854](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20221003194925854.png)

链接：[Page 1 | Top packages (pub.dev)](https://pub.dev/packages)

​		[Page 1 | Top packages (flutter-io.cn)](https://pub.flutter-io.cn/packages)

​		[Search results for sdk:flutter. (pub.dev)](https://pub.dev/packages?q=sdk%3Aflutter)



### 4.部分引入

![image-20221003200937112](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20221003200937112.png)



### 5.延时加载

![image-20221003201008124](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20221003201008124.png)