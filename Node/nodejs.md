#  :exclamation:注意：导包须知

> 导入模块若用import方法需要在package.json中加入"type":module才行，不然只能用require
>
> 本笔记大部分使用 import方法和  export方法
>
> 若想用node基本方法可不加type使用 require和module.exports方法

## 一、什么是Node.js

`Node.js是基于ChromeV8引擎的JavaScript运行环境`

注意:浏览器是javascript的前端运行环境,Node.js是javascript的后端运行环境Node.js中无法调用DOM和BOM等浏览器内置API。



## 二、fs文件系统模块

### ①fs读取文件内容readFile()

```js
//导入fs模块
const fs = require('fs');
//fs.readFile(path[,options],callback)
//参数1：path 必选参数，表示文件路径
//参数2：options 可选参数  表示编码格式
//参数3：callback 必选参数 表示回调函数

fs.readFile('../txt/01.txt','utf-8',function(err,dataStr){
    //三个参数中编码参数为选填函数
    //读取成功则err返回null，读取失败err返回失败类型，dataStr返回undefined
    console.log(err)
    console.log('-------------')
    console.log(dataStr)
        
})
```



### ②判断文件是否读取成功

```js
const fs = require('fs')
fs.readFile('z.txt','utf-8',function(err,result){
    if(err){
        return console.log('读取失败',+err.message)
    }
    console.log('读取成功',result)
})
```



### ③向指定文件中写入内容writeFile()

> 该方法会覆盖文件原有的内容

```
const fs = require('fs')
//参数1：文件路径
//参数2：文件内容
//参数3：回调函数
//写入会覆盖原有内容
fs.writeFileSync('z.txt','hello world',function(err,result){
    if(err){
        console.log(err.messgae)
    }
    console.log(result);
})
```



### ④:star:路径问题

因为node命令执行的文件如果是使用的`相对路径`会在node当前目录下的路径和执行文件的命令进行拼接

解决：执行的文件使用绝对路径（但是代码的可移植性差，不易维护）

```js
const fs = require('fs')
// 路径双斜杠是转义
fs.writeFileSync('D:\\桌面\\实训笔记\\NodeJS\\02-文件系统模块\\txt\\z.txt','hello world1',function(err,result){
    if(err){
        console.log(err.messgae)
    }
    console.log('成功'+result);
})
```

完美方案：(__dirname  表示的是当前文件所处的目录)

![image-20220803093302188](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220803093302188.png)

```js
fs.writeFileSync(__dirname+'/txt/z.txt','hello world2',function(err,result){
    if(err){
        console.log(err.messgae)
    }
    console.log('成功'+result);
})
```



## fs模块案例

![image-20220802210059327](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220802210059327.png)

![image-20220802210107663](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220802210107663.png)

目标：将上图的格式转换为下图新格式写入到新文件中

```js
const fs = require('fs')
fs.readFile('txt/成绩.txt', 'utf8', function (err, result) {
    if (err) {
        console.log(err.message);
    } else {
        //先以空格分割字符串为数组
        const arrOld = result.split(' ');
        //创建新数组来接收遍历后的数据
        const arrNew = []
        //遍历数组，将=换成：再push到新数组中
        arrOld.forEach(item => {
            arrNew.push(item.replace('=', ':'))
        })
        //将新数组转换为字符串形式join方法会把数组转化为字符串，并设置元素之间的分隔符
        const newStr = arrNew.join('\n');
        //将字符串写入目标文件
        fs.writeFile('txt/成绩-ok.txt', newStr, function (err, result) {
            if (err) {
                console.log(err.message);
            } else {
                console.log('写入成功');
            }
        })
    }
})
```



## 三、path路径模块

path模块是Node.js官方提供用来**处理路径**的模块,使用前需要用require('path')来引入。



### ①路径拼接path.join()

```js
const path = require('path')
//注意  ../会抵消前面的路径  所以结果为 \a\b\d\e
const pathStr = path.join('/a','/b/c','../','./d','e')
console.log(pathStr);
```

> ​	注意：之后的路径拼接不在使用__dirname+的格式，可以用 path.join( _dirname,str)的形式拼接路径

```js
const path = require('path')
const fs = require('fs')
fs.readFile(path.join(__dirname,'/txt/z.txt'),'utf8',function(err,result){
    if(err){
        console.log(err.message)
    }else{
        console.log(result)
    }
})
```



