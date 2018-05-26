---
description: Ember 框架中的对象模型
---

# Ember 中的Object Model

## JavaScript的Object与Ember的Ember.Object

关于JavaScript这个语言应该很清楚，可是说是基于OO的语言，但它又与其它的基于OO的语言又不同。

以继承来讲，JavaScript的继承是基于[原型继承](https://www.liaoxuefeng.com/wiki/001434446689867b27157e896e74d51a89c25cc8b43bdb3000/0014344997013405abfb7f0e1904a04ba6898a384b1e925000)，具体实现不在这里做过多的解释。

### 简单讲一下JavaScript Object

简单来说JavaScript拥有一个非常简单的对象模型，你可以用一对大括号\({ }\)来定义对象字面量，然后你就可以在大括号里面创建属性、 方法，你可以访问、修改、调用你的定义，基本就是这样，这就是最简单的JavaScript的对象模型，关于你想深入了解，你可以向@党性王把JavaScript的书借来看看。

刚才说了JavaScript的简单的对象模型，那这种简单的对象模型使得这门语言很容易被初学者所接受 ，但是当我们开发**大型**、**复杂**的交互的Web程序的时候，这么简单的模型很难满足我们的需求。

比如说我们想要知道对象有没有被修改，这个时候在对象外面的代码或者其它地方是否知道这个对象被修改了呢？

再比如说我们想知道修改的这个对象，在修改前的value与修改后的value分别是什么呢？在开发Web的时候这种问题时非常重要的，现在好多都是要求在页面不刷新的状况\(除Ajax外\)，你要修改某个对象的时候视图也要同时被更改。但这个在原生的JavaScript中并没有提供一个有效的解决方案。

### 对比一下Angular JS

那在[AngularJS](https://angularjs.org/) 中要做到上述的功能，它内部有个叫做Dirty checking（脏检查）的功能，简单的说就是有个巨大的无限循环来检查对象作用域下用在Angular下的对象它有没有变化，有变化它会通过某些机制去通知整个系统去更新这个对象，来达到你想要的效果。

### [Ember Object](https://guides.emberjs.com/release/object-model/)

相对于Angular JS的这种检查机制，我们的Ember采用的是另一种机制，不会像Angular JS那样不停的去检查整个对象，Ember直接从根本解决这个问题，直接扩展了原生的JavaScript的Object，这就显得非常高级了😏。

那在原生的JavaScript中我们是根据Object这个去做延伸的基点，在Ember中Ember提供了Ember.Object的这个对象，这个对象就是基于原生的Object去扩展而来的同时也带来了一些独有的一些特征\(属性\)。

比如：computed（计算属性）、observer（观察者模式）。

那你用Ember.Object去开发web应用的时候，所有的对象都有了新的特征，比如相互之间通知、根据一个属性的变化去计算另一个属性的值类似于这样的特性。所有我们把这些特性叫做Ember Object Model 。

那Ember提供的Route、Component、Service、Mixin等这些都是基于Ember Object扩展出来的，本质上也是通过原型继承得来的。

要想使用这些就必须要了解Ember Object Model，这篇就大概的介绍下原生与Ember的区别，在一章会介绍具体的用法。

