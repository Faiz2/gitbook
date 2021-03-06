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
    this.route('my-first-route', {path: '/hiEmber'})
})
```
{% endcode-tabs-item %}
{% endcode-tabs %}

这个时候你的访问样子就变成了，http://localhost:4200/hiEmber ，这是因为path这个参数设置的是url进来时的一个标志，符合这个标志的就会进行渲染，这个时候你就会发现url变了，但是渲染的内容却没有改变。

## 定义子路由

{% code-tabs %}
{% code-tabs-item title="创建子路由命令" %}
```bash
ember g route my-first-route/child
```
{% endcode-tabs-item %}
{% endcode-tabs %}

相对应的router.js文件是这个样子滴

{% code-tabs %}
{% code-tabs-item title="app/router.js" %}
```javascript
Route.map(function() {
    this.route('my-first-route', {path: 'hiEmber'}, function(){
        this.route('child')
    })
})
```
{% endcode-tabs-item %}
{% endcode-tabs %}

这个时候你访问应该是 http://localhost:4200/hiEmber/child

每个路由下面都会有个index的子路由，这部分工作由Ember帮我们完成了，其实完整的应该是这个样子的

{% code-tabs %}
{% code-tabs-item title="app/router.js" %}
```javascript
Route.map(function() {
    this.route('my-first-route', {path: 'hiEmber'}, function(){
        this.route('index', {path: '/'});
        this.route('child');
    })
})
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## 创建动态路由

动态路由是指，在访问url时，url后的参数会变动的，比如我们在看博客时，每点击一个博客上面的url就会相应的变动。

相对应的router.js文件是这个样子滴

{% code-tabs %}
{% code-tabs-item title="app/router.js" %}
```javascript
Route.map(function() {
    this.route('my-first-route', {path: 'hiEmber:id'}, function(){
        this.route('index', {path: '/'});
        this.route('child');
    })
})
```
{% endcode-tabs-item %}
{% endcode-tabs %}

那访问的地址将会变成  http://localhost:4200/hiEmber/165142116510/child

## 第一部分总结

上面只是些对url的控制，还算很简单，只要搞清楚层级关系应该都没什么么问题，所以加油吧！

## 路由中获取模型数据

如何在页面渲染的时候给出数据呢？那以前的做法大部分都是在load的时候去发送一个ajax请求数据，返回response把数据填充到dom中。

现在到了Ember中有一丢丢的类似，只不过把load换成了model hook，数据渲染变成了模板渲染。

下面我将着重介绍比较重要的部分。

### model hook

model是钩子函数，大部分经过路由的数据渲染都是从model这个hook来执行的，当这个钩子触发时，就已经确定了数据要往哪个模板进行渲染，只需要把数据访问逻辑写好就没什么问题了，下面是示例code

{% code-tabs %}
{% code-tabs-item title="model.js" %}
```javascript
import Route from '@ember/routing/route';

export default Route.extend({
    model() {
        return [
            {
                id: 1,
                name: '张三'
            },
            {
                id: 2,
                name: '李四'    
            }
        ]
    }
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="model.hbs" %}
```markup
<div>
    <ul>
        {{#each model as |item| }}
            <li>{{item.name}}</li>
        {{/each}}
    </ul>
</div>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

#### 代码解释

访问mode路由后，该路由model hook被触发  返回数据视图进行渲染，视图层通过each进行循环，把从model出来的数据渲染到视图的ul下。

上面的例子是手动设置假数据，下面会有ajax进行请求模拟真实场景的code

{% code-tabs %}
{% code-tabs-item title="model.js" %}
```javascript
import Route from '@ember/routing/route';
import { inject } from '@ember/service';

export default Route.extend({
    ajax: inject(),
    model() {
        return this.get('ajax').request('/api/search')
    }
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

{% code-tabs %}
{% code-tabs-item title="model.hbs" %}
```markup
<div>
    <ul>
        {{#each model as |item| }}
            <li>{{item.name}}</li>
        {{/each}}
    </ul>
</div>
```
{% endcode-tabs-item %}
{% endcode-tabs %}

#### 代码解释

上面的code中用到了 inject，Ember中有service的概念也有依赖注入的概念，具体的你们可自行Google来查询，Ember重新写了jQuery的ajax的Function，让其更加符合Promise/A+规范，当然jQuery在3.0后已经完全符合Promise/A+规范了，在这里用inject的意思是，因为Ember中把ajax注册成了service，那使用时就应该用依赖注入的形式来使用来减少代码的污染与耦合，ajax对象里实现了request、post、put等函数。

### 动态model hook

动态的model hook以刚才讲的没啥太大的区别，简单的说就是多了个传参，比如：http://localhost:4200/api/search/10010，以下是code

{% code-tabs %}
{% code-tabs-item title="model.js" %}
```javascript
import Route from '@ember/routing/route';
import { inject } from '@ember/service';

export default Route.extend({
    ajax: inject(),
    model(params) {
        let url = 'api/search/' + params.id
        return this.get('ajax').request(url)
    }
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

#### 代码解释

跟上面的code很像，就多了个参数，唯一值得说的就是 params.id的id从何而来，这就和你声明路由时的标志有关系啦，你怎么声明的那就怎么取出来就行了。

### 重用model 上下文

有时候你需要获取一个模型，但是你的路由没有参数，因为它是一个子路由，直接在上面或者上面几层的路由有你的路由需要的参数。

在这种情况下，您可以使用paramsFor方法来获取父路由的参数。

这里需要注意的是，如果你尝试在同级别路由上使用paramsFor，将无法获得你预期的结果。以下是code

{% code-tabs %}
{% code-tabs-item title="model/index.js" %}
```javascript
import Route from '@ember/routing/route';
import { inject } from '@ember/service';

export default Route.extend({
    ajax: inject(),
    model() {
        let { id } = this.paramsFor('model')
        let url = 'api/search/' + id
        return this.get('ajax').request(url)
    }
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

#### 代码解释

通过Route提供的paramsFor来过去model路由的传入参数，这里获取的是所有，我这里只有一个id所以就取了一个。

在一些特殊情况下，父路由已经加载了部分数据，而子路由在访问时需要用到那些数据，这个时候可以使用modelFor，以下是code

{% code-tabs %}
{% code-tabs-item title="model/index.js" %}
```javascript
import Route from '@ember/routing/route';
import { inject } from '@ember/service';

export default Route.extend({
    ajax: inject(),
    model() {
        return this.modelFor('model')
    }
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## 路由的跳转

重定向和跳转，都是web开发中会遇到的需求或者问题，今天我们来看看在Ember中是怎么做这件事情的吧！

第一种方法是**transitionTo**，从route调用transitionTo或从Controller中调用**transitionToRoute。**

这写操作将停止当前正在进行的所有，并启动一个新的transition作为重定向进入到另一页面。

 transitionTo的行为与link-to完全相同。关于link-to 自行去官网看template

另一个是**replaceWith**，工作方式与transitionTo相同。

它们之间唯一的区别是他们对于历史管理， replaceWith替换当前路由记录并将其替换为我们重定向到的路由记录，而transitionTo离开当前路由的记录并为重定向创建一个新记录。

具体的请去官方网站查看  [传送门](https://guides.emberjs.com/v2.18.0/routing/redirection/)

