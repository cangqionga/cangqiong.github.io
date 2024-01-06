Vue-router学习
一、开启我们的第一个项目
我们在上篇文章就已经学到，如何利用脚手架开启一个vue项目了，今天，我们就通过vite开启我们项目来学习vue-router
如果你不知道如何开启一个项目可以看看：[vue]学习使用vite和cli脚手架开启你自己的vue项目！ - 掘金 (juejin.cn)
选择使用vite开始项目！安装完项目之后就可以开始我们的学习啦!注意，大家可以先把项目默认的内容清除哦！
二、学习vue-router的使用
当我们需要完成SPA开发(单页面应用开发)的时候，就不得不说一下vue-router了！
简单的意思就是，当我们需要在一个页面实现多个页面的转换，而不经过跳转的开发模式，也就是让多个页面在一个页面中实现！
1、为你的项目安装路由
首先第一步，我们需要为我们的项目安装路由的依赖，使用npm install vue-router@4安装路由！
使用VS code进入到项目目录下，打开终端输入npm install vue-router@4

安装成功之后，开始我们接下来的操作！
2、为全局配置好路由
首先，在我们的src目录下新建一个文件夹router，在文件夹下面新建一个index.js文件，（其实名字都是自己取的，到时候导入的时候把名字写对就行。）
接下来，我们要配置我们的index.js文件，这里我们先导入import {createWebHistory,createRouter} from 'vue-router'这里涉及到了vue路由的两种模式，我们会在后面解析路由原理中讲到！
js复制代码import { createWebHashHistory,createRouter, createWebHistory } from "vue-router";//导入

//这里用于存放我们的vue-router组件
const routes = [

]
//这里用于创建一个路由
const router = createRouter({
    history:createWebHistory(),//这里有两种模式，我们选择的是history模式还有一种hash模式
    routes:routes//引入我们的组件数组
}
)

export default router//抛出我们的路由

这里主要分为四个步骤

第一步：导入相对性的包
第二步：配置我们的路由组件
第三步：创建一个路由，设定路由模式，引用我们的组件
第四步：将我们的路由默认抛出（要想别的组件能够引用我们的路由，我们就得将这个路由抛出）

接下来，我们要配置main.js文件，这里是我们整个项目配置地方
我们需要将我们建立的组件应用到整个页面当中！我们这样做！
js复制代码import { createApp } from 'vue'
import App from './App.vue'
import router from './router/index.js'

createApp(App)
.use(router)
.mount('#app')

好啦！这样我们整个配置就基本上配置好了，接下来就可以开始编写我们的路由了！
3、编写路由页面
首先，我们假设一个场景，在页面上，我们需要一个首页和一个名单，点击首页会显示一些东西，点击名单会显示一些名单，同时，页面不会发生跳转，且首页和名单这两个标签不会消失，实现在页面内进行改变！
那我们就从App.vue开始(其实更加推荐的是所有的页面都使用不同的组件，而App.vue只需要负责配置这些页面即可，这里是方便大家学习，我们这样做！)
App.vue
vue复制代码<script setup>
</script>

<template>
  <div>
    <router-link to="/home">首页</router-link>|
    <router-link to="/list">名单</router-link>
  </div>
  <router-view></router-view>
</template>

<style scoped>
*{SS
  text-align: center;
  font-size: 40px;
}
</style>

我们可以看到，在整个App.vue当中我们有两个新的标签<router-link to=""></router-link>和<router-view></router-view>
给大家介绍一下：
<router-link to="">这个标签，其实就是相当于一个a标签，通过点击我们进行相应的url地址，而to则表示我们要到达的地址！
<router-view>这个相当于一个入口，代表我们路由的入口，也就是说，路由中的内容会这个标签所在的DOM结构位置出现！
这里，我们就可以看到页面效果了！

我们点击首页对应的地址会变为：http://localhost:5173/home
点击名单对应的地址会变为：http://localhost:5173/list
接下来，我们就要取实现这样两个页面
基本配置+Home.vue
我们可以在src目录下新建一个文件夹，用于存放不同的页面（当然你也可以不必如此），在新建一个Home.vue文件
vue复制代码<template>
    <div>
        <ul>
            <h1>这里是首页</h1>
            <h2>这里是首页</h2>
            <h3>这里是首页</h3>
            <h4>这里是首页</h4>
        </ul>
    </div>
</template>

好，这么页面我们就简单写成这样，那你会疑问，页面上还是没有这个啊，不着急，我们需要配置一下！来到router文件夹下的index.js文件
js复制代码import home from '../views/Home.vue'

const routes = [
    {
        path:'/home',
        component: home
    }
]

在index.js文件中，我们将刚刚编写的Home.vue文件导入进来，用home来表示它
接下来就需要在routes路由页面当中进行配置，数组里面存放一个又一个的对象，表示不同的页面。
添加一个对象到数组中，这个对象有两部分：
path表示路由路径--当然要于你链接的路径一致，也就是<router-link to=''>中to的目标地址一致
component表示路由组件--表示要使用的组件是哪一个，也就是要使用的页面是哪一个文件
配置好之后，我们再点击首页：

