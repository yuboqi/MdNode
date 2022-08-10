# JS文件(端口文件)server.js



```js
//1.引用express模块
const express = require('express');

//2.创建express实例
const app = express();

//3.创建路由实例
app.all('/server',(request,response)=>{
    //设置响应头，设置允许跨域
    response.setHeader('Access-Control-Allow-Origin','*');
    //设置响应体
    response.send("HELLO AJAX SERVER");
})

app.all('/json-server',(request,response)=>{
    //设置响应头，设置允许跨域
    response.setHeader('Access-Control-Allow-Origin','*');
    //响应数据
    const data = {
        name:'张三'
    };
    JSON.stringify(data);
    //设置响应体
    response.send(data);
})
//IE缓存
app.all('/ie',(request,response)=>{
    //设置响应头，设置允许跨域
    response.setHeader('Access-Control-Allow-Origin','*');
    //设置响应体
    response.send("HELLO IE2");
})
//延时响应
app.all('/delay',(request,response)=>{
    //设置响应头，设置允许跨域
    response.setHeader('Access-Control-Allow-Origin','*');
    setTimeout(()=>{
        response.send("延时响应");
    },4000);
    //设置响应体
  
})

//4.启动服务器
app.listen(8000,()=>{
    console.log("8000端口服务器启动成功");
})
```





# GET请求和POST请求

## GET请求

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HELLO</title>
    <style>
        #result{
            width:200px;
            height: 100px;
            border: 1px solid red;
        }
    </style>
</head>
<body>
    <button>点击发送请求</button>
    <div id="result">

    </div>
    <script>
        //获取button元素
        const btn = document.getElementsByTagName('button')[0];
        const result = document.getElementById('result');
        //给button绑定点击事件
        btn.onclick = function(){
            //1.创建XMLHttpRequest对象
            const xhr = new XMLHttpRequest();
            //2.设置请求方式和请求地址
            xhr.open('GET','http://127.0.0.1:8000/server');
            //3.发送
            xhr.send();
            //4.事件绑定 处理服务端返回的结果
            //readystate 是 xhr对象中的属性，表示状态 0 1 2 3 4 (4是已经完成的状态)
            xhr.onreadystatechange = function(){
                //如果readystate等于4，表示已经完成了
                if(xhr.readyState ==4){
                    //判断状态是否为200，如果是200，表示请求成功
                    if(xhr.status >=200&& xhr.status<300){
                        //处理结果 行 头 空行 体
                        //1.响应行
                        // console.log(xhr.status);//状态码
                        // console.log(xhr.statusText);//状态字符串
                        // console.log(xhr.getAllResponseHeaders);//响应头
                        // console.log(xhr.response);//响应体

                        //设置result的文本
                        result.innerHTML = xhr.responseText;

                    }else{

                    }
                }
            }
        }
    </script>
</body>
</html>
```



## POST请求

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #result{
            width:200px;
            height: 100px;
            border: 1px solid red;
        }
    </style>
</head>
<body>
        <div id="result"></div>
        <script>
            //获取元素对象
            const result = document.getElementById('result');
            //给result绑定点击事件
            result.addEventListener("mouseover",function(){
                //创建对象
                const xhr = new XMLHttpRequest();
                //初始化 设置类型与URL
                xhr.open('POST','http://127.0.0.1:8000/server');
                //设置请求头
                xhr.setRequestHeader('Content-Type','application/x-www-form-urlencoded');
                //发送
                xhr.send();
                //事件绑定
                xhr.onreadystatechange = function(){
                    if(xhr.readyState ==4){
                        if(xhr.status >=200 && xhr.status<300){
                            result.innerHTML = xhr.response;
                    }

                }
            }
        });
        </script>
</body>
</html>
```



# JSON转化

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        #result{
            width:200px;
            height: 100px;
            border: 1px solid red;
        }
    </style>
</head>
<body>
    <div id="result"></div>
    <script>
        const result = document.getElementById('result');
        window.onkeydown = function(){
            const xhr = new XMLHttpRequest();
            //①设置响应体的类型为json
            xhr.responseType = 'json';
            xhr.open('GET','http://127.0.0.1:8000/json-server');
            xhr.send();
            xhr.onreadystatechange = function(){
                if(xhr.readyState ==4){
                    if(xhr.status >=200 && xhr.status<300){
                    //    console.log(xhr.response);
                    //    result.innerHTML = xhr.response;

                    //手动解析JSON
                    // let data =JSON.parse(xhr.response);
                    // console.log(data);
                    // result.innerHTML = data.name;

                    //②自动解析JSON
                    result.innerHTML = xhr.response.name;
                    }
                }
            }
        }
    </script>