### ②获取路径中的文件名path.basename()方法

```js
const path = require('path')

//定义文件存放路径
const fpath = '/a/b/c/index.html'

const fullName = path.basename(fpath)
console.log(fullName);//输出 index.html

const fileName = path.basename(fpath,'.html')
console.log(fileName);//输出 index
```



### ③获取文件扩展名path.extname()

```js
const path = require ('path')
//定义文件存放路径
const fpath = '/a/b/c/index.html'

const name = path.extname(fpath)
console.log(name) //输出  .html
```



## 四、http模块

http模块是Node.js官方提供的，用来**创建Web服务器**的模块，通过http.createServe()方法，就能把电脑变成Web服务器，要使用该方法，需要首先导入http模块

```js
const http = require('http')
```



### ①创建基本的web服务器

步骤：①引入http模块②http.createServe创建服务器实例③绑定request事件 ④启动

```js
//导入http模块
const http = require('http')
//创建服务器实例
const server = http.createServer()
//绑定request事件，监听请求
server.on('request',function(req,res){
    console.log('访问了服务器');//只有访问了才会打印，先执行下面的启动
})
//启动服务器
server.listen(8080,function(){
    console.log('服务器启动成功 http://127.0.0.1:8080');
})
```

#### 1.req请求对象

在监听事件的回调函数中，req可以返回请求对象的相关信息

```js
const http = require('http')
const server = http.createServer()
server.on('request',(req,res)=>{
    console.log('访问了服务器');
    //req对象url属性
    console.log(req.url); //url地址
    //req对象请求方式method属性
    console.log(req.method); //get  post等请求
    //req对象请求头headers属性
    console.log(req.headers);//请求头信息
})
server.listen(8080,function(){
    console.log('服务器启动成功 http://localhost:8080');
})
```

#### 2.res响应对象

在服务器的request事件处理函数中，如果想`访问与服务器相关的数据或者属性`，可以使用下面的方法

```js
const http = require('http')
const server = http.createServer()
server.on('request',(req,res)=>{
    console.log('访问了服务器');
    const str = `You request url:${req.url},and request method is:${req.method}`
    //将str写入到res中，返回数据给客户端
    res.end(str)
})
server.listen(8080,function(){
    console.log('服务器启动成功 http://localhost:8080');
})
```

#### 3.:star:防止res中文乱码问题

> ​	解决：手动设置内容编码格式

```
const http = require('http')
const server = http.createServer()
server.on('request',(req,res)=>{
    console.log('访问了服务器');
    const str='你访问了服务器'
    //设置请求头，设置编码格式
    res.setHeader('Content-Type','text/plain;charset=utf-8')
    res.end(str)
})
server.listen(8080,function(){
    console.log('服务器启动成功 http://localhost:8080');
})
```



### ②根据不同的url响应返回不同的html内容

```js
const http = require('http')
const server = http.createServer()
server.on('request',(req,res)=>{
    console.log('访问了服务器');
    res.setHeader('Content-Type','text/html; charset=utf-8')
    const str = `<h1>你访问了服务器,url:${req.url} method:${req.method}</h1>`
    //只要请求url不为 /index 或者 / 就会被报错404
    if(req.url=='/index'||req.url=='/'){
        res.end(str)
    }else{
        res.end('404')
    }
})
server.listen(8080,()=>{
    console.log('服务器启动成功 http://localhost:8080');
})
```



### ③服务器时钟案例

![image-20220803140714140](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220803140714140.png)

```js
const http = require('http')
const fs = require('fs')
const path = require('path')

const server = http.createServer()

server.on('request',(req,res)=>{
    //拿到请求的url映射为文件路径
    const fpath = path.join(__dirname,req.url)
    //读取文件内容响应给客户端
    fs.readFile(fpath,(err,data)=>{
        if(err){
            res.end('404 Not Found')
        }else{
            res.end(data)
        }
    })
})

server.listen(8080,()=>{
    console.log('服务器启动成功 http://localhost:8080');
})
```

**会直接把js和css返回出来是因为在html中用link引入了两个文件**

> 问题：①第一次进页面会报404错误 ②每次都要输入/clock/index.html太麻烦

