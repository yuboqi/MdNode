# 笔记和代码在

![image-20220713145733672](.\picture\image-20220713145733672.png)





# 一、Vue核心

## 数据绑定

### 		①v-bind单向数据绑定

![image-20220708144253679](.\picture\image-20220708144253679.png)

```html
    <div class="root">
        <h1>Hello,{{name}} ,{{age}}</h1>
        <h1>Hello,{{school.name}} ,{{age}}</h1>
        <a v-bind:href="school.url">百度</a>
        <a :href="school.url">百度</a>
    </div>

    <script>
        Vue.config.productionTip = false;
        
        new Vue({
            el:'.root',
            data:{
                name:'尚硅谷123',
                age:'18',
                school:{
                    name:'ybq',
                    url:'http://www.baidu.com'
                }
             
            }
        })
```



### 		:star:②v-model双向绑定

![image-20220708151351267](.\picture\image-20220708151351267.png)

```html
    <div id="text">
        数据双向绑定：<input type="text" v-model:value="name"><br>
        数据双向绑定：<input type="text" v-model="name"><br>
        数据单项绑定：<input type="text" v-bind:value="name"><br>
    </div>

```





## data和el的两种写法

![image-20220708153010385](.\picture\image-20220708153010385.png)



```js
//el和data的第一种写法
    new Vue({
        el:'#root',
        data:{
            name:'张三'
        }
    })

//el和data 的第二种写法（模块化常用data第二种写法）
    const v =new Vue({
        
        // data(){//相当于 data:function(){}
        //     name:'张三'
        // }
        data:function(){
            return{
                name:'张三'
            }
        }
    })
    v.$mount('#root') //相当于 el:'#root'注意在函数外面
 
```





## :star:MVVM模型

![image-20220708154154894](.\picture\image-20220708154154894.png)

![image-20220708154655937](.\picture\image-20220708154655937.png)

![image-20220708155145254](.\picture\image-20220708155145254.png)



## :exclamation:数据代理

### 	:exclamation:Object.defineProperty

```js
    let number = 18;
    let person = {
        name : 'ybq',
        adress:'beijing',
    }
    // Object.defineProperty(person,'age',{
    //     value:'18',
    //     enumerable:true,//控制属性是否可以被枚举，默认值false
    //     writable:true,//控制属性是否可以被修改，默认值false
    //     configurable:true,//控制属性是否可以被删除，默认值false
    // })

    Object.defineProperty(person, 'age',{
        
        get:function(){
            return number;
        }
    })//该方法可以让值实时更改
```



![image-20220708164202872](.\picture\image-20220708164202872.png)

**用obj2.x =124，来修改x的值会调用set方法，将set的value值赋值给obj.x来实现数据代理**

![image-20220708171123517](.\picture\image-20220708171123517.png)



## 事件处理

### 	①事件的基本使用

![image-20220708174051384](.\picture\image-20220708174051384.png)

```html
<body>
    <div id="root">
       <button v-on:click="showInfo">点我提示信息</button>
       <!-- 第二种写法 -->
       <button @click="showInfo1">点我提示信息（不传参）</button>
       <button @click="showInfo2('aas',$event)">点我提示信息（传参）</button>
    </div>
</body>

<script>
    Vue.config.productionTip = false;
    const vm =new Vue({
        el:'#root',
        methods:{
            showInfo(event){
                alert('点击了按钮1');
                // console.log(this);//this指向Vue实例  this是vm
            },
            showInfo1(event){
                alert('点击了按钮2');
                // console.log(this);//this指向Vue实例  this是vm
            },
            showInfo2(s,event){

                alert('点击了按钮' +s);
                // console.log(this);//this指向Vue实例  this是vm
            }
        }
    })
```

**注意：在事件函数后面加（）可以传参给函数，字符串，数字类型等**



### 	:star:②事件修饰符（可连写 .prevent.stop）

![image-20220708174330633](.\picture\image-20220708174330633.png)

```js
<body>
    <div id="root">
       <a href="http://atguigu.com" @click.prevent="showInfo">尚硅谷</a>
    </div>
</body>

<script>
    Vue.config.productionTip = false;
    new Vue({ 
        el:'#root',
        data:{

        },
        methods:{
            showInfo(){
                alert('尚硅谷');
            }
        }
    })
```



### 	:star:③键盘事件（可连写 @keyup.ctrl.y）

![image-20220708195340682](.\picture\image-20220708195340682.png)

![image-20220708194858277](.\picture\image-20220708194858277.png)

![image-20220708195119495](.\picture\image-20220708195119495.png)



## 计算属性与监视

![image-20220708205141218](.\picture\image-20220708205141218.png)

![image-20220708205830692](.\picture\image-20220708205830692.png)



![image-20220708205813175](.\picture\image-20220708205813175.png)

### 	①用插值语法完成案例

```js
    <div id="root">
        姓：<input type="text" v-model="firstName"><br>
        名：<input type="text" v-model="lastName"><br>
        全名：<span>{{firstName.slice(0,3)}} - {{lastName}}</span>
        <!-- slice是截取firstName中的前三个字符，{{firstName.slice(0,3)}} -->
    </div>

    <script>
        Vue.config.productionTip = false;

        new Vue({
            el:'#root',
            data:{
                firstName:'张123',
                lastName:'三123',
            }
        })
    </script>
```



### 	②用methods完成案例

```js
   <div id="root">
        姓：<input type="text" v-model="firstName"><br>
        名：<input type="text" v-model="lastName"><br>
        全名：<span>{{fullName()}}</span>
    </div>

    <script>
        Vue.config.productionTip = false;

        const vm =new Vue({
            el:'#root',
            data:{
                firstName:'张123',
                lastName:'三123',
            },
            methods:{
                fullName(){
                    return this.firstName + '-' + this.lastName;
                }
            }
        })
    </script>
```



### 	:star:③用计算属性完成案例computed:

```js
    <div id="root">
      姓：<input type="text" v-model="firstName" /><br />
      名：<input type="text" v-model="lastName" /><br />
      全名：<span>{{fullName}}</span>
    </div>

    <script>
      Vue.config.productionTip = false;

      const vm = new Vue({
        el: "#root",
        data: {
          firstName: "张123",
          lastName: "三123",
        },
        computed: {
          fullName: {
            get() {
              return this.firstName + "-" + this.lastName;
            },

            set(value) {
              const lits = value.split("-");
              this.firstName = lits[0];
              this.lastName = lits[1];
            },
          },
        },
      });
```

### 	当你所需要的属性只读不需修改时，可以不用写set属性



## 监视属性

### 	①天气案例

![image-20220709094924414](.\picture\image-20220709094924414.png)

