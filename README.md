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
3. [良好的兼容性](./#liang-hao-de-jian-rong-xing)​
4. [约定优于配置](./#yue-ding-you-yu-pei-zhi)
5. [数据的双向绑定](./#shu-ju-de-shuang-xiang-bang-ding)
6. [基于JavaScript的模板引擎](./#ji-yu-javascript-de-zi-fu-chuan-mo-ban-yin-qing)
7. [完备的构建工具和完整构建流程](./#wan-bei-de-gou-jian-gong-ju-he-wan-zheng-gou-jian-liu-cheng)
8. [渐进式的向下兼容](./#jian-jin-shi-de-xiang-xia-jian-rong)
9. [开发效率阶梯式的增加](./#kai-fa-xiao-lv-jie-ti-shi-de-zeng-jia)
10. [牛逼的开发插件](./#niu-bi-de-kai-fa-tiao-shi-cha-jian)

### 全栈式解决方案​

Ember Js 是一个大而全的框架，它几乎囊括了单页应用开发所需要的方方面面: component，model，service，route，temlate，ember-data。

借助 Ember Js 几乎可以完成任何规模的复杂应用，而不用担心它没有提供足够丰富的特性或者需要求助其他第三方库\(不一定可以很好的和框架本身集成\)。

### 基于jQuery

Ember Js 是完全基于 jQuery 的，意味着任何基于 jQuery 的第三方库都可以和 ember app 集成，而这些年构建于 jQuery 之上的框架和插件不计其数，在没有必要重复造轮子的地方，完全可以用丰富的第三方轮子替代，比如 bootstrap，semantic-ui 这种大而全的 UI framework，jQuery-File-Upload 这种可以兼容各种主流浏览器的文件上传组件。

利用这一优势，大量现成的 jQuery 插件能很快集在 ember app 中，借助 ember component 又可以很轻松达到复用的目的。

### 良好的兼容性

最低兼容IE8，目前咱么项目中使用了babel与cssmodule 与sass所以咱们最低支持IE9。

[babel官网 &lt;- 传送门](https://babeljs.io/)

### **约定优于配置**

开发、管理和维护复杂的单页应用，是一件非常考验组织架构的事情，组件的复用、网络的交互、全局状态的管理、复杂的表单数据、路由等都需要经过精心设计和严格的代码规范才能最大限度的保证在多人协同开发之下，代码仍具有良好的维护成本和高效高质的产出。

Ember Js 秉承约定由于配置的理念，已经在框架层面把应用的最基本结构确定了，开发者只需要顺势而为，即可保证代码的可维护性和可协作性。  


### **数据的双向绑定**

不同于在 React 中，数据只能单向流动，Ember Js 中的数据默认是双向的，这意味着数据的变更完全交由框架处理，虽然双向数据绑定在复杂应用中易于导致数据的状态变更不易跟踪和维护，但是对于频繁且复杂的表单处理，双向绑定可以极大的提高开发效率，通过一定的约束和规范，让双向绑定在可控的范围内发生，并不会对维护造成太大的影响。

### 基于JavaScript的字符串模板引擎

Ember Js中的模板的渲染是基于Glimmer.js引擎，对于习惯了传统模板的很多后端程序员来说，字符串模板非常易于接受和理解，几乎没有学习成本，而且能很好的反应 html 结构和视图，这点相对于 React 的 jsx 语法就有很大的不同。这点也足以构成像我这样的后端程序员偏爱 Ember Js 的一个理由。

[Glimmer Js &lt;- 传送门](https://glimmerjs.com/)

### 完备的构建工具和完整构建流程

Ember Js 社区提供了完备的构建工具和构建流程来保证 ember app 的开发和发布效率，基上能完成在多种环境之下的一键开发和部署，非常方便。

[Ember Observer Ember的社区中很有名的工具库 &lt;- 传送门](https://emberobserver.com/)

[npm 这个是啥我就不多说了 &lt;- 传送门](https://www.npmjs.com/)

### 渐进式的向下兼容

前端的发展日新月异，新技术层出不穷，要想一直惠于新技术和新方案的发展，需要不断的升级优化。

这也带来了不小的升级维护开销，如果一个框架完全不考虑遗留系统，升级代价巨大，对于人力紧缺，时间宝贵的小团队来说，这样的代价负担不起。Ember Js 很好的做到了这一点，基本每个版本都可以做出很平滑的过渡，而不是大规模的修改。在这一点上，Angular 就显得非常激进，虽然说现在好了很多。

### 开发效率阶梯式的增加

当你熟悉了Ember Js框架后，你的开发效率是成本的增长，这个等你们掌握了后就会有感受的。

### 牛逼的开发调试插件

为什么这个要拿出来说一下呢，其他的语言我不管，但是对于前端来讲，牛逼的开发调试插件能为省去一大部分时间。[Ember Inspector  &lt;- 传送门](https://chrome.google.com/webstore/detail/ember-inspector/bmdblncegkenkacieihfhpjfppoconhi)