```js
//解决
    let fpath = ''//让fpath为空方便修改
    if(req.url ==='/'){
        fpath = path.join(__dirname,'/clock/index.html')//如果用户输入为/或者刚进页面，会通过方法把fpath赋值为首页
    }else{
        fpath = path.join(__dirname,'/clock',req.url)//如果用户手动修改url地址，则只需要自动补全/clock部分即可
    }
```



## 五、模块化

模块分为:内置模块  用户自定义模块  第三方模块

### ①加载模块(require方法加载模块时，会执行模块中的代码)

```js
//1.加载内置的fs模块
const http = require('http')

//2.加载自定义的模块   自定义模块时 .js后缀可以省略 
const z = require('./z.js')

//3.加载第三方模块
const moment = require('moment')
```



### ②Node.js中的模块作用域

和函数作用域类似，在**自定义模块中**定义的变量方法等成员，只能在当前模块内被访问，这种模块级别的访问限制，叫做模块作用域

`好处：防止全局变量被污染`

### ③向外共享模块作用域成员

#### 1.module对象

每一个自定义模块中都有一个module对象，它存储了和当前模块有关的信息

![image-20220803144240425](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220803144240425.png)

#### 2.module.exports对象

在自定义模块中，可以使用module.exports来将模块内的成员共享出去

```js
//自定义模块.js
module.exports.name ='zhangsan'
const age = 20
module.exports.sayHello=function() {
    console.log('hello')
}
module.exports.age = age//方法二

//引入自定义模块.js
const m = require('./02-module.exports使用.js')

console.log(m)
```

![image-20220803145222600](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220803145222600.png)

#### 3.注意点

使用require方法导入模块时，导入的结果，永远以**module.exports指向的对象为准**

#### 4.exports对象

为了简化module.exports而出，默认情况下exports和module.exports指向同一个对象

```js
const username = 'zsw'
exports.username = username

exports.age = 18

exports.sayHello = function(){
    console.log('hello')
}
```

#### 5.:star:exports和 module.exports使用误区

> 时刻记住，require模块时，得到的永远是module.exports指向的对象

```js
exports.usename = 'zsw'
module.exports = {
    gender:'男',
    age :'22'
}

//导入后的module结果不会有usname，因为module.exports创建了新对象，然后改变了module.exports的指向，不在指向exports.username创建的对象中
```

![image-20220803152843483](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220803152843483.png)



### ④Node.js中的模块化规范

Node.js遵循了CommonJS模块化规范，CommomJS规定了**模块的特性**和**各模块之间如何相互依赖**

> CommonJS规定：
>
> ①每个模块内部，`moudle变量`代表当前模块
>
> ②module变量是一个对象，它的exports属性(moudle.exports)是对外的接口
>
> ③加载某个模块，其实是加载该模块的module.exports属性.require方法加载模块



## 六、npm与包

### ①包

Node.js中的第三方模块叫包

> 包和内置模块的关系：包是基于内置模块封装出来的

### :star:②npm

当你使用import来引入包时类似下面的情况你会出现响应的报错

```js
import moment from 'moment';
const dt = moment().format('YYYY-MM-DD HH:mm:ss');
console.log(dt);
```

![image-20220803164306026](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220803164306026.png)

解决：在package.json文件中加入 "type": "module"即可，因为import是ES6引入的方法

### ③包管理配置文件

#### 1.package.json

在该配置文件中，记录了整个项目安装了哪些包，一般项目的npm包占的内存比较大，所以在上传到github时通常用.gitignore中忽略上传node_modules文件夹，成员通过查看package.json中查看项目所需要的包

> 可以用npm init -y来创建package.json 文件

#### 2.dependencies节点

在package.json文件中，这个节点专门记录使用npm install安装过的包

![image-20220803165452210](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220803165452210.png)

#### :star:3.拿到Github项目后(没有node_modules项目)

当你拿到一个剔除了node_modules的项目后，需要把包先下载到项目才能跑起来

> 需要执行 npm install 命令

#### 4.卸载包

> npm uninstall 包名

#### 5.devDependencies节点

如果某些包只在项目开发阶段会用到，上线后不会用到，建议放在该节点中。

> npm install 包名 -D 

### :star:④解决下包速度慢问题

#### 1.淘宝镜像服务器：

```js
npm config get registry//查看当前镜像源
npm config set registry=https://registry.npm.taobao.org/  //切换到淘宝镜像源

```