```js
<body>
    <div id="root">
       <h2>今天天气很{{info}}</h2>
       <button @click="changeWeather">切换天气</button>
    </div>
</body>

<script>
    Vue.config.productionTip = false;
    new Vue({
        el:'#root',
        data:{
            isHot:true,
        },
        methods: {
            changeWeather(){
                this.isHot = !this.isHot;
            }
        },
        computed:{
            info(){
                return this.isHot ? '炎热' : '凉爽';
            }
        }
    })
</script>
```



### 	:star:②监视属性

![image-20220709095750905](.\picture\image-20220709095750905.png)

```js
  <body>
    <div id="root">
      <h2>今天天气很{{info}}</h2>
      <button @click="changeWeather">切换天气</button>
    </div>
  </body>

  <script>
    Vue.config.productionTip = false;
    const vm = new Vue({
      el: "#root",
      data: {
        isHot: true,
      },
      methods: {
        changeWeather() {
          this.isHot = !this.isHot;
        },
      },
      computed: {
        info() {
          return this.isHot ? "炎热" : "凉爽";
        },
      },
      watch: {
        //方法一
        isHot: {
          immediate: true, //初始化时就让handler执行
          handler(newValue, oldValue) {
            //当isHot变化时执行
            console.log("isHot修改了", newValue, oldValue);
          },
        },
      },
    });
    vm.$watch("isHot", {
      //方法二
      immediate: true, //初始化时就让handler执行
      handler(newValue, oldValue) {
        //当isHot变化时执行
        console.log("isHot修改了", newValue, oldValue);
      },
    });
  </script>
```



### :exclamation:	③深度监视deep

![image-20220709101347452](.\picture\image-20220709101347452.png)

```
  <body>
    <div id="root">
      <h2>a的值是：{{number.a}}</h2><br>
      <button @click="number.a++">点我让a+1</button><br>
      <h2>b的值是：{{number.b}}</h2>
      <button @click="number.b++">点我让b+1</button><br>
    </div>
  </body>

  <script>
    Vue.config.productionTip = false;
    const vm = new Vue({
      el: "#root",
      data: {
        isHot: true,
        number:{
          a:1,
          b:1,
        }
      },
      watch: {
        number: {
          deep: true,
          handler(newValue, oldValue) {
            //当isHot变化时执行
            console.log("number修改了");
          },
        },
      },
    });
  </script>
```

### 简写

#### 	条件：当监测不需要immediate和deep时可以简写

![image-20220709102508274](.\picture\image-20220709102508274.png)

![image-20220709102959036](.\picture\image-20220709102959036.png)



## :exclamation:computed和watch区别

![image-20220709104611193](.\picture\image-20220709104611193.png)





## 绑定样式

### 	⭐️ `:star:`①绑定class样式(字符串写法)

![image-20220709105314972](.\picture\image-20220709105314972.png)

### 	⭐️ `:star:`②class绑定(数组写法)

![image-20220709110736742](.\picture\image-20220709110736742.png)



### 	③class绑定(对象写法)

![image-20220709111113763](.\picture\image-20220709111113763.png)



### 	④style绑定(不常用)

![image-20220709111726845](.\picture\image-20220709111726845.png)

![image-20220709111804908](.\picture\image-20220709111804908.png)	



## :star:条件渲染

![image-20220709113755482](.\picture\image-20220709113755482.png)

![image-20220709112947146](.\picture\image-20220709112947146.png)

**v-show 的逻辑是改变display的属性值来进行渲染**

**v-if的逻辑是新增 删除dom结构来进行渲染的，所以当快速切换要保证效率是尽量用v-show**



![image-20220709113259610](.\picture\image-20220709113259610.png)

**v-if  v-else-if不允许被中途加上东西打断，如图则div  @下面的v-else-if属性失效**



### v-if和template配合使用

![image-20220709113607524](.\picture\image-20220709113607524.png)

**template模板的使用在渲染后不会保留template标签，这样不会影响dom结构，只能配合v-if使用**



## 列表渲染

### 	①基本列表

​	![image-20220709151242701](.\picture\image-20220709151242701.png)



### ⭐️ `:star:`	②key的作用与原理(index作为key)



![image-20220709152834491](.\picture\image-20220709152834491.png)

**当以index作为key时，如果新增数据的数据打乱排列顺序，则会导致文本错乱情况，而且还重复地有已经存在的数据产生，极大的影响了内存和速度，当然如果不写key，Vue会自动以index索引值作为key**



### 	⭐️ `:star:`③key的作用与原理(id作为key)

![image-20220709153115714](.\picture\image-20220709153115714.png)



```js
<body>
    <div id="root">
        <button @click.once="add">新增</button>
       <ul>
        <li v-for="(p,index) in persons" :key="p.id">
            {{p.name}}-{{p.age}}
            <input type="text">
        </li>

       </ul>
    </div>
</body>

<script>
    Vue.config.productionTip = false;
    new Vue({
        el:'#root',
        data:{
            persons:[
                {id:'001',name:'张三',age:18},
                {id:'002',name:'李四',age:20},
                {id:'003',name:'王五',age:22},
            ]
        },
        methods: {
            add(){
                this.persons.unshift({id:'004',name:'赵六',age:24});
            }
        },
    })
</script>
```

### 	⭐️ `:star:`④for in  和 for  of区别

![image-20220709154517930](.\picture\image-20220709154517930.png)

![image-20220709155126116](.\picture\image-20220709155126116.png)



## 列表过滤(模糊搜索)

```js
<body>
    <div id="root">
        <input type="text" v-model="keywords">
       <ul>
        <li v-for="(p,index) in filterPersons" :key="p.id">
            {{p.name}}-{{p.age}}
        </li>

       </ul>
    </div>
</body>

<script>
    Vue.config.productionTip = false;
    //#region 列表过滤
    // new Vue({
    //     el:'#root',
    //     data:{
    //         persons:[
    //             {id:'001',name:'马冬梅',age:18},
    //             {id:'002',name:'周冬雨',age:20},
    //             {id:'003',name:'周杰伦',age:22},
    //         ],
    //         keywords:'',
    //     },
    //     computed:{//用computed来计算属性
    //         filterPersons(){
    //             return this.persons.filter((p)=>{
    //                 return p.name.indexOf(this.keywords)>-1;
    //             })
    //         }
    //     }
    // })
    //#endregion 
    //用watch来监听属性
    new Vue({
        el:'#root',
        data:{
            persons:[
                {id:'001',name:'马冬梅',age:18},
                {id:'002',name:'周冬雨',age:20},
                {id:'003',name:'周杰伦',age:22},
            ],
            keywords:'',
            filterPersons:[],
        },
        watch:{
            keywords:{
            immediate:true,
           handler(val){
            this.filterPersons = this.persons.filter((p)=>{
                return p.name.indexOf(val)>-1;
            })
           }
            }

        }
    })
</script>
```



