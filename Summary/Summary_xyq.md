# StarWar 项目小结

|项目名称|成员姓名|成员学号|
|-|-|-|
|简单 web 服务与客户端开发实战|熊永琦|16340258|

## 简述

在这个项目里，我（[@siskonemilia](https://github.com/siskonemilia)）和徐伟元（[@xwy27](https://github.com/xwy27)）同学负责前端的编写。其中，我主要负责写前端逻辑，也负责 API 展示界面代码的编写和 API 的设计，并参与了全局视觉效果的构建。

在查阅了一些文档后，我们确认使用 **Axios** 代替 jQuery 作为与后端进行 AJAX 交互的工具，并且将 JSON 渲染作为账户权限控制的功能。

## API 设计

本项目 API 参考 Restful 设计标准进行构建（为了确保服务端数据服务的安全性，我们弃用了 DELETE 和 PUT 方法，这两种方法可能被黑客用来）。对于敏感数据的提交，改变服务器状态的请求，我们使用 POST 方法，而对于不改变服务器状态的只读的请求，或是不涉及敏感数据的提交，我们使用 GET 方法。同时，在命名上，我们将不同类别的操作分离，从而实现了较好的 API 可读性。

[API 设计参考](https://github.com/S-Vanguard/StarWar_Client/blob/master/doc/API_design.md)

## Axios with Vue.js：jQuery 的优秀替代者

在 2018 年的今天，jQuery 陈旧的样式，死板的语法和古老的架构显得与各种现代框架格格不入。因而在本项目中，我们使用 [Axios](https://github.com/axios/axios) 替代 jQuery 进行与服务端的 AJAX 交互。

Axios 相对于 jQuery 的优势在哪里呢？首先，其支持 **在 ECMAScript 7 中引入的 Promise 语法**，这种语法能够很好地规避 JavaScript 中的「回调地狱」，使得代码更加清新易读。同时，Axios 还支持对于 JSON 的全自动解析，这使得我们不必去考虑繁杂的 JSON 解析和错误处理，Axios 会帮我们把这些都处理妥当！

那么 jQuery 的 DOM 操作该怎么替代呢？Github 给出的答案是原生的 JavaScript DOM 操作。不过在本项目中，我们的更好的选择是完全通过 Vue.js 来进行 DOM 操作。通过数据绑定和条件渲染，我们就可以实现几乎所有我们想要的渲染效果变更。

## 如何优雅地渲染一个 JSON

在本项目中，没有登陆的用户只能够查看通过 `JSON.stringlify` 渲染的 plain text 版本的 JSON 数据，而登录用户需要能够查看渲染为可视化组件的数据。在查阅了 Element-UI 的组件文档后，我们确认使用可折叠的表格作为承载的组件。

在用户进入展示页面时，我们通过 API 获取当前登录状态，如果正常登录，我们就对获取到的 API 进行渲染。当用户尝试通过 API 获取 JSON 后，我们就会将其转换为一个 JSON 数组，并且将其设置为 `el-table` 的数据源，然后通过我们预先设计的模版，它就可以渲染为一个美观的表格，并且支持伸缩交互的特性。