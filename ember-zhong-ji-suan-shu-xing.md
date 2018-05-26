---
description: 本章主要讲解计算属性的一些概念与使用语法
---

# Ember 中计算属性

## 介绍

计算属性在Ember中算是比较重要的一个特性，下面我们来讲一下他大概在什么场景下会使用。

首先简单的说下计算属性的概念，计算属性允许您将函数声明为属性，就是你可以通过将计算属性定义为function来创建一个执行函数，当要求出该属性的值时，Ember将自动调用。

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
    fullName: computed('firstName', 'lastName',  function(){
        let firstName = this.get('firstName');
        let lastName = this.get('lastName');
        return `${firstName}-${lastName}`
    })
});

let qp = Person.create({
    firstName: '钱',
    lastName: '鹏'
})
window.console.info(qp.get('fullName')) // console 钱-鹏
```

此处一定要是用.get来获取fullName，只有触发这个get操作，计算属性才会被Ember执行。

computed依赖的firstName和lastName任何改变，那在get fullName的时候就会重新计算。



computed的计算依赖还可以**Object里的属性值**，以下是code：

```javascript
import EmberObject, { computed } from '@ember/object';

const obj = EmberObject.extend({
    baz: { foo: 'Test1', tzl: 'Test2' }
    fullName: computed('baz.{foo, tzl}',  function(){
        return `${this.get('baz.foo')}-${this.get('baz.tzl')}`
    })
});

let o = obj.create();
window.console.info(o.get('fullName')) // console Test1-Test2
```



computed的计算依赖也可以computed，以下是code：

```javascript
import EmberObject, { computed } from '@ember/object';

const Person = EmberObject.extend({
    firstName: '',
    lastName: '',
    fullName: computed('firstName', 'lastName',  function(){
        return `${this.get('firstName')}-${this.get('lastName')}`
    }),
    describe: computed('fullName', function(){
        return `你好我的名字叫: ${this.get('fullName')}`;
    })
});

let qp = Person.create({
    firstName: '钱',
    lastName: '鹏'
})
window.console.info(qp.get('describe')) // console 你好我的名字叫: 钱-鹏
```



上章我们讲到，Object会有get和set方法，那computed也是Object扩展下来的，那么它肯定也有get和set，computed所有的get方法都在上面演示完了，下面演示以下set，在一般情况下很少会对computed进行set操作，大多是都是get，那如何使用set，以下是code

```javascript
import EmberObject, { computed } from '@ember/object';

const Person = EmberObject.extend({
    firstName: '',
    lastName: '',
    fullName: computed('firstName', 'lastName',{
        get(key) {
            return `${this.get('firstName')}-${this.get('lastName')}`
        },
        set(key, value) {
            let [fName, lName] = value.split(/\s+/)
            this.set('firstName', fName);
            this.set('lastName', lName);
            return value;
        }
    })
});

let qp = Person.create({
    firstName: '钱',
    lastName: '鹏'
})
window.console.info(qp.get('fullName')) // console 钱-鹏
window.console.info(qp.get('firstName')) // console 钱
window.console.info(qp.get('lastName')) // console 鹏
qp.set('fullName', 'Alex Qian');
window.console.info(qp.get('fullName')) // console Alex-Qian
window.console.info(qp.get('firstName')) // console Alex
window.console.info(qp.get('lastName')) // console Qian

```

到现在computed基本的用法和概念差不多都讲完了，剩余拓展的部分你可以去官网查看相对应的例子。