## 列表排序

```js
<body>
    <div id="root">
        <input type="text" v-model="keywords">
        <button @click="sorttype = 2">升序</button>
        <button @click="sorttype = 1">降序</button>
        <button @click="sorttype = 0">原序</button>
        <ul>
            <li v-for="(p,index) in filterPersons" :key="p.id">
                {{p.name}}---{{p.age}}
            </li>
        </ul>
    </div>
    <script>
       Vue.config.productionTip = false
    new Vue({
        el:'#root',
        data:{
            persons:[
                {id:'001',name:'马冬梅',age:18},
                {id:'002',name:'周冬雨',age:20},
                {id:'003',name:'周杰伦',age:22},
            ],
            keywords:'',
            sorttype:0,
        },
        computed:{//用computed来计算属性
            filterPersons(){
                const arr = this.persons.filter((p)=>{
                    return p.name.indexOf(this.keywords)>-1;
                })
                if(this.sorttype != 0){
                    arr.sort((p1,p2)=>{
                        return this.sorttype ==1?p2.age-p1.age:p1.age-p2.age;
                    })
                }
                return arr;
            }
        }
    })
    </script>
```

**sort()方法会给arr数组进行排序，升序的话返回p1.age -p2.age**



## :exclamation:Vue.set方法

### :exclamation:Vue.set方法不能对于Vue本身属性和Vue根属性(data属性)直接使用，会报错，只能对于属性对象进行添加属性

```js
<body>
    <div id="root">
        <button @click="addLeader">点我新增校长</button>
       <h2>学校：{{school.name}}</h2>
       <h2>地址：{{school.adress}}</h2>
       <h2>校长:{{school.leader}}</h2>
       
    </div>
</body>

<script>
    Vue.config.productionTip = false;
    const vm =new Vue({
        el:'#root',
        data:{
            school:{
                name:'清华大学',
                adress:'北京市海淀区'
            }
        },
        methods: {
            addLeader(){
                 // Vue.set(this.school,'leader','张三');
                this.$set(this.school,'leader','张三');
            }
        },
    })
</script>
```



## :exclamation:Vue监测数据的原理：

![image-20220709201853991](.\picture\image-20220709201853991.png)



##  :exclamation:Vue监测数组的原理

#### Vue无法让用户直接通过数组的索引值将修改的数据直接完成响应式，只能通过系列Vue的数组方法来修改值(该方法为Vue通过数组对象Array包装过后的方法)，当然也能通过set方法来实现修改。

![image-20220709200025041](.\picture\image-20220709200025041.png)

![image-20220709200352107](.\picture\image-20220709200352107.png)

![image-20220709200448491](.\picture\image-20220709200448491.png)





## :star:收集表单数据

![image-20220710092304516](.\picture\image-20220710092304516.png)

```js
<body>
    <div id="root">
       <form @submit.prevent="demo">
        账号： <input type="text" v-model.trim="personInfo.account" placeholder="请输入账号"> <br>
        密码： <input type="password" v-model="personInfo.password" > <br>
        年龄： <input type="number" v-model.number="personInfo.age"> <br>
        性别： 
        男<input type="radio" value="男" v-model="personInfo.sex" name="sex">
        女<input type="radio" value="女" v-model="personInfo.sex" name="sex"><br>
        爱好：
        学习<input type="checkbox" v-model="personInfo.hobby" value="study" >
        游戏<input type="checkbox" v-model="personInfo.hobby" value="game">
        抽烟<input type="checkbox" v-model="personInfo.hobby" value="smoke" >
        <br>
        所属校区
        <select v-model="personInfo.adress">
            <option value="">请选择校区</option>
            <option value="北京">北京</option>
            <option value="上海">上海</option>
        </select>
        <br>
        其他信息:
        <textarea v-model.lazy="personInfo.other"></textarea>
        <br>
        <input type="checkbox" v-model="personInfo.agree" >阅读协议<br>
        <button>提交</button>
    </form>
    </div>
</body>

<script>
    Vue.config.productionTip = false;
    new Vue({
        el:'#root',
        data:{
            personInfo:{
                account:'',
                password:'',
                age:'',
                sex:'',
                hobby:[],
                adress:'',
                other:'',
                agree:'',
            }
        },
        methods: {
            demo(){
                console.log(JSON.stringify(this.personInfo));
            }
        },
    })
</script>
```



## :star:过滤器

![image-20220710095831126](.\picture\image-20220710095831126.png)

```js
<body>
    <div id="root">
        时间戳时间：{{time}}<br>
        <!-- methods实现 -->
        格式化后的时间：{{formatTime()}}<br>
        <!-- 计算属性实现 -->
        格式化后的时间：{{formatTime2}}<br>
        <!-- 过滤器实现 -->
        格式化后的时间：{{time | formatTime3}}<br>
        格式化后的时间：{{time | formatTime3('YYYY-MM-DD')}}<br>
    </div>

    <script>
        Vue.config.productionTip = false;
        //全局过滤器
        // Vue.filter('formatTime3',function(value,str='YYYY-MM-DD HH:mm:ss'){
        //     return dayjs(value).format(str);
        // })
        new Vue({
            el:'#root',
            data:{
                time:1657418616133,
            },
            methods:{
                formatTime(){
                    return dayjs(this.time).format('YYYY-MM-DD HH:mm:ss');
                },
            },
            computed:{
                formatTime2(){
                    return dayjs(this.time).format('YYYY-MM-DD HH:mm:ss');
                },
                },
            //局部过滤器
                filters:{
                formatTime3(value,str='YYYY-MM-DD HH:mm:ss'){
                    return dayjs(value).format(str);
                }
            }    
            }
        )
    </script>
</body>
```

#### :star:过滤器不允许用于v-model内



## :exclamation:Vue内置指令

![image-20220710102028598](.\picture\image-20220710102028598.png)



![image-20220710103545886](.\picture\image-20220710103545886.png)

![image-20220710104404169](.\picture\image-20220710104404169.png)

![image-20220710104354121](.\picture\image-20220710104354121.png)

![image-20220710104618492](.\picture\image-20220710104618492.png)

```js
    <div id="root">
       <h2 v-once>初始化n的值为:{{n}}</h2>
       <h2>当前n的值为:{{n}}</h2>
       <button @click="n++">点我n+1</button>
    </div>
</body>

<script>
    Vue.config.productionTip = false;
    new Vue({
        el:'#root',
        data:{
            n:'1'
        },
        methods: {
            
        },
    })
```

![image-20220710105052234](.\picture\image-20220710105052234.png)



