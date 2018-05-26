---
description: 本章主要讲解计算属性的一些概念与使用语法
---

# Ember 中计算属性

## 介绍

计算属性在Ember中算是比较重要的一个特性，下面我们来讲一下他大概在什么场景下会使用。

首先简单的说下计算属性的概念，计算属性允许您将函数声明为属性，就是你可以通过将计算属性定义为function来创建一个执行函数，当您要求该属性的值时，Ember将自动调用该属性。

有一点尤为重要，计算属性是**惰性求值（lazy）**，简单来讲就是需要时在进行计算处理，所以在使用时会有些小陷阱需要注意哦。

## 使用场景

使用场景还是比较多的，比如数学计算、设置属性、结合API处理一些后端返回的数据。

举一个简单的例子，这里和官方一样，关于用户名的显示问题。

一般来说，当一个人登入了系统，肯定会显示用户名，那这用户名的显示是基于后端同学返给你的接口中的字段来获取的，一般来说要么直接给你全名，要么就是firstName与lastName的通过两个字段给你返回来。

因为全名（fullName）是可以firstName与lastName计算出来，那如果以前没有计算属性，一定是在前端先拼一个firstName 再来个lastName，亦或者写一个fullName的Function 并且return出 firstName和lastName。这样做有个巨大的缺陷，就是一旦firstName或lastName被改变后，我们无法获得新的fullName，导致视图刷新才能显示最新的值。那有没有什么办法在改变值后还能悄无声息的去得到新的值并且无刷新的渲染到页面？答案就是使用计算属性来做这件事情，计算属性会根据**依赖的属性**改变去计算出自己的值。

## 具体使用

```javascript
import EmberObject, { computed } from '@ember/object';

const Person = EmberObject.extend({
    firstName: '',
    lastName: '',
    fullName: computed('firstName', 'lastName',  {
        let firstName = this.
        return ``
    })
});
```