#### 2.nrm

```js
npm i nrm -g //下载nrm工具
nrm ls //查看所有可用镜像源
nrm use taobao //淘宝镜像源
```



## :star:七、模块加载的机制

 `模块在第一次加载后会被缓存`，意味着多次调用require不会导致代码被多次执行。

注意：不论是内置模块、用户自定义模块、还是第三方模块，他们都会优先从缓存中加载，从而提高模块的加载效率

### ①优先级

> Node自带的内置模块优先级大于第三方模块，优先级最高

### ②自定义模块加载机制

> 自定义模块加载时需要 ./或者 ../来标识

### ③第三方模块加载机制

> 如果没有找到对应的第三方模块，则移动到上一层的目录，直到找到为止





## :star:八、Express

官方概念:Express是基于Node.js平台，快速，开放，极简的Web开发框架

理解：express的作用和Node.js内置的http模块类似，**专门用来创建Web服务器的**

本质:`就是一个npm上面的第三方包`

```js
//导入express
import express  from 'express';

//创建服务器
const app = express()

//启动服务器
app.listen(8080,()=>{
    console.log('server is running at port 8080')
})
```

### ①GET和POST请求

```js
//导入express
import express  from 'express';

//创建服务器
const app = express()

app.get('/user',function(req,res){
    res.send({
        name:'张三',
        age:18,
        gender:'男'
    })
})

app.post('/user',function(req,res){
    res.send('Posh请求')
})

//启动服务器
app.listen(8080,()=>{
    console.log('server is running at http://127.0.0.1:8080')
})
```

### :star:②获取url参数

> req.query

```js
import express from "express";

const app = express();

app.get('/user',(req,res)=>{
//用req.query获取url参数
//默认情况下req.query为空对象
    console.log(req.query);
    res.send('get请求')
})

app.post('/user',(req,res)=>{
    console.log(req.query);
    res.send('post请求')
})

app.listen(8080,()=>{
    console.log('server is running at http://127.0.0.1:8080')
})
```

![image-20220804102547127](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220804102547127.png)

![image-20220804102554089](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220804102554089.png)

>req.params
>
>在:name后面加上?表示该参数可为空

```js
app.get('/user/:id/:name?',(req,res)=>{
    console.log(req.params);
    res.send('get请求')
})
```

![image-20220804103255940](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220804103255940.png)

![image-20220804103305807](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220804103305807.png)



### ③托管静态资源

#### 1.无前缀托管

![image-20220804103936538](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220804103936538.png)

```js
import express from "express";

const app = express()

//将平级下的clock目录里面的资源对外开放
app.use(express.static('./clock'))

app.listen(8080,()=>{
    console.log('服务器启动成功 http://127.0.0.1:8080')
})
```

>如果需要托管多个静态资源目录，只需要多次调用express.static()函数

`访问静态资源文件时，express.static()函数会根据目录添加顺序查找所需的文件，即如果两次的函数调用都有index.html文件，则用户查找index.html会根据函数调用的顺序显示第一个`

#### 2.挂载路径访问前缀

```js
app.use('/abc',express.static('./public'))

//public 目录里面有  index.html
//大部分情况下前缀名和目录名一致
```

这样后可以通过带有 /public 前缀的地址来访问public目录中的文件

例如: http://127.0.0.1/abc/index.html



### :exclamation:④nodemon使用

> 作用：每次写完.js文件都要重启node服务器，nodemon会自动重启

#### 1.安装

```js
npm install -g nodemon
```

#### 2.使用

```js
//在终端不使用 node+文件名  直接 nodemon +文件名启动
```

![image-20220804113257117](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220804113257117.png)



## :exclamation:九、Express路由

概念：在express中，**路由指的是客户端的请求和服务器处理函数的映射关系**

组成：请求类型   请求的URL地址  处理函数

```js
app.METHOD(PATH,HANDLER)
//METHOD:请求类型  post  get等
//PATH:请求的URL地址
//HANDLER:处理函数
```

路由匹配的注意点:																								    ①按照定义的先后顺序进行匹配																				      ②请求类型和URL同时匹配成功，才会调用相应的处理函数

最简单用法：把路由挂在到app上(用的少，麻烦不好处理)

