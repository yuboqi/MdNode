# JS



# forEach()遍历

![image-20220706183106137](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220706183106137.png)



# filter()筛选

![image-20220706183338043](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220706183338043.png)

![image-20220706183502830](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220706183502830.png)



# some()查找是否有满足条件的元素

![image-20220706183756093](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220706183756093.png)

![image-20220706183911202](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220706183911202.png)

#### some返回值为布尔类型(false true)



# filter 和 some区别

![image-20220706184237057](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220706184237057.png)



# 实例1：用forEach页面渲染

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        input{
            width: 50px;
        }
        .search{
            width: 700px;
            margin: 0 auto;
            margin-bottom: 20px;
        }
        table{
            width: 700px;
            margin: 0 auto;
        }
    </style>
</head>
<body>
    <div class="search">
        按照价格查询：<input type="text" class="start">-<input type="text" class="end">
        <button class="search-price">搜索</button>按照商品名称查询：<input type="text" class="product">
        <button class="search-pro">查询</button>
    </div>

    <table border="1" cellspacing="0">
        <thead>
            <th>id</th>
            <th>商品名称</th>
            <th>价格</th>
        </thead>

        <tbody>

        </tbody>
    </table>

    <script>
        var data = [{
            id:1,
            pname:'小米',
            price:3999
        },{
            id: 2,
            pname: 'oppo',
            price: 999
        },{
            id: 3,
            pname: '荣耀',
            price: 1299
        },{
            id: 4,
            pname:'华为',
            price: 1999
        },]

        // var tbody = document.getElementsByTagName('tbody')[0];
        var tbody = document.querySelector('tbody');
        data.forEach(function(value){
            var tr = document.createElement('tr');
            tr.innerHTML = '<td>'+value.id+'</td> <td>'+value.pname+'</td> <td>'+value.price+'</td>';
            tbody.appendChild(tr);
        })
    </script>
</body>
</html>
```



# 实例完善：实现筛选和查询功能

![image-20220706193007939](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220706193007939.png)

![image-20220706193033654](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220706193033654.png)

```
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        input{
            width: 50px;
        }
        .search{
            width: 700px;
            margin: 0 auto;
            margin-bottom: 20px;
        }
        table{
            width: 700px;
            margin: 0 auto;
        }
    </style>
</head>
<body>
    <div class="search">
        按照价格查询：<input type="text" class="start">-<input type="text" class="end">
        <button class="search-price">搜索</button>按照商品名称查询：<input type="text" class="product">
        <button class="search-pro">查询</button>
    </div>

    <table border="1" cellspacing="0">
        <thead>
            <th>id</th>
            <th>商品名称</th>
            <th>价格</th>
        </thead>

        <tbody>

        </tbody>
    </table>

    <script>
        var data = [{
            id:1,
            pname:'小米',
            price:3999
        },{
            id: 2,
            pname: 'oppo',
            price: 999
        },{
            id: 3,
            pname: '荣耀',
            price: 1299
        },{
            id: 4,
            pname:'华为',
            price: 1999
        },]
        //获取元素
        // var tbody = document.getElementsByTagName('tbody')[0];
        var tbody = document.querySelector('tbody');
        var start = document.querySelector('.start');
        var end = document.querySelector('.end');
        var search_price = document.querySelector('.search-price');
        var search_pro = document.querySelector('.search-pro');
        var product = document.querySelector('.product');
        setDate(data);
        //渲染页面
        function setDate(mydata){
            tbody.innerHTML = '';
            mydata.forEach(function(value){
            var tr = document.createElement('tr');
            tr.innerHTML = '<td>'+value.id+'</td> <td>'+value.pname+'</td> <td>'+value.price+'</td>';
            tbody.appendChild(tr);
        })
        }

        //范围查询
        search_price.addEventListener('click',function(){
            var newDate = data.filter(function(value){
                return value.price>=start.value && value.price<=end.value;
            })
            setDate(newDate);
        })


        //按照商品名称查询(some合适，filter耗时)
        search_pro.addEventListener('click',function(){
            data.some(function(value){
                if(value.pname ===product.value){
                    setDate([value]);
                    return true;//终止循环
                }
            })
        })
    </script>
