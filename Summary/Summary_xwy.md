# 前端开发总结

>Author: 徐伟元
>Date: 2018-12-16

## 简述

在这个项目里，我和熊永琦负责的是前端，其中，我主要写页面(**登陆/API/修改/gitpage**)，熊永琦主要写逻辑。

经过考量，这次的主体框架为 **Vue** 。因为没有美工设计，所以 UI 使用的是 **Element-UI** ，基于 Vue 的前端 UI 框架。同时，使用 **axios** 替代了 JQuery。

这次的开发，较为粗浅地学习了 Vue，就用原本就不多的开发经验，来稍微聊聊对 Vue 的认知和开发中的考虑。

目录如下：
<!-- TOC -->
- [Vue](#vue)
- [SPA ? MPA ?](#spa--mpa-)
- [Why not JQuery](#why-not-jquery)
<!-- /TOC -->

## Vue

Vue 作为国人开发的一款前端框架，近来的火热程度是越来越高。相比有名的 react 和 angular，也是不遑多让。它如此受欢迎的原因也很明显：简单，高效，而且优雅(我的个人感觉2333)。

为什么简单？他的数据驱动，只要是入了门的，都可以很简单的书写，同时是类似 python，go 编程习惯的循环写法，对于后端来说，也是一眼就看明白了；他的 Vue 实例，采用类面向对象的思想，让你将不同的内容，分门别类的写在不同的地方，data / methods... *在学习的时候，甚至都半开玩笑，这是为后端同学快速上手前端而开发的框架吧*。

它的高效，可以看看官方教程中与其他框架的[对比](https://cn.vuejs.org/v2/guide/comparison.html)，这是一个在综合性能方面不输其他框架的新框架。

至于优雅，这就是见仁见智了。对我而言，我觉得它是优雅的，因为 Vue 让人更少的关注于 html 本身的编写，而是让人用真正编程的思想去看待它。比如同类数据，使用 `v-for` 绑定；不同情况使用 `v-if` 区分。最棒的是，它的监听结构，绑定数据的页面，会在数据变动时，实时变动，完全没有必要刷新页面！

## SPA ? MPA ?

到这里，相信会 Vue 的，或者涉猎过 Vue 的人，都看过[官方教程](https://cn.vuejs.org/v2/guide/)了。里面说得 Vue 都是它的好处，而且教会了你一个很新奇的东西：单文件组件，也就是 `.Vue` 文件。一开始接触这个是会觉得很奇怪的，不是前端开发吗？不写 html，写 Vue 就好了？其实不然，这个单文件组件，就是把你的页面，切分成小块，每一个块是一个组件，而且数据分离，逻辑分离，html 结构分离。比如一个登陆页面，我们可以分成 3 个部分：顶部标题栏，底部标题栏和中间的登陆表单。我们编写 3 个 .Vue 文件分别对应这三个部分，然后在主页面中引入这三个组件，并写在 html 中就好了。

你会问了，为什么要这么麻烦？这其实是很好的一个做法。因为，我们一个 WEB 应用，肯定不止一个登陆页面，假设我们有5个页面，每个页面的顶部栏，底部栏都是风格统一的(一个应用嘛)，那么我们把这写 html 和 js 重复写 5 遍吗？这是不可能的。

所以，这个单文件组件的价值就体现出来了。将页面切分组件，每次关注一个组件，完成所有的页面代码，最后拼接在一起就好了。

是啊，多好的东西啊。接着你可以去看看我们的[前端项目](https://github.com/S-Vanguard/StarWar_Client)，然后你会回来说：你说了半天单文件组件的好处，为什么你一个 .Vue 文件都没有？原因很简单：**速度**。

这个单文件组件，需要你使用 Vue-cli 脚手架搭建你的前端项目，这样子你写的 .Vue 文件才会被脚手架 build 的时候绑进去。而至于这个脚手架干了什么呢？它干了一件很常见的事情：webpack 打包。最终，你的项目会是一个 **SPA**。SPA 比 MPA 不好吗？也不能说不好，各有优缺点。但在我看来，它对于初始的用户响应来说，速度太慢([Vue 的 SPA 和 MPA 渲染速度对比](https://www.cnblogs.com/tiedaweishao/p/6644267.html))，用户体验不好。

至于 SPA 和 MPA 的区别，比较明显的还有一点：路由的管理。SPA 需要前端实现路由，因为后端基本只负责传递数据(真的就是数据，而不是页面，这也是 Vue-cli 脚手架工程配合其他后台的基本思想)，而 MPA 由后台来实现路由，前端只负责页面逻辑，路由匹配是后端完成的。

所以，在这里，我选择了 MPA。那如何让 MPA 也能保留 Vue 的单文件组件的思想呢？官方给出了[方案](https://cn.vuejs.org/v2/guide/components.html)。我们在 JS 中给 Vue 实例全局设定组件即可(*具体的例子可以参考我在项目中的 [global.js](https://github.com/S-Vanguard/StarWar_Client/blob/master/js/global.js)*)。这个方案唯一的缺点就是，相比单文件组件的 .Vue 文件，将 html，js，css 合并在一个文件中，我们只能完成 html 和 js 的组件定义，至于 css，只能使用 css 文件了。

## 总结

了解新技术是一个不断学习的过程，学习新技术(Vue, axios)的优点，旧技术的不足([JQuery 为何逐渐被抛弃](https://blog.csdn.net/csdnnews/article/details/81256798))。