</body>
</html>
```



# 防止IE缓存

#### 主要代码：xhr.open('GET','http://127.0.0.1:8000/ie?t=' +Date.now());

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HELLO</title>
    <style>
        #result{
            width:200px;
            height: 100px;
            border: 1px solid red;
        }
    </style>
</head>
<body>
    <button>点击发送请求</button>
    <div id="result">

    </div>
    <script>
        //获取button元素
        const btn = document.getElementsByTagName('button')[0];
        const result = document.getElementById('result');
        //给button绑定点击事件
        btn.onclick = function(){
            //1.创建XMLHttpRequest对象
            const xhr = new XMLHttpRequest();
            //2.设置请求方式和请求地址   防止IE缓存
            xhr.open('GET','http://127.0.0.1:8000/ie?t=' +Date.now());
            //3.发送
            xhr.send();
            //4.事件绑定 处理服务端返回的结果
            //readystate 是 xhr对象中的属性，表示状态 0 1 2 3 4 (4是已经完成的状态)
            xhr.onreadystatechange = function(){
                //如果readystate等于4，表示已经完成了
                if(xhr.readyState ==4){
                    //判断状态是否为200，如果是200，表示请求成功
                    if(xhr.status >=200&& xhr.status<300){
                        //处理结果 行 头 空行 体
                        //1.响应行
                        // console.log(xhr.status);//状态码
                        // console.log(xhr.statusText);//状态字符串
                        // console.log(xhr.getAllResponseHeaders);//响应头
                        // console.log(xhr.response);//响应体

                        //设置result的文本
                        result.innerHTML = xhr.response;

                    }else{

                    }
                }
            }
        }
    </script>
</body>
</html>
```

# 

# 网络超时和异常

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>HELLO</title>
    <style>
        #result{
            width:200px;
            height: 100px;
            border: 1px solid red;
        }
    </style>
</head>
<body>
    <button>点击发送请求</button>
    <div id="result">

    </div>
    <script>
        //获取button元素
        const btn = document.getElementsByTagName('button')[0];
        const result = document.getElementById('result');
        //给button绑定点击事件
        btn.onclick = function(){
            //1.创建XMLHttpRequest对象
            const xhr = new XMLHttpRequest();
            //超时设置
            xhr.timeout = 2000;
            //超时回调
            xhr.ontimeout = function(){
                alert("请求超时");
            };

            //网络异常回调
            xhr.onerror = function(){
                alert("网络异常");
            }
            //2.设置请求方式和请求地址   防止IE缓存
            xhr.open('GET','http://127.0.0.1:8000/delay');
            //3.发送
            xhr.send();
            //4.事件绑定 处理服务端返回的结果
            //readystate 是 xhr对象中的属性，表示状态 0 1 2 3 4 (4是已经完成的状态)
            xhr.onreadystatechange = function(){
                //如果readystate等于4，表示已经完成了
                if(xhr.readyState ==4){
                    //判断状态是否为200，如果是200，表示请求成功
                    if(xhr.status >=200&& xhr.status<300){
                        //处理结果 行 头 空行 体
                        //1.响应行
                        // console.log(xhr.status);//状态码
                        // console.log(xhr.statusText);//状态字符串
                        // console.log(xhr.getAllResponseHeaders);//响应头
                        // console.log(xhr.response);//响应体

                        //设置result的文本
                        result.innerHTML = xhr.response;

                    }else{

                    }
                }
            }
        }
    </script>
</body>
</html>
```



# 请求取消

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <button>点击发送</button>
    <button>点击取消</button>

    <script>
        //获取元素对象
        const btns = document.getElementsByTagName('button');
        let x =null;
        btns[0].onclick = function(){
            x = new XMLHttpRequest();
            x.open('GET','http://localhost:8000/delay');
            x.send();

        }

        //abort
        btns[1].onclick = function(){
            x.abort();
        }
    </script>
</body>
</html>
```





# 重复请求问题

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>重复请求问题</title>
</head>
<body>
    <button>点击发送</button>

    <script>
        //获取元素对象
        const btns = document.getElementsByTagName('button');
        let x =null;

        //标识变量
        let isSending =false; //是否正在发送请求
        btns[0].onclick = function(){
            //判断标识变量
            if(isSending){
                x.abort();
            }//如果正在发送，则取消该请求，创建一个新请求
            x = new XMLHttpRequest();
            isSending = true;
            x.open('GET','http://localhost:8000/delay');
            x.send();
            x.onreadystatechange = function(){
                if(x.readyState ==4){
                    //修改表示变量
                    isSending = false;
                }
            }
        }

        //abort
        btns[1].onclick = function(){
            x.abort();
        }
    </script>
</body>
</html>
```



# 使用fetch函数发送AJAX请求

![image-20220705202001214](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220705202001214.png)



# 使用JQuery发送AJAX请求

![image-20220705202140739](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220705202140739.png)

![image-20220705202210875](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220705202210875.png)



# jQuery通用方法发送AJAX请求

![image-20220705202306342](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220705202306342.png)

![image-20220705202350550](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220705202350550.png)



# 如何解决跨域

## ①JSONP

​			

![image-20220705204347503](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220705204347503.png)

### 实例：检测用户名是否存在

![image-20220705204858858](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220705204858858.png)



## jQuery发送JOSNP

![image-20220705205248048](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220705205248048.png)

![image-20220705205316694](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220705205316694.png)



## ②CORS

![image-20220705205801622](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220705205801622.png)