```js
import express from 'express'
//创建web服务器
const app = express()

//路由挂载
app.get('/',(req,res)=>{res.send('hello world')})

app.post('/',(req,res)=>{res.send('post')})

//启动web服务器
app.listen(8080,()=>{console.log('服务器启动成功 http://127.0.0.1:8080');})
```



### ①模块化路由

为了方便对路由进行模块化的管理，不建议直接将路由挂在到app上，而是推荐将路由抽离为单独的模块

```js
import express from 'express'
//创建路由
const router = express.Router()

router.get('/',(req,res)=>{
    res.send('hello world GET')
})

router.post('/',(req,res)=>{
    res.send('hello world POST')
})
export default router;//对外暴露
_____________________________________________________________________
import express from 'express'
//引入路由组件
import router from './02-router.js'
const app = express()
//注册路由组件
app.use(router)

app.listen(8080,()=>{
    console.log('服务器启动成功 http://127.0.0.1:8080');
})
```



### ②为路由模块添加前缀

在路由注册时在注册路由前添加即可

```js
app.ues('/api',router)
```



### ③中间件

特指业务流程的中间处理环节																					

> 作用:对请求进行预处理

![image-20220804144433469](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220804144433469.png)



#### 1.中间件格式

Express的中间件，本质上就是一个function处理函数，格式如下

![image-20220804144614383](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220804144614383.png)

`注意：中间件函数的形参列表中，必须包含next参数，而路由的处理函数中没有next参数`

#### 2.next函数的作用

next函数时实现多个中间件连续调用的关键，它表示把流转关系转交给下一个中间件或者路由

![image-20220804144852249](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220804144852249.png)

#### 3.全局生效的中间件

通过调用app.use(中间件函数)，即可定义一个全局生效的中间件

```js
import express from 'express'
const app = express()
//定义一个中间件
const vm = (req,res,next)=>{
    console.log('中间件')
    next()
}
//全局中间件
app.use(vm)

//简化形式：
//app.ues =( (req,res,next)=>{
//    console.log('中间件')
//    next()
//})

app.listen(8080,()=>{
    console.log('服务器启动成功 http://127.0.0.1:8080')
})
```

#### 4.中间件的作用

![image-20220804152528060](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220804152528060.png)

```js

import express from 'express'
const app = express()

app.use((req,res,next)=>{
    const time = Date.now()
    req.startTime = time
    console.log('中间件')
    next()
}
)
app.get('/',(req,res)=>{
    console.log('现在是'+req.startTime)
})

app.listen(8080,()=>{
    console.log('服务器启动成功 http://127.0.0.1:8080')
})
```

#### 5.定义多个中间件

通过app.use()连续定义多个中间件



###  ④局部生效的中间件

**在.get中的URL和处理函数直接写中间件函数，可以让中间件函数局部生效**

**若有多个局部中间件用[ ]或者 ，分割**

```js

import express from 'express'
const app = express()

const vm = (req,res,next)=>{
    console.log('局部中间件')
    next()
}
const vm2 = (req,res,next)=>{
    console.log('局部中间件2')
    next()
}
//局部生效中间件  或者[vm,vm2]
app.get('/',vm,vm2,(req,res)=>{
    console.log('现在是'+Date.now())
    res.send('hello world')
})

app.get('/home',(req,res)=>{
    console.log('现在是'+Date.now())
    res.send('home')
})

app.listen(8080,()=>{
    console.log('服务器启动成功 http://127.0.0.1:8080')
})
```

### ⑤中间件的5个注意事项

> ①一定要在路由之前注册中间件
>
> ②客户端的请求可以连续调用多个中间件处理
>
> ③中间件执行完后不要忘记调用next()
>
> ④调用完next()后不要写额外的代码
>
> ⑤连续调用多个中间件的时候，共享req和res对象



### ⑥中间件的分类

#### 1.应用级别的中间件

概念：绑定到app实例上的中间件 app.use()  app.get() app.post()等

```js
app.get('/',vm,vm2,(req,res)=>{
    console.log('现在是'+Date.now())
    res.send('hello world')
})

app.use((req,res,next)=>{
    const time = Date.now()
    req.startTime = time
    console.log('中间件')
    next()
}
)
```



#### 2.路由级别的中间件

绑定到express.Router()实例上的中间件

```js
const router = express.Router()
const vm = (req,res,next)=>{
    console.log('局部中间件')
    next()
}
router.get('/',vm,(req,res)=>{
    res.send('hello world GET')
})

```