## :star:自定义指令

![image-20220710161021044](.\picture\image-20220710161021044.png)

```js
<body>
    <div id="root">
       <h2>当前n 的值是：<span v-text="n"></span></h2>
       <h2>放大10倍n 的值是：<span v-big="n"></span></h2>
       <button @click="n++">点我n++</button>
    </div>
</body>

<script>
    Vue.config.productionTip = false;
    new Vue({
        el:'#root',
        data:{
            n:1,
        },
        directives:{
            big(element,binding){
                element.innerText = binding.value*10;
            }
        }
    })
</script>
```



```js
<body>
    <div id="root">
       <h2>当前n 的值是：<span v-text="n"></span></h2>
       <h2>放大10倍n 的值是：<span v-big="n"></span></h2>
       <button @click="n++">点我n++</button>
       <input type="text" v-fbig:value="n">
    </div>
</body>

<script>
    Vue.config.productionTip = false;
    new Vue({
        el:'#root',
        data:{
            n:1,
        },
        directives:{
            big(element,binding){
                element.innerText = binding.value*10;
            },

            fbig:{
                //指令与元素成功绑定
                bind(element,binding){
                    element.value = binding.value;
                },
				//指令所在元素被插入页面
                inserted(element,binding){
                    element.focus();
                },
				//指令所在的模板被重新解析
                update(element,binding) {
                    element.focus();
                    element.value = binding.value;
                },
                },
            }
        }
    )
</script>
```



## :exclamation:生命周期

![image-20220710165507367](.\picture\image-20220710165507367.png)

### 	呼吸灯实例

![image-20220710165613800](.\picture\image-20220710165613800.png)

![image-20220710165543079](.\picture\image-20220710165543079.png)

```js
<body>//未实现销毁效果，也没能关闭定时器
    <div id="root">
       <h2 :style="{opacity:opacity}" >欢迎学习Vue</h2>
       <!-- <div v-once>{{change()}}</div> -->
    </div>
</body>

<script>
    Vue.config.productionTip = false;
    new Vue({
        el:'#root',
        data:{
            opacity:1,
        },
        methods: {
            // change(){
            //     console.log('change');
            //     setInterval(()=>{
            //         this.opacity -= 0.1;
            //         if(this.opacity <= 0){
            //             this.opacity = 1;
            //         }
            //     },16)
            // }
        },
        mounted() {
            setInterval(()=>{
                    this.opacity -= 0.1;
                    if(this.opacity <= 0){
                        this.opacity = 1;
                    }
                },16)
        },
    })
</script>
```

![image-20220710192516860](.\picture\image-20220710192516860.png)

![image-20220710193630374](.\picture\image-20220710193630374.png)

```js
<body>//完成销毁效果，关闭定时器
    <div id="root">
       <h2 :style="{opacity : opacity}">欢迎学习Vue</h2><br>
       <button @click="stop">销毁Vue</button>
    </div>
</body>

<script>
    Vue.config.productionTip = false;
    new Vue({
        el:'#root',
        data:{
            opacity:1,
        },
        methods: {
            stop(){
                this.$destroy();
            }
        },
        mounted() {
           this.timer= setInterval(()=>{
                this.opacity -=0.1;
                if(this.opacity<=0){
                    this.opacity = 1;
                }
            },100)
        },
        beforeDestroy() {
            clearInterval(this.timer);
        },

    })
</script>
```



# 二、Vue组件化编程

## :star:组件的定义

![image-20220711085849923](.\picture\image-20220711085849923.png)

![image-20220710195914829](.\picture\image-20220710195914829.png)

![image-20220710200029421](.\picture\image-20220710200029421.png)

![image-20220710200036162](.\picture\image-20220710200036162.png)

![image-20220710200048434](.\picture\image-20220710200048434.png)

```html
<body>
    <div id="root">
       <school></school>
    </div>
</body>

<script>
    Vue.config.productionTip = false;
    Vue.component('school',{//全局组件
        template:'<div>{{school.name}}</div>',
        data:function(){
            return {
                school:{
                    name:'清华大学'
                }
            }
        }
    })

    // const a = Vue.extend({//局部组件
    //     template:`
    //     <div>
    //     <h2>学校姓名:{{schoolName}}</h2>
    //     <h2>学校地址:{{adress}}</h2>
    //     <button @click="showName">展示名字</button>
    //     </div>
    //     `,
    //     data(){
    //         return {
    //             schoolName:'北京大学',
    //             adress:'北京市海淀区'
    //         }
    //     },
    //     methods: {
    //         showName(){
    //             alert(this.schoolName)
    //         }
    //     },
    // });
    new Vue({
        el:'#root',

        components:{
            // school : a,
        }

    })
```



## :star:组件的嵌套

![image-20220711093153090](.\picture\image-20220711093153090.png)

```Vue
<body>
    <div id="root">
       
    </div>
</body>

<script>
    Vue.config.productionTip = false;

    const student = Vue.extend({
        template:`
            <div>
                <h2>学生信息</h2>
                <p>姓名：{{name}}</p>
                <p>年龄：{{age}}</p>   
            </div>
        `,
        data(){
            return {
                    name:'zhangsan',
                    age:18
            }
        },
    });
    const school = Vue.extend({
        template:`
            <div>
                <h2>{{name}}</h2>
                <p>{{address}}</p>
                <student></student>   
            </div>
        `,
        data(){
            return {
                    name:'清华大学',
                    address:'北京市海淀区'
            }
        },
        components:{
            student
        }
    });


    
    const hello = Vue.extend({
        template:`
       <h2>{{msg}}</h2>
        `,
        data(){
            return {
                msg:'hello'
            }
        },
    });

    const app = Vue.extend({
        template:`
            <div>
            <school></school>
            <hello></hello>    
            </div>
        `,
        components:{
            school,
            hello
        },
    });

    new Vue({
        template:`<app></app>`,
        el:'#root',
        components:{
            app
        },
    })
</script>
```



## :exclamation:VueComponent

![image-20220711104035925](.\picture\image-20220711104035925.png)





## :exclamation:Vue和Component的关系

![image-20220711110649224](.\picture\image-20220711110649224.png)



## :exclamation:三、使用Vue脚手架

![image-20220711160027786](.\picture\image-20220711160027786.png)

![image-20220711160906360](.\picture\image-20220711160906360.png)

![image-20220711160927153](.\picture\image-20220711160927153.png)

![image-20220711160936174](.\picture\image-20220711160936174.png)



## :star:ref属性

![image-20220711163910974](.\picture\image-20220711163910974.png)

![image-20220711163947829](.\picture\image-20220711163947829.png)

![image-20220711163822107](.\picture\image-20220711163822107.png)

```vue
<template>
  <div>
    <h2 v-text="msg" ref="title"></h2>
    <button @click="showInf">点我得到H2信息</button>
    <School></School>
  </div>
