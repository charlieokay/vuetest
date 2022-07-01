学习前面：

1.想让Vue工作，就*必须创建一个Vue实例，且要传入一个配置对象*;
2.root容器里的代码依然符合html规范，只不过混入了一些特殊的Vue语法;
3.root容器里的代码被称为【Vue模板】;
4. Vue实例和容器是**一一对应**的; 
5. 真实开发中**只有一个Vue实例**，**并且会配合着组件一起使用;**
6.**{{xxx}}中的xxx要写js表达式**，且xxx可以自动读取到data中的所有属性;
7.一旦data中的数据发生改变，那么模板中用到该数据的地方也会自动更新; 
    **注意区分:js表达式和js代码(语句)**

# 1.表达式:一个表达式会产生一个值，可以放在任何一个需要值的地方:
(1). a
(2). a+b
(3). demo(1)
(4). x === y ? 'a' : 'b'

2.js代码(语句)
(1). if (){  }
(2). for (){  }


# 2.模板语法 （Vue模板语法有2大类:）

1.**插值语法** {{ }}
功能:用于解析*标签体内容*。
写法:{{xxx}}，xxx是js表达式，且可以直接读取到data中的所有属性。

2.**指令语法**    v-bind：、v-on：、v-model：
功能:用于*解析标签*（包括:标签属性、标签体内容、绑定事件.....) 。
举例:v-bind :href="xxx”或简写为 :href="xxx"，xxx同样要写js表达式,且可以直接读取到data中的所有属性。
**备注: Vue中有很多的指令，且形式都是: v-????，此处我们只是拿v-bind举个例子。**

# 模板语法
v-html

v-if

v-once

v-bind   -----  :

v-on     -----  @

v-model

v-for

# 3.数据绑定 （单向、双向数据绑定）
       <div>
            <h2>{{info}}</h2>
            <input type="text" v-bind:value="info" />
            <button type="button">单向添加</button>
            <br />
            <br />
            <input type="text" v-model:value="info" />
            <button type="button">双向添加</button>
       </div>
       
Vue中有2种数据绑定的方式:
1.**单向绑定**(v-bind):数据只能从data流向页面。
2.**双向绑定**(v-model):数据不仅能从data流向页面，还可以从页面流向data.
备注:
1.双向绑定一般都应用在**表单类元素**(*或者输入类元素*)上(如: **input、select**等)
2.v-model:value 可以简写为v-model，因为v-model默认收集的就是value值。


# 4.el和data的两种写法
```html

<div id="root">
  容器
</div>

var x = new Vue({
            el: "#root",
            data: {
                msg: "hello vue",
                info: "hello victor",
                age: 24,
                url: "***********",
                other: {
                    name: "pic",
                    age: 23,
                },
            },
            // data: function() {
            //     return {
            //         name: "victor"
            //     };
            // },
        });
        
        //v.$mount('#root');
        
```

# ****1.el有2种写法****
(1).new Vue时候配置el属性。 *(el: "#root")*,
(2).先创建Vue实例，随后再通过*v. $mount( ' #root ')*指定el的值。

****2.data有2种写法****
(1).对象式
data: {
                msg: "hello vue",
                info: "hello victor",
                age: 24,
                url: "************",
                other: {
                    name: "pic",
                    age: 23,
                },
            },
(2).函数式
data: function() {
              return {
                 name: "victor"
               };
            },
如何选择:目前哪种写法都可树,**以后学习到组件时，data必须使用函数式，否则会报错**。

****3.一个重要的原则:****
由Vue管理的函数，一定不要写箭头函数，一旦写了箭头函数，this就不再是Vue实例了。

# 5.MVVM模型
**MVVM是Model-View-ViewModel的简写**。它本质上就是MVC 的改进版。MVVM 就是将其中的View 的状态和行为抽象化，让我们将视图 UI 和业务逻辑分开。当然这些事 ViewModel 已经帮我们做了，它可以取出 Model 的数据同时帮忙处理 View 中由于需要展示内容而涉及的业务逻辑。

MVVM模型
1.M:模型(Model) : data中的数据
2. V:视图(View):模板代码
3.VM:视图模型(ViewModel)

Vue实例观察发现:
1.data中**所有的属性,**最后都出现在了vm身上。
2.vm身上所有的属性及 Vue原型上所有属性，在Vue模板中都可以直接使用。


# 6.Object.defineProperty方法
 let = person{
            name:'victor'，
            address;'上海'，
            *//age:24,*
}

 Object.defineProperty(person,'**age**',{
             **value:18，**
             enumerable:true,//控制属性是否可以枚举（遍历）

get(){

}

set(){

}
        })

1.Vue中的数据代理
   通过vm对象来代理data对象中属性的操作（读/写)
2.Vue中数据代理的好处
更加方便的操作data中的数据
3.基本原理
   通过object.defineProperty()把data对象中所有属性添加到vm上.为每一个添加到vm上的属性，都指     定一个getter/setter.
  在getter/setter内部去操作（读/写)data中对应的属性。


# 6.事件处理
**事件的基本使用:**
1.使用v-on :xxx或@xxx绑定事件,其中xxx是事件名;
2.事件的回调需要配置在methods对象中，最终会在vm上;
3.methods中配置的函数，*不要用箭头函数! 否则this就不是vm了*;
4.methods中配置的函数，都是被Vue所管理的函数，this的指向是vm或组件实例对象;
5.@click="demo”和@click="demo($event)”效果一致，但后者可以传参;

# 7.事件修饰符
**.stop
.prevent
.capture
.self
.once
.passive**

## computed watch methods

## 计算属性:
1.定义:要用的属性不存在,要通过已有属性计算得来。当所依赖的内容发生变化时，才会重新执行计算。
2.原理:底层借助了0bjcet.defineproperty方法提供的getter和setter.
3.get函数什么时候执行?
    (1).初次读取时会执行一次。
    (2).当依赖的数据发生改变时会被再次调用。
4.优势:与methods实现相比，内部有缓存机制（复用），效率更高，调试方便。
5.备注:
    1.计算属性最终会出现在vm上，直接读取使用即可。
    2.如果计算属性要被修改，那必须写set函数去响应修改，且set中要引起计算时依赖的数据发生t

# 侦听器和计算属性：watch  对比 computed    建议使用 计算属性
1.computed能完成的功能,watch都可以完成。
2.watch能完成的功能，computed不一定能完成，例如: **watch可以进行异步操作**。
# computed 和 methods 
计算属性和方法函数比较：若两者均可以，建议采用计算属性。因为有缓存机制




# 两个重要的小原则:
1.所被*Vue管理的函数，最好写成普通函数*，这样this的指向才是vm或组件实例对象
2.所有*不被Vue所管理的函数（定时器的回调函数、ajax的回调函数等)，最好写成箭头函数*，这样this的指向才是vm 或组件实例对象。

# 监视属性
    

















