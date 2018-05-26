---
description: 本章主要讲解Ember框架中非常重要的组成部分路由
---

# Ember 中的路由器

当我们在开发Web应用程序的时候，我们无时无刻的都在思考着一些特定的问题，比如说：

1. 当前页面显示的是什么
2. 当用户点击了页面的某个连接将会跳转到那里
3. 某些事件发生的时候因为业务逻辑的关系，页面的显示将会发生变化等

类似这样的问题我们都会称之为 **应用程序的状态**，对于前端开发而言，应用程序的状态绝大部分都是通过url来表现的。

url本是可以通过很多方式来改变比如：

1. 用户可以在地址栏里面输入或粘贴进入应用程序
2. 通过浏览器的前进后退键来改变
3. 通过点击链接改变
4. 通过应用程序中内部的一些逻辑进行跳转改变

那路由在这里扮演的角色就是一个“连接器“，我们可以创建若干个路由，每个路由都映射一个url，当地址栏的url改变到它的时候，那对应的路由就会去接手来进行下面的工作 。

路由它所要承担的职责通常会包含以下几个：

1. 渲染模板
2. 提供数据
3. 跳转路由

1. 当进入路由时，会将绑定的模板直接渲染到页面上，这里的模板你就可以直接认为是HTML。

2. 路由会提供模板所需要的数据，可以使ajax也可以是其他方式的

3. 比如没有登入的人是不可以进入到系统中，那这个时候就会跳转到其他路由上来去处理这件事情

在Web开发中，路由扮演者很重要的角色，它看上去不是那么的显眼，但却在整个系统中是重要的一环，视图与数据路由更是有承上启下的作用。

**在Ember中Application 是整个应用程序的最顶层，这一点要记好**，每个路由下都会有个默认的Index路由，这点等到了实际项目中通过调试工具你会看见。

## 定义路由

{% code-tabs %}
{% code-tabs-item title="创建路由命令" %}
```bash
ember g route my-first-route
```
{% endcode-tabs-item %}
{% endcode-tabs %}

然后他就会在app/routes/生成一个my-first-route.js 路径是 **app/routes/my-first-route.js**，同时也会生成一个template文件 路径是 **app/templates/my-first-route.hbs**和一个test文件 路径是 **tests/unit/routes/route-name-test.js。**

这里有个小技巧，就是在执行Ember命令时在后面加个-d 就可以看到模拟执行的效果。

这时打开app/router.js文件，你会发现刚才定义的路由已经在这个文件里面了

{% code-tabs %}
{% code-tabs-item title="app/router.js" %}
```javascript
Route.map(function() {
    this.route('my-first-route')
})
```
{% endcode-tabs-item %}
{% endcode-tabs %}

当然如果你很有自信并且对Ember无比的熟悉，你也可以手动在map里面去写路由，然后在对应的地方创建其他依赖。

现在你想访问刚创建的路由，url是这个样子滴 http://localhost:4200/my-first-route，那如果想把把my-first-route换掉，但同时也要访问刚才的模板怎么办？你可以这样写

{% code-tabs %}
{% code-tabs-item title="app/router.js" %}
```javascript
Route.map(function() {
    this.route('my-first-route', {path: 'hiEmber'})
})
```
{% endcode-tabs-item %}
{% endcode-tabs %}