</template>

<script>
import School from './components/School'
export default {
    name:'App',
    components:{
        School
    },
    data(){
        return {
            msg:'hello vue'
        }
    },
    methods: {
        showInf(){
            console.log(this.$refs.title)
        }
    },
    
}
</script>

```



## :star:props配置

![image-20220711193451098](.\picture\image-20220711193451098.png)

```vue

School.vue
<template>
  <div class="demo">
    <h2>校长名称：{{name}}</h2>
    <h2>校长年龄：{{newAge}}</h2>
     <button @click="addAge">点我age+1</button>
  </div>
</template>

<script>
export default {
    name:'School',
    data() {
        return{
            newAge: this.age,
        }
    },
    methods: {
        addAge(){
            this.newAge++;
        }
    },
    //简单声明接收
    // props:['name','age'],

    //接收的同时对数据进行限制
    // props:{
    //     name:String,
    //     age:Number,
    // }
    
    // 接收的同时对数据进行限制，默认值的指定
    props:{
        name:{
            type:String,
            require:true,
        },
        age:{
            type:Number,
            require:true,
            default:18,
        },
    }
}
</script>

App.vue
<template>
  <div>
    <h2 v-text="msg"></h2>
    <School name="小张" :age="28"></School>
  </div>
</template>

<script>
import School from './components/School'
export default {
    name:'App',
    components:{
        School
    },
    data(){
        return {
            msg:'hello vue'
        }
    },  
}
</script>
```

![image-20220711195102818](.\picture\image-20220711195102818.png)







## :star:mixin混入

![image-20220711202428144](.\picture\image-20220711202428144.png)

```vue
Student.vue
<template>
  <div class="demo">
    <h2 @click="showName">校长名称：{{name}}</h2>
    <h2>校长年龄：{{age}}</h2>
  </div>
</template>

<script>
import{mixin} from '../mixin'
export default {
    name:'School',
    data() {
       return {
           name:'小张',
           age:18,
       }
    },
    mixins:[mixin],
}
</script>
```

```js
mixin.js

export const mixin = {
    methods: {
        showName(){
            alert(this.name);
        }
    },

}

```



## :star:Vue插件

![image-20220712094417459](.\picture\image-20220712094417459.png)



## :exclamation:scoped样式

![image-20220712095506145](.\picture\image-20220712095506145.png)



## 总结TodoList案例

1. 组件化编码流程：

   ​	(1).拆分静态组件：组件要按照功能点拆分，命名不要与html元素冲突。

   ​	(2).实现动态组件：考虑好数据的存放位置，数据是一个组件在用，还是一些组件在用：

   ​			1).一个组件在用：放在组件自身即可。

   ​			2). 一些组件在用：放在他们共同的父组件上（<span style="color:red">状态提升</span>）。

   ​	(3).实现交互：从绑定事件开始。

2. props适用于：

   ​	(1).父组件 ==> 子组件 通信

   ​	(2).子组件 ==> 父组件 通信（要求父先给子一个函数）

3. 使用v-model时要切记：v-model绑定的值不能是props传过来的值，因为props是不可以修改的！

4. props传过来的若是对象类型的值，修改对象中的属性时Vue不会报错，但不推荐这样做。



## :exclamation:组件的自定义事件

1. 一种组件间通信的方式，适用于：<strong style="color:red">子组件 ===> 父组件</strong>

2. 使用场景：A是父组件，B是子组件，B想给A传数据，那么就要在A中给B绑定自定义事件（<span style="color:red">事件的回调在A中</span>）。

3. 绑定自定义事件：

   1. 第一种方式，在父组件中：```<Demo @atguigu="test"/>```  或 ```<Demo v-on:atguigu="test"/>```

   2. 第二种方式，在父组件中：

      ```js
      <Demo ref="demo"/>
      ......
      mounted(){
         this.$refs.xxx.$on('atguigu',this.test)
      }
      ```

   3. 若想让自定义事件只能触发一次，可以使用```once```修饰符，或```$once```方法。

4. 触发自定义事件：```this.$emit('atguigu',数据)```		

5. 解绑自定义事件```this.$off('atguigu')```

6. 组件上也可以绑定原生DOM事件，需要使用```native```修饰符。

7. 注意：通过```this.$refs.xxx.$on('atguigu',回调)```绑定自定义事件时，回调<span style="color:red">要么配置在methods中</span>，<span style="color:red">要么用箭头函数</span>，否则this指向会出问题！



## :exclamation:全局事件总线（GlobalEventBus）

1. 一种组件间通信的方式，适用于<span style="color:red">任意组件间通信</span>。

2. 安装全局事件总线：

   ```js
   new Vue({
   	......
   	beforeCreate() {
   		Vue.prototype.$bus = this //安装全局事件总线，$bus就是当前应用的vm
   	},
       ......
   }) 
   ```

3. 使用事件总线：

   1. 接收数据：A组件想接收数据，则在A组件中给$bus绑定自定义事件，事件的<span style="color:red">回调留在A组件自身。</span>

      ```js
      methods(){
        demo(data){......}
      }
      ......
      mounted() {
        this.$bus.$on('xxxx',this.demo)
      }
      ```

   2. 提供数据：```this.$bus.$emit('xxxx',数据)```

4. 最好在beforeDestroy钩子中，用$off去解绑<span style="color:red">当前组件所用到的</span>事件。



## :exclamation:消息订阅与发布（pubsub）

1. 一种组件间通信的方式，适用于<span style="color:red">任意组件间通信</span>。

2. 使用步骤：

   1. 安装pubsub：```npm i pubsub-js```

   2. 引入: ```import pubsub from 'pubsub-js'```

   3. 接收数据：A组件想接收数据，则在A组件中订阅消息，订阅的<span style="color:red">回调留在A组件自身。</span>

      ```js
      methods(){
        demo(data){......}
      }
      ......
      mounted() {
        this.pid = pubsub.subscribe('xxx',this.demo) //订阅消息
      }
      ```

   4. 提供数据：```pubsub.publish('xxx',数据)```

   5. 最好在beforeDestroy钩子中，用```PubSub.unsubscribe(pid)```去<span style="color:red">取消订阅。</span>



## :star:nextTick

1. 语法：```this.$nextTick(回调函数)```
2. 作用：在下一次 DOM 更新结束后执行其指定的回调。
3. 什么时候用：当改变数据后，要基于更新后的新DOM进行某些操作时，要在nextTick所指定的回调函数中执行。



## Vue封装的过度与动画

1. 作用：在插入、更新或移除 DOM元素时，在合适的时候给元素添加样式类名。

2. 图示：

   ![image-20220715150346579](.\picture\image-20220715150346579.png)

3. 写法：

   1. 准备好样式：

      - 元素进入的样式：
        1. v-enter：进入的起点
        2. v-enter-active：进入过程中
        3. v-enter-to：进入的终点
      - 元素离开的样式：
        1. v-leave：离开的起点
        2. v-leave-active：离开过程中
        3. v-leave-to：离开的终点

   2. 使用```<transition>```包裹要过度的元素，并配置name属性：

      ```vue
      <transition name="hello">
      	<h1 v-show="isShow">你好啊！</h1>
      </transition>
      ```

   3. 备注：若有多个元素需要过度，则需要使用：```<transition-group>```，且每个元素都要指定```key```值。



## :exclamation:vue脚手架配置代理

### 方法一

​	在vue.config.js中添加如下配置：

```js
devServer:{
  proxy:"http://localhost:5000"
}
```

说明：

1. 优点：配置简单，请求资源时直接发给前端（8080）即可。
2. 缺点：不能配置多个代理，不能灵活的控制请求是否走代理。
3. 工作方式：若按照上述配置代理，当请求了前端不存在的资源时，那么该请求会转发给服务器 （优先匹配前端资源）

### 方法二

​	编写vue.config.js配置具体代理规则：

```js
module.exports = {
	devServer: {
      proxy: {
      '/api1': {// 匹配所有以 '/api1'开头的请求路径
        target: 'http://localhost:5000',// 代理目标的基础路径
        changeOrigin: true,
        pathRewrite: {'^/api1': ''}
      },
      '/api2': {// 匹配所有以 '/api2'开头的请求路径
        target: 'http://localhost:5001',// 代理目标的基础路径
        changeOrigin: true,
        pathRewrite: {'^/api2': ''}
      }
    }
  }
}
/*
   changeOrigin设置为true时，服务器收到的请求头中的host为：localhost:5000
   changeOrigin设置为false时，服务器收到的请求头中的host为：localhost:8080
   changeOrigin默认值为true
*/
```

说明：

1. 优点：可以配置多个代理，且可以灵活的控制请求是否走代理。
2. 缺点：配置略微繁琐，请求资源时必须加前缀。



## :star:插槽

1. 作用：让父组件可以向子组件指定位置插入html结构，也是一种组件间通信的方式，适用于 <strong style="color:red">父组件 ===> 子组件</strong> 。

2. 分类：默认插槽、具名插槽、作用域插槽

3. 使用方式：

   1. 默认插槽：

```vue
父组件中：
        <Category>
           <div>html结构1</div>
        </Category>