这样，我们的效果就实现啦！！
同样的，我再写一个名单界面
子路由+List.vue
同样是在views文件下新建一个文件List.vue
vue复制代码<template>
    <div>
        <!-- 子路由 -->
        <router-link to="/list/yanyan">大肥羊</router-link>|
        <router-link to="/list/xiongxiong">狗熊岭</router-link>
        <router-view></router-view>
    </div>
</template>

这里我们将用到子路由！可以看到我们使用同样的原理新建了两个<router-link>
注意，子路由的地址一定要填写完整，不能写成to='/yanyan'这种，要加上父路径的地址to='/list/yanyan'
接下来，我们可以在views文件中在新建一个文件夹children，再在这个文件下新建两个文件yanyan.vue和xiongxiong.vue
yanyan.vue
vue复制代码<template>
    <div>
        <ul>
            <h4>喜羊羊</h4>
            <h4>沸羊羊</h4>
            <h4>美羊羊</h4>
            <h4>懒羊羊</h4>
            <h4>慢羊羊</h4>
        </ul>
    </div>
</template>

xiongxiong.vue
vue复制代码<template>
    <div>
        <ul>
            <h4>熊大</h4>
            <h4>熊二</h4>
            <h4>李老板</h4>
            <h4>光头强</h4>
            <h4>吉吉</h4>
        </ul>
    </div>
</template>

接下来，我们要做的就是配置好路由文件下的index.js文件
按照上一步操作
js复制代码import { createWebHashHistory,createRouter, createWebHistory } from "vue-router";
import home from '../views/Home.vue'
import list from '../views/List.vue'
const routes = [
    {
        path:'/home',
        component: home
    },
    {
        path:'/list',
        component:list
    }
]

我们先将List.vue引入到页面当中！这样，我们再点击名单时就会出现：

接下来，如何配置子路由呢？
同样导入子路由先
我们需要在对应父路由下加入一个children属性，也是存放一个数组，数组里面存放对象用于展示不同的页面
这样我们的配置文件会写成这样：
js复制代码import { createWebHashHistory,createRouter, createWebHistory } from "vue-router";
import home from '../views/Home.vue'
import list from '../views/List.vue'
import yanyan from '../views/children/yanyan.vue'


const routes = [
    {
        path:'/home',
        component: home
    },
    {
        path:'/list',
        component:list,
        children:[
            {
                path:'yanyan',
                component:yanyan
            },
            {
                path:'/list/xiongxiong',
                component:()=>import('../views/children/xiongxiong.vue')
            }
        ]
    }
]

先介绍导入部分：我们可以使用两种导入方式
​	第一种是在头部直接导入：
import yanyan from'../views/children/yanyan.vue'
​	第二种是在component属性中导入:
component:()=>import('../views/children/xiongxiong.vue')
同样的，我们首先配置好了list的路由之后，添加了一个属性children，以同样的方式，用数组存储对象配置子路由！
在配置子路由的路径时，也有两种方式：
​				第一种是不要加/,直接写path:'yanyan'
​				第二种是加/,但是要把路径写完整path:'/list/xiongxiong'
这样我们的效果就实现啦！

重定向
不知道大家有没有发现，当我们进入页面或者名单当中，一开始那些内容是不显示的，而是要通过我们点击才会显示！万一以后你要写项目，页面上一开始空空如也多不美观？比如你想要让页面默认显示内容的时候，我们就要使用重定向了！！
如何使用重定向，我们就需要在父级路由当中再添加一个对象，用于重定向，比如我们要让页面默认显示首页的内容,我们要这样做！
js复制代码const routes = [
    //这里是重定向！
    {
        path:'',
        redirect:'/home'
    },
    {
        path:'/home',
        component: home
    },
    {
        path:'/list',
        component:list,
        children:[
            {
                path:'yanyan',
                component:yanyan
            },
            {
                path:'/list/xiongxiong',
                component:()=>import('../views/children/xiongxiong.vue')
            }
        ]
    }
]

可以看到，我们又添加了一个对象，其中有两个属性path和redirect，path对应的是当前的URL地址，而redirect表示你要重定向的地址也就是你要展示的页面,这样当我们每次进入页面当中，都会默认显示首页中的内容。
同理！在名单页面当中，如果我们要默认显示yanyan.vue中的内容,我们也只需要在yanyan.vue的父路由中添加一个重定向！
js复制代码{
    path:'/list',
    component:list,
    children:[
        {
            path:'/list',
            redirect:'/list/yanyan'
        },
        {
            path:'yanyan',
            component:yanyan
        },
        {
            path:'/list/xiongxiong',
            component:()=>import('../views/children/xiongxiong.vue')
        }
    ]
}

看看效果吧！

三、如果你不会清空项目，请看这里
安装成功后，项目会自动为我们按照一部分的基本结构和样式等等，我们将项目中自动生成的，不需要的部分删除掉！
1、从main.js开始

将图中这行删除！
2、清空App.vue

我们将App.vue中的元素删除成如图，只有基本结构即可！
3、删除文件
将如图的文件都删除掉，我们的项目基本上就干净啦！


作者：Aidan路修远i
链接：https://juejin.cn/post/7320655354429063205
来源：稀土掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
