# 公司前端介绍

**公司使用Ember Js作为前后端分离的前端主体框架，在这个框架中我们进行业务开发，为了你能更快的适应上手，下面我来介绍下在原有的架构中咱们公司用到了哪些插件或工具。**

1. [操作系统](gong-si-qian-duan-jie-shao.md#cao-zuo-xi-tong)
2. [Node.js](gong-si-qian-duan-jie-shao.md#node-js)
3. [Yarn](gong-si-qian-duan-jie-shao.md#yarn)
4. [ember-bootstrap](gong-si-qian-duan-jie-shao.md#ember-bootstrap)
5. [sass](gong-si-qian-duan-jie-shao.md#sass)
6. [ember-echarts](gong-si-qian-duan-jie-shao.md#ember-echarts)
7. [ember-mirage](gong-si-qian-duan-jie-shao.md#ember-mirage)
8. [ember-cookies](gong-si-qian-duan-jie-shao.md#ember-cookies)
9. [css-modules](gong-si-qian-duan-jie-shao.md#ember-css-modules)
10. [file-upload](gong-si-qian-duan-jie-shao.md#ember-file-upload)
11. [models-table](gong-si-qian-duan-jie-shao.md#ember-models-table)
12. [postcss](gong-si-qian-duan-jie-shao.md#postcss)
13. [postcss-import](gong-si-qian-duan-jie-shao.md#postcss-import)

### 操作系统

> 公司开发部门，所有的开发人员前端也好后端也好都是Linux或者Mac操作系统，选择Linux的原因是
>
> 1. 相对于Windows稳定很多，与线上部署环境接近
> 2. 环境搭建简单无繁琐配置项
> 3. 字符集问题
> 4. 程序员就不应该使用WIndows（除了娱乐）



### Node.js

> [传送门 -&gt; Node.js](https://nodejs.org/en/)

> Node.js他不是一个js应用，而是js运行平台。
>
> Node.js采用C++语言编写而成，是一个Javascript的运行环境。
>
> 为什么采用C++语言呢？据Node.js创始人Ryan Dahl说，最初希望采用Ruby来写Node.js，但是后来发现Ruby虚拟机的性能不能满足他的要求，后来他尝试采用V8引擎，所以选择了C++语言。（万佛之宗）
>
> 既然不是Javascript应用，为何叫.js呢？
>
> 这是因为Node.js是一个Javascript的运行环境，提到Javascript，大家首先想到的是日常使用的浏览器，现代浏览器包含了各种组件，包括渲染引擎、Javascript引擎等，其中Javascript引擎负责解释执行网页中的Javascript代码，作为Web前端最重要的语言之一，Javascript一直是前端工程师的专利。
>
> Node.js是一个后端的Javascript运行环境，这意味着你可以编写系统级或者服务器端的Javascript代码，交给Node.js来解释执行。
>
> 更多的信息点击传送门去官网了解

### Yarn

> 进入Yarn的官网就会看到这几个字，快速、可靠和安全的依赖管理工具
>
> 快速：Yarn的下载他会缓存每个包，再次下载时会先到本地找，无需重复下载，而且还能并行化操作最大化利用系统资源，提升效率
>
> 安全：Yarn每次安装时都会校验查看文件是否完整
>
> 安全可靠：Yarn 使用详细、简介的 lockfile文件（就是json文件） 和确定性算法来安装依赖，能够保证在一个系统上的运行的安装过程也会以同样的方式运行在其他系统上。
>
> 具体去上一章找传送门

### Ember-Bootstrap

> Bootstrap都知道，来自Twitter，是目前市面上排名前几的UI层面的前端框架。
>
> 那Ember中对于引用Bootstrap来说是一件比较繁琐的事情，所以就有了Ember-Bootstrap这个Addons。
>
> 用法与原生的少许不同，相信你很快就会适应的。
>
> [传送门](https://www.ember-bootstrap.com/)

### Sass

### Ember-Echarts

### Ember-Mirage

### Ember-Cookies

### Ember-Css-Modules

### Ember-File-Upload

### Ember-Models-Table

### Postcss

### Postcss-Import