子组件中：
        <template>
            <div>
               <!-- 定义插槽 -->
               <slot>插槽默认内容...</slot>
            </div>
        </template>
```

​		2.具名插槽：	

```vue
父组件中：
        <Category>
            <template slot="center">
              <div>html结构1</div>
            </template>

            <template v-slot:footer>
               <div>html结构2</div>
            </template>
        </Category>
子组件中：
        <template>
            <div>
               <!-- 定义插槽 -->
               <slot name="center">插槽默认内容...</slot>
               <slot name="footer">插槽默认内容...</slot>
            </div>
        </template>
```

​	3.作用域插槽：

1. 理解：<span style="color:red">数据在组件的自身，但根据数据生成的结构需要组件的使用者来决定。</span>（games数据在Category组件中，但使用数据所遍历出来的结构由App组件决定）

2. 具体编码：

```vue
父组件中：
		<Category>
			<template scope="scopeData">
				<!-- 生成的是ul列表 -->
				<ul>
					<li v-for="g in scopeData.games" :key="g">{{g}}</li>
				</ul>
			</template>
		</Category>

		<Category>
			<template slot-scope="scopeData">
				<!-- 生成的是h4标题 -->
				<h4 v-for="g in scopeData.games" :key="g">{{g}}</h4>
			</template>
		</Category>
子组件中：
        <template>
            <div>
                <slot :games="games"></slot>
            </div>
        </template>
		
        <script>
            export default {
                name:'Category',
                props:['title'],
                //数据在子组件自身
                data() {
                    return {
                        games:['红色警戒','穿越火线','劲舞团','超级玛丽']
                    }
                },
            }
        </script>
```





## :exclamation:Vuex(全部要看)

### 1.概念

​		在Vue中实现集中式状态（数据）管理的一个Vue插件，对vue应用中多个组件的共享状态进行集中式的管理（读/写），也是一种组件间通信的方式，且适用于任意组件间通信。

### 2.何时使用？

​		多个组件需要共享数据时

### 3.搭建vuex环境

1. 创建文件：```src/store/index.js```

```js
//引入Vue核心库
import Vue from 'vue'
//引入Vuex
import Vuex from 'vuex'
//应用Vuex插件
Vue.use(Vuex)

//准备actions对象——响应组件中用户的动作
const actions = {}
//准备mutations对象——修改state中的数据
const mutations = {}
//准备state对象——保存具体的数据
const state = {}

//创建并暴露store
export default new Vuex.Store({
	actions,
	mutations,
	state
})
```



2.在```main.js```中创建vm时传入```store```配置项

```js
......
//引入store
import store from './store'
......