#### 3.错误级别的中间件

专门捕获项目中发生异常错误，防止项目崩溃，只有发生错误了才会执行

> 可以直接全局定义一个错误中间件，这样程序只要发生错误就不会崩溃
>
> :star:一定要注册在所有路由之后

格式：4个形参  (err,req,res,next)

```js
app.use((err,req,res,next)=>{
	console.log('发生了错误'+err,nessage)
	res.send('Error'+err.message)
})
_____________________________________________________________________

import express from 'express'
const app = express()

app.get('/',(req,res)=>{
   throw new Error('error')//人为创造错误
   res.send('hello world')
})

//下面的中间件只有发生错误了才会执行，注册在所有路由之后
app.use((err,req,res,next)=>{
    console.log("发生了错误"+err.message);
    res.send('错误')//错误后返回客户端信息
})

app.listen(8080,()=>{
    console.log('服务器启用： http://127.0.0.1:8080');
})
```



#### 4.Express内置的中间件

在Express 4.16.0版本开始，内置了3个常用的中间件

①express.static 快速托管静态资源的内置中间件

②express.json 解析JSON格式的请求体数据(兼容性:4.16.0+版本可用)

```js
app.use(express.json())
app.use(express.urlencoded())
```

```js
//启动服务器后在postman中发送请求 带有JSON格式数据
import express from 'express';
const app = express();
app.use(express.json())
app.post('/user',(req,res)=>{
    //如果不使用express.json()中间件，则req.body为undefined
    console.log(req.body);
    res.send('ok')
})
app.listen(8080,()=>{
    console.log('服务器启动成功 http://127.0.0.1:8080')
})
```

![image-20220804164042853](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220804164042853.png)

![image-20220804164053894](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220804164053894.png)

③express.urlencoded 解析URL-encoded格式的请求体数据(4.16.0+版本可用)

```js
//也是在req.body中拿到数据
//启动服务器后在postman中发送请求 带有urlencoded格式数据
import express from 'express';
const app = express();
app.use(express.urlencoded({ extends:false}))
app.post('/user',(req,res)=>{
    //如果不使用express.urlencoded()中间件，则req.body为undefined
    console.log(req.body);
    res.send('ok')
})
app.listen(8080,()=>{
    console.log('服务器启动成功 http://127.0.0.1:8080')
})
```

>要求为 express.urlencoded({extends:false})

#### 5.第三方中间件

可以按需下载并配置第三方中间件

①需要运行 npm install body-parser安装中间件

②导入中间件require()或者import

③使用app.use()注册中间件



## 十、使用Express写接口

> 在写posh接口时，通过req.body拿到相应的数据，而且要使用内置的中间件把相关的格式转化才能拿到数据
>
> router.use(express.json())   router.use(express.urlencoded({extends:false}))										app.use(express.json())   		app.use(express.urlencoded({extends:false}))
>
> 

```js
import express from 'express'

const router = express.Router()

router.get('/get',(req,res)=>{
    const query = req.query
    res.send({
        status:0,
        msg:'GET请求成功',
        data:query
    })
})

//router.use(express.urlencoded({extended:false}))
router.use(express.json())
router.post('/post',(req,res)=>{
    const body = req.body
    res.send({
        status:0,
        msg:'POST请求成功',
        data:body
    })
})

export default router 


_____________________________________________________________________

import express  from 'express'
import apiRouter from './02-apiRouter.js'

const app = express()
app.use('/api',apiRouter)

app.listen(8080,()=>{
console.log('服务器创建成功 http://127.0.0.1:8080')
})
```

> 上面的方法存在跨域问题



## :exclamation:十一、解决跨域问题

解决跨域的问题有两种：																							①CORS(主流解决方法   推荐使用) 																	②JSONP(有缺陷，只能解决GET请求)

### ①使用CORS中间件解决跨域问题

```js
//首先得安装再导入
import cors from 'cors'
app.use(cors())
```



### :star:②CORS响应头 Access-Conrol-Allow-Origin

```js
//之润许来自 http://itcast.cn的请求
res.setHeader('Access-Contol-Allow-Oringin','http://itcast.cn')
//允许任何域的请求
res.setHeader('Access-Contol-Allow-Oringin','*')
```

> 直接post get相关请求中添加这个响应头可解决跨域问题

