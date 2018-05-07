---
description: 该文档用于Pharbers(法伯宏业)公司内部培训新人使用
---

# Ember Js 前端框架-公司内部培训

## 什么是Ember Js

[**Ember Js官网 &lt;- 传送门**](https://www.emberjs.com/)

[**Ember Js官方的学习路线网站 &lt;- 传送门**](https://emberjs.com/learn/)

{% tabs %}
{% tab title="简单解释" %}
Ember Js简单来说就是一个基于**jQuery**的前端框架，所有jQuery的插件他都可以使用并且提供了开箱即用的api与模板类。
{% endtab %}

{% tab title="详细解释" %}
Ember 是一个应用级别的框架，它不是一个库（好比 jQuery），也不是一个插件（好比 jQuery 的各种插件），它是用来创造整体化的并且更适合规模较大的应用程序的框架。

Ember 作为框架，它提供给你的是一个基础，涵盖了现代 Web App 所需要的一切基本功能支持，比如数据绑定（单向／双向）、状态控制和管理（路由）、视图抽象化（components 等）等等。

另外作为一个框架，它当然还要负责应用逻辑分层和代码组织管理等基本功能。

具体到你要实现的功能，你可以只用 Ember，然后手写 Javascript 代码来实现（如果功能不太复杂的话），你也可以应用第三方的代码库，比如 jQuery 及其插件们（如果功能复杂的话）。

还有其他各种各样的前端相关的功能特性都可以实施在 Ember 应用程序上（所谓 Ember 应用程序，就是指基于 Ember 框架开发的应用程序，可以是 Web，也可以是 Mobile），比如 WebSocket，各种 HTML5 API 等等都可以。
{% endtab %}
{% endtabs %}

## 为什么选择Ember Js

原因有以下几点

1. [全栈式解决方案​](./#quan-zhan-shi-jie-jue-fang-an)
2. [基于jQuery](./#ji-yu-jquery)​
3. 良好的兼容性​
4. 约定优于配置
5. 数据的双向绑定
6. 基于JavaScript的模板引擎
7. 渐进式的向下兼容
8. 开发效率阶梯式的增加

### 全栈式解决方案​

Ember Js 是一个大而全的框架，它几乎囊括了单页应用开发所需要的方方面面: component，model，service，route，temlate，ember-data。

借助 Ember Js 几乎可以完成任何规模的复杂应用，而不用担心它没有提供足够丰富的特性或者需要求助其他第三方库\(不一定可以很好的和框架本身集成\)。

### 基于jQuery

Ember Js 是完全基于 jQuery 的，意味着任何基于 jQuery 的第三方库都可以和 ember app 集成，而这些年构建于 jQuery 之上的框架和插件不计其数，在没有必要重复造轮子的地方，完全可以用丰富的第三方轮子替代，比如 bootstrap，semantic-ui 这种大而全的 UI framework，jQuery-File-Upload 这种可以兼容各种主流浏览器的文件上传组件。

利用这一优势，大量现成的 jQuery 插件能很快集在 ember app 中，借助 ember component 又可以很轻松达到复用的目的。

### 良好的兼容性