//创建vm
new Vue({
	el:'#app',
	render: h => h(App),
	store
})
```



1. ###    4.基本使用

   1. 初始化数据、配置```actions```、配置```mutations```，操作文件```store.js```

      ```js
      //引入Vue核心库
      import Vue from 'vue'
      //引入Vuex
      import Vuex from 'vuex'
      //引用Vuex
      Vue.use(Vuex)
      
      const actions = {
          //响应组件中加的动作
      	jia(context,value){
      		// console.log('actions中的jia被调用了',miniStore,value)
      		context.commit('JIA',value)
      	},
      }
      
      const mutations = {
          //执行加
      	JIA(state,value){
      		// console.log('mutations中的JIA被调用了',state,value)
      		state.sum += value
      	}
      }
      
      //初始化数据
      const state = {
         sum:0
      }
      
      //创建并暴露store
      export default new Vuex.Store({
      	actions,
      	mutations,
      	state,
      })
      ```

   2. 组件中读取vuex中的数据：```$store.state.sum```

   3. 组件中修改vuex中的数据：```$store.dispatch('action中的方法名',数据)``` 或 ```$store.commit('mutations中的方法名',数据)```

      >  备注：若没有网络请求或其他业务逻辑，组件中也可以越过actions，即不写```dispatch```，直接编写```commit```





### 5.getters的使用

1. 概念：当state中的数据需要经过加工后再使用时，可以使用getters加工。

2. 在```store.js```中追加```getters```配置

   ```js
   ......
   
   const getters = {
   	bigSum(state){
   		return state.sum * 10
   	}
   }
   
   //创建并暴露store
   export default new Vuex.Store({
   	......
   	getters
   })
   ```

3. 组件中读取数据：```$store.getters.bigSum```



### 6.四个map方法的使用

1. <strong>mapState方法：</strong>用于帮助我们映射```state```中的数据为计算属性

   ```js
   computed: {
       //借助mapState生成计算属性：sum、school、subject（对象写法）
        ...mapState({sum:'sum',school:'school',subject:'subject'}),
            
       //借助mapState生成计算属性：sum、school、subject（数组写法）
       ...mapState(['sum','school','subject']),
   },
   ```

2. <strong>mapGetters方法：</strong>用于帮助我们映射```getters```中的数据为计算属性

   ```js
   computed: {
       //借助mapGetters生成计算属性：bigSum（对象写法）
       ...mapGetters({bigSum:'bigSum'}),
   
       //借助mapGetters生成计算属性：bigSum（数组写法）
       ...mapGetters(['bigSum'])
   },
   ```

3. <strong>mapActions方法：</strong>用于帮助我们生成与```actions```对话的方法，即：包含```$store.dispatch(xxx)```的函数

   ```js
   methods:{
       //靠mapActions生成：incrementOdd、incrementWait（对象形式）
       ...mapActions({incrementOdd:'jiaOdd',incrementWait:'jiaWait'})
   
       //靠mapActions生成：incrementOdd、incrementWait（数组形式）
       ...mapActions(['jiaOdd','jiaWait'])
   }
   ```

4. <strong>mapMutations方法：</strong>用于帮助我们生成与```mutations```对话的方法，即：包含```$store.commit(xxx)```的函数

   ```js
   methods:{
       //靠mapActions生成：increment、decrement（对象形式）
       ...mapMutations({increment:'JIA',decrement:'JIAN'}),
       
       //靠mapMutations生成：JIA、JIAN（对象形式）
       ...mapMutations(['JIA','JIAN']),
   }
   ```

> 备注：mapActions与mapMutations使用时，若需要传递参数需要：在模板中绑定事件时传递好参数，否则参数是事件对象。



### 7.模块化+命名空间

1. 目的：让代码更好维护，让多种数据分类更加明确。

2. 修改```store.js```

   ```javascript
   const countAbout = {
     namespaced:true,//开启命名空间
     state:{x:1},
     mutations: { ... },
     actions: { ... },
     getters: {
       bigSum(state){
          return state.sum * 10
       }
     }
   }
   
   const personAbout = {
     namespaced:true,//开启命名空间
     state:{ ... },
     mutations: { ... },
     actions: { ... }
   }
   
   const store = new Vuex.Store({
     modules: {
       countAbout,
       personAbout
     }
   })
   ```

3. 开启命名空间后，组件中读取state数据：

   ```js
   //方式一：自己直接读取
   this.$store.state.personAbout.list
   //方式二：借助mapState读取：
   ...mapState('countAbout',['sum','school','subject']),
   ```

4. 开启命名空间后，组件中读取getters数据：

   ```js
   //方式一：自己直接读取
   this.$store.getters['personAbout/firstPersonName']
   //方式二：借助mapGetters读取：
   ...mapGetters('countAbout',['bigSum'])
   ```

5. 开启命名空间后，组件中调用dispatch

   ```js
   //方式一：自己直接dispatch
   this.$store.dispatch('personAbout/addPersonWang',person)
   //方式二：借助mapActions：
   ...mapActions('countAbout',{incrementOdd:'jiaOdd',incrementWait:'jiaWait'})
   ```

6. 开启命名空间后，组件中调用commit

   ```js
   //方式一：自己直接commit
   this.$store.commit('personAbout/ADD_PERSON',person)
   //方式二：借助mapMutations：
   ...mapMutations('countAbout',{increment:'JIA',decrement:'JIAN'}),
   ```



## :exclamation:路由

1. 理解： 一个路由（route）就是一组映射关系（key - value），多个路由需要路由器（router）进行管理。
2. 前端路由：key是路径，value是组件。

### 1.基本使用

1. 安装vue-router，命令：```npm i vue-router```

2. 应用插件：```Vue.use(VueRouter)```

3. 编写router配置项:

   ```js
   //引入VueRouter
   import VueRouter from 'vue-router'
   //引入Luyou 组件
   import About from '../components/About'
   import Home from '../components/Home'
   
   //创建router实例对象，去管理一组一组的路由规则
   const router = new VueRouter({
   	routes:[
   		{
   			path:'/about',
   			component:About
   		},
   		{
   			path:'/home',
   			component:Home
   		}
   	]
   })
   
   //暴露router
   export default router
   ```

4. 实现切换（active-class可配置高亮样式）

   ```vue
   <router-link active-class="active" to="/about">About</router-link>
   ```

5. 指定展示位置

   ```vue
   <router-view></router-view>
   ```

### 2.几个注意点

1. 路由组件通常存放在```pages```文件夹，一般组件通常存放在```components```文件夹。
2. 通过切换，“隐藏”了的路由组件，默认是被销毁掉的，需要的时候再去挂载。
3. 每个组件都有自己的```$route```属性，里面存储着自己的路由信息。
4. 整个应用只有一个router，可以通过组件的```$router```属性获取到。

### 3.多级路由（多级路由）

1. 配置路由规则，使用children配置项：

   ```js
   routes:[
   	{
   		path:'/about',
   		component:About,
   	},
   	{
   		path:'/home',
   		component:Home,
   		children:[ //通过children配置子级路由
   			{
   				path:'news', //此处一定不要写：/news
   				component:News
   			},
   			{
   				path:'message',//此处一定不要写：/message
   				component:Message
   			}
   		]
   	}
   ]
   ```

2. 跳转（要写完整路径）：

   ```vue
   <router-link to="/home/news">News</router-link>
   ```

### 4.路由的query参数

1. 传递参数

   ```vue
   <!-- 跳转并携带query参数，to的字符串写法 -->
   <router-link :to="/home/message/detail?id=666&title=你好">跳转</router-link>
   				
   <!-- 跳转并携带query参数，to的对象写法 -->
   <router-link 
   	:to="{
   		path:'/home/message/detail',
   		query:{
   		   id:666,
               title:'你好'
   		}
   	}"
   >跳转</router-link>
   ```

2. 接收参数：

   ```js
   $route.query.id
   $route.query.title
   ```

### 5.命名路由

1. 作用：可以简化路由的跳转。

2. 如何使用

   1. 给路由命名：

      ```js
      {
      	path:'/demo',
      	component:Demo,
      	children:[
      		{
      			path:'test',
      			component:Test,
      			children:[
      				{
                            name:'hello' //给路由命名
      					path:'welcome',
      					component:Hello,
      				}
      			]
      		}
      	]
      }
      ```

   2. 简化跳转：

      ```vue
      <!--简化前，需要写完整的路径 -->
      <router-link to="/demo/test/welcome">跳转</router-link>
      
      <!--简化后，直接通过名字跳转 -->
      <router-link :to="{name:'hello'}">跳转</router-link>
      
      <!--简化写法配合传递参数 -->
      <router-link 
      	:to="{
      		name:'hello',
      		query:{
      		   id:666,
                  title:'你好'
      		}
      	}"
      >跳转</router-link>
      ```

### 6.路由的params参数

1. 配置路由，声明接收params参数(`占位符title后面加?表示title不确定是否存在`)

   ```js
   {
   	path:'/home',
   	component:Home,
   	children:[
   		{
   			path:'news',
   			component:News
   		},
   		{
   			component:Message,
   			children:[
   				{
   					name:'xiangqing',
   					path:'detail/:id/:title', //使用占位符声明接收params参数
   					component:Detail
   				}
   			]
   		}
   	]
   }
   ```

2. 传递参数

   ```vue
   <!-- 跳转并携带params参数，to的字符串写法 -->
   <router-link :to="/home/message/detail/666/你好">跳转</router-link>
   				
   <!-- 跳转并携带params参数，to的对象写法 -->
   <router-link 
   	:to="{
   		name:'xiangqing',
   		params:{
   		   id:666,
               title:'你好'
   		}
   	}"
   >跳转</router-link>
   ```

   > 特别注意：路由携带params参数时，若使用to的对象写法，则不能使用path配置项，必须使用name配置！

3. 接收参数：

   ```js
   $route.params.id
   $route.params.title
   ```

### 7.路由的props配置

​	作用：让路由组件更方便的收到参数

```js
{
	name:'xiangqing',
	path:'detail/:id',
	component:Detail,

	//第一种写法：props值为对象，该对象中所有的key-value的组合最终都会通过props传给Detail组件
	// props:{a:900}

	//第二种写法：props值为布尔值，布尔值为true，则把路由收到的所有params参数通过props传给Detail组件
	// props:true
	
	//第三种写法：props值为函数，该函数返回的对象中每一组key-value都会通过props传给Detail组件
	props(route){
		return {
			id:route.query.id,
			title:route.query.title
		}
	}
}
```

### 8.```<router-link>```的replace属性

1. 作用：控制路由跳转时操作浏览器历史记录的模式
2. 浏览器的历史记录有两种写入方式：分别为```push```和```replace```，```push```是追加历史记录，```replace```是替换当前记录。路由跳转时候默认为```push```
3. 如何开启```replace```模式：```<router-link replace .......>News</router-link>```



### 9.编程式路由导航this.$router.push

1. 作用：不借助```<router-link> ```实现路由跳转，让路由跳转更加灵活

2. 具体编码：

   ```js
   //$router的两个API
   this.$router.push({
   	name:'xiangqing',
   		params:{
   			id:xxx,
   			title:xxx
   		}
   })
   
   this.$router.replace({
   	name:'xiangqing',
   		params:{
   			id:xxx,
   			title:xxx
   		}
   })
   this.$router.forward() //前进
   this.$router.back() //后退
   this.$router.go() //可前进也可后退
   ```

### 10.缓存路由组件

1. 作用：让不展示的路由组件保持挂载，不被销毁。

2. 具体编码：

   ```vue
   <keep-alive include="News"> 
       <router-view></router-view>
   </keep-alive>
   ```

### 11.两个新的生命周期钩子

1. 作用：路由组件所独有的两个钩子，用于捕获路由组件的激活状态。
2. 具体名字：
   1. ```activated```路由组件被激活时触发。
   2. ```deactivated```路由组件失活时触发。



### 12.路由守卫

1. 作用：对路由进行权限控制

2. 分类：全局守卫、独享守卫、组件内守卫

3. 全局守卫:

   ```js
   //全局前置守卫：初始化时执行、每次路由切换前执行
   router.beforeEach((to,from,next)=>{
   	console.log('beforeEach',to,from)
   	if(to.meta.isAuth){ //判断当前路由是否需要进行权限控制
   		if(localStorage.getItem('school') === 'atguigu'){ //权限控制的具体规则
   			next() //放行
   		}else{
   			alert('暂无权限查看')
   			// next({name:'guanyu'})
   		}
   	}else{
   		next() //放行
   	}
   })
   
   //全局后置守卫：初始化时执行、每次路由切换后执行
   router.afterEach((to,from)=>{
   	console.log('afterEach',to,from)
   	if(to.meta.title){ 
   		document.title = to.meta.title //修改网页的title
   	}else{
   		document.title = 'vue_test'
   	}
   })
   ```

4. 独享守卫:

   ```js
   beforeEnter(to,from,next){
   	console.log('beforeEnter',to,from)
   	if(to.meta.isAuth){ //判断当前路由是否需要进行权限控制
   		if(localStorage.getItem('school') === 'atguigu'){
   			next()
   		}else{
   			alert('暂无权限查看')
   			// next({name:'guanyu'})
   		}
   	}else{
   		next()
   	}
   }
   ```

5. 组件内守卫：

   ```js
   //进入守卫：通过路由规则，进入该组件时被调用
   beforeRouteEnter (to, from, next) {
   },
   //离开守卫：通过路由规则，离开该组件时被调用
   beforeRouteLeave (to, from, next) {
   }
   ```

### 13.路由器的两种工作模式



1. 对于一个url来说，什么是hash值？—— #及其后面的内容就是hash值。

2. hash值不会包含在 HTTP 请求中，即：hash值不会带给服务器。

3. hash模式：

   1. 地址中永远带着#号，不美观 。
   2. 若以后将地址通过第三方手机app分享，若app校验严格，则地址会被标记为不合法。
   3. 兼容性较好。

4. history模式：

   1. 地址干净，美观 。

   2. 兼容性和hash模式相比略差。

   3. 应用部署上线时需要后端人员支持，解决刷新页面服务端404的问题。

      ​													 ![image-20220718204937594](.\picture\image-20220718204937594.png)

      ![image-20220718205003015](.\picture\image-20220718205003015.png)


![image-20220718204922934](.\picture\image-20220718204922934.png)

![image-20220718205037468](.\picture\image-20220718205037468.png)

![image-20220718205054977](.\picture\image-20220718205054977.png)

![image-20220718204753781](.\picture\image-20220718204753781.png)





## :star:组件库

![image-20220718205150175](.\picture\image-20220718205150175.png)