```js
router.get('/get',(req,res)=>{
    const query = req.query
    res.setHeader('Access-Control-Allow-Origin','*')//用了CORS之后，这个就不用了
    res.send({
        status:0,
        msg:'GET请求成功',
        data:query
    })
})
```

**该方法没有下载引入CORS包来使用**



### ③CORS响应头 Access-Conrol-Allow-Headers

> 默认情况下，CORS仅支持客户端向服务器发送规定的9个请求头
>
> 如果要发送额外的请求头信息，则需要通过Access-Conrol-Allow-Headers对额外的请求头进行声明

```js
res.setHeader(' Access-Conrol-Allow-Headers','Content-Type,X-Custom-Header')
```



### ④CORS响应头 Access-Conrol-Allow-Methods

```js
//允许POST 和GET请求
res.setHeader(' Access-Conrol-Allow-Methods','POST,GET')
//允许全部请求方式
res.setHeader(' Access-Conrol-Allow-Methods','*')
```



### ⑤简单请求和预检请求

#### 1.简单请求

①请求方式：GET POST HEAD三者之一

②HTTP头部信息不超过一些基本字段

#### 2.预检请求

①请求方式为GET POST HEAD之外的请求类型

②请求头中包含了自定义头部字段

③向服务器发送了application/json格式的数据

>区别：
>
>简单请求的特点：客户端与服务器之间只发生一次请求
>
>预检请求的特点：发送两次请求，OPTION预检请求成功后才会发送真正的请求



### ⑥JSONP接口

![image-20220804205811987](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220804205811987.png)

![image-20220804205848712](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220804205848712.png)

<img src="C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220804210115340.png" alt="image-20220804210115340" style="zoom:200%;" />



## 十二、Express连接数据库

> ①npm i mysql																															②import mysql
>
> ③mysql.createPool()添加连接信息

### ①判断是否连接成功

```js

import mysql from 'mysql'
const db = mysql.createPool({
    host:'localhost',
    user:'root',
    password:'root',
    database:'my_db_01'
})
//执行select语句，结果为数组
db.query('select * from student',(err,resluts)=>{
    if(err)
    return console.log(err.message)
    console.log(resluts)
})
```



### ②插入/更新/删除

```js

const stu ={name:'张三',id:8, sex:'男'} 
const sqlstr = 'insert into student(name,id,sex) values(?,?,?)'
db.query(sqlstr,[stu.name,stu.id,stu.sex],(err,results)=>{
    if(err)
    return console.log(err.message);
    //判断插入数据是否成功
    if(results.affectedRows ===1){
        console.log('插入数成功')
    }
})
————————————————————————————————————————————————————————————————————
//快速插入方法
const stu ={name:'ybq',id:6, sex:'男'} 
//插入语句用set？即可
const sqlstr = 'insert into student set ?'
const sqlstr2 = 'update  student set ? where id=?'
const sqlstr3 = 'delete from  student  where id=?'
db.query(sqlstr,stu,(err,results)=>{
    if(err)
    return console.log(err.message);
    //判断插入数据是否成功
    if(results.affectedRows ===1){
        console.log('插入数成功')
    }
})
```

> mysql 的id具有唯一性，如果插入的id是自增长的而且不是人为插入的id那么id即使被删除还是存在，新加入的数据id不会占用被删除后的id



`执行插入、更新语句和删除后，返回的数据都是对象，所以可以用 results.affectedRows来判断是否插入、更新或删除成功`

> 因为删除是直接删除的，有可能因为操作失误导致，可以使用标记删除法

### ③标记删除法

![image-20220805111458251](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220805111458251.png)

![image-20220805111810527](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220805111810527.png)

```js

const sqlstr = 'update student set status=? where id=?'
db.query(sqlstr,[1,1],(err,results)=>{
    if(err) console.log(err.message);
    if(results.affectedRows ===1){
        console.log('更新成功');
    }
})
```



## :star:十三、前后端的身份认证

两种开发模式:①服务端渲染模式(推荐Session认证)   ②前后端分离模式(JWT认证)

### ①Session认证机制

#### 1.http协议的无状态性

指的是客户端每次HTTP请求都是独立的，连续多个请求之间没有直接的关系，服务器不会主动保留每次HTTP请求的状态

#### 2.突破HTTP无状态的限制