</body>
</html>
```



# forEach()和some()区别

![image-20220706193956502](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220706193956502.png)



# trim()方法 返回值是一个字符串

![image-20220706194042635](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220706194042635.png)

![image-20220706194150964](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220706194150964.png)

#### 常用范围：判断文本框内容为空当输入空格判断不为空的现象，解决在下图

![image-20220706194606151](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220706194606151.png)



# Object.defineProperty()对象方法

![image-20220706194943576](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220706194943576.png)

![image-20220706195039427](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220706195039427.png)

![image-20220706195347564](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220706195347564.png)

![image-20220706195525984](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220706195525984.png)



# 函数定义

![image-20220706200154132](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220706200154132.png)

![image-20220706200237300](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220706200237300.png)

![image-20220706195846433](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220706195846433.png)

![image-20220706195953436](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220706195953436.png)



# 函数调用方式



![image-20220706201549046](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220706201549046.png)

![image-20220706201632565](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220706201632565.png)

![image-20220706201739955](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220706201739955.png)

![image-20220706201747231](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220706201747231.png)



# 改变this指向

## call

![image-20220706201939495](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220706201939495.png)



## apply

![image-20220706201954240](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220706201954240.png)



## bind  不会调用函数（最常用）

![image-20220706202240313](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220706202240313.png)

![image-20220706202435436](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220706202435436.png)



## 应用：

![image-20220707094737280](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220707094737280.png)



# call apply bind总结

![image-20220707095010311](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220707095010311.png)



# 严格模式

![image-20220707095232208](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220707095232208.png)

![image-20220707095430241](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220707095430241.png)

### 变量规定

![image-20220707095705317](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220707095705317.png)

### this指向问题

![image-20220707100021847](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220707100021847.png)

### 严格模式下函数问题

![image-20220707100243593](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220707100243593.png)



# 浅拷贝 深拷贝

### 浅拷贝

![image-20220707103625605](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220707103625605.png)

### 深拷贝

![image-20220707104109692](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220707104109692.png)





# ES6

## 	let特点 

![image-20220707104529381](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220707104529381.png)****



![image-20220707104748367](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220707104748367.png)



## 	const

![image-20220707105327102](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220707105327102.png)

![image-20220707105602582](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220707105602582.png)



## 	var let const区别

![image-20220707105628035](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220707105628035.png)



# 解构赋值

## 	数组解构

![image-20220707110051755](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220707110051755.png)

![image-20220707110001489](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220707110001489.png)

​	

## 	对象解构

![image-20220707110140119](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220707110140119.png)

![image-20220707110348704](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220707110348704.png)



# 箭头函数

![image-20220707110618459](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220707110618459.png)

![image-20220707110729064](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220707110729064.png)



## 	箭头函数的this关键字

![image-20220707111028255](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220707111028255.png)



# 剩余参数

![image-20220707111118746](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220707111118746.png)

![image-20220707111244184](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220707111244184.png)

![image-20220707111646049](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220707111646049.png)



# 扩展运算符

![image-20220707111858825](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220707111858825.png)

## 	合并数组

![image-20220707112005017](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220707112005017.png)

## 	伪数组转换

![image-20220707112237828](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220707112237828.png)



# Array.from()将伪(类)数组转换为数组

![image-20220707112327529](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220707112327529.png)

![image-20220707112417612](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220707112417612.png)

# find()

![image-20220707112543355](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220707112543355.png)



# findIndex()

![image-20220707112747526](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220707112747526.png)



# includes()

![image-20220707112855739](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220707112855739.png)



# 模板字符串

![image-20220707113005024](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220707113005024.png)

![image-20220707113022707](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220707113022707.png)

![image-20220707113341879](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220707113341879.png)



# startsWith()和endsWith()

![image-20220707113511512](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220707113511512.png)



# repeat()

![image-20220707113536210](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220707113536210.png)



# Set数据结构

![image-20220707113654875](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220707113654875.png)

## 利用set完成数组去重

![image-20220707113841632](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220707113841632.png)



## Set方法

![image-20220707113917295](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220707113917295.png)

## 遍历Set

![image-20220707113953089](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220707113953089.png)