![image-20220805141218374](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220805141218374.png)

`现实生活中的会员卡身份认证的方式，叫做Cookie`

#### 3.什么是Cookie

Cookie是存储在用户浏览器中的一段不超过4kb的字符串。它由Name和Value和其他几个用于控制Cookie有效期、安全性、使用范围的可选属性组成

> Cookie的极大特性：	
>
> ① 自动发送
>
> ②域名独立
>
> ③过期时限
>
> ④4KB限制

#### 4.Cookie在身份认证的作用 

客户端第一次请求服务器时，服务器通过**响应头**的形式发送一个Cookie，客户端会自动保存在浏览器中。

随后，客户端每次请求服务器时，浏览器会自动将身份认证相关的Cookie，通过**请求头**的形式发送给服务器

#### 5.Cookie不具有安全性

![image-20220805142313284](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220805142313284.png)

#### 6.提高身份认证的安全性

简而言之就是使用Cookie+Session的形式进行验证

![image-20220805142501346](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220805142501346.png)



### :star:②Express中使用Session认证

>①安装express-session中间件  npm i express-session
>
>②配置express-session中间件 app.use(session({}))

```js
//导入session中间件
import session from "express-session";
import express from "express";
const app = express();
//注册session中间件
app.use(session({
    secret:'keyboard cat',//secret 属性的值可以为任意字符串，但建议使用一个随机字符串
    resave:false,//固定写法
    saveUninitialized:true//固定写法
}))
```

③向session中存数据（可以通过req.session存数据）

```js
//导入session中间件
import session from "express-session";
import express from "express";
const app = express();
//不要忽略乱码问题
app.use(express.urlencoded({extends:false}));
//注册session中间件
app.use(session({
    secret:'keyboard cat',//secret 属性的值可以为任意字符串，但建议使用一个随机字符串
    resave:false,//固定写法
    saveUninitialized:true//固定写法
}))

app.post('/api/login',(req,res)=>{
    if(req.body.name!=='admin'||req.body.password!=='123'){
        return res.send({status:1,msg:'用户名或密码错误'})
    }
    req.session.user = req.body//将用户名和密码存入session
    req.session.islogin = true//将用户登录状态存入session
    res.send({status:0,msg:'登录成功'})
    console.log(req.session);
})
app.listen(8080,()=>{
    console.log('服务器启动成功 http://127.0.0.1:8080')
})
```

![image-20220805144418923](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220805144418923.png)

![image-20220805144428594](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220805144428594.png)



④从Session中取数据

```js
app.get('/api/name',(req,res)=>{
    if(req.session.islogin){
        return res.send({status:0,msg:'success',name:req.session.user.name})
    }
    res.send({starus:1,msg:'fail'})
})
```



⑤清空session

```js
app.post('/api/logout',(req,res)=>{
    req.session.destroy()
    res.send({status:0,msg:'success'})
})
```



### ③JWT认证机制(前后端分离)

#### 1.Session认证局限性

Session认证机制需要配合Cookie才能实现，由于Cookie默认不支持跨域访问，所以当涉及到跨域请求接口，需要做很多额外的配置，才能实现。

#### 2.JWT工作原理(token)

![image-20220805162017662](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220805162017662.png)

#### 3.JWT组成成分

![image-20220805162156870](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220805162156870.png)

> Payload部分才是真正的用户信息，是加密过的字符串
>
> Header和Signature是安全相关的部分

#### 4.JWT的使用方式

客户端收到服务器的JWT后，通常存储到localStorage或sessionStorage中

此后，客户端每次与服务端通信，都要带上这个字符串，推荐把JWT放在HTTP的请求头的Authorization字段中

```js
Authorization:Bearer <token>
```



### ④在Express中使用JWT

```js
npm install jsonwebtoken express-jwt//两个包
//jsonwebtoken用于生成JWT字符串
//express-jwt用于字符串解析还原成JSON对象
```

![image-20220805163356585](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220805163356585.png)

![image-20220805163404258](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220805163404258.png)

![image-20220805163851416](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220805163851416.png)

![image-20220805163519092](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220805163519092.png)

![image-20220805163752082](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220805163752082.png)

![image-20220805164005680](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220805164005680.png)

![image-20220805164030645](C:\Users\22476\AppData\Roaming\Typora\typora-user-images\image-20220805164030645.png)
