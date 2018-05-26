---
description: 本章主要讲解，如何区分Classes和Instances并且如何创建了解该语法
---

# Ember 中的Classes 和 Instances

在了解Ember时，你会看到类似Component.extend（）和DS.Model.extend（）的代码。

在这里，您将了解这个extend（）方法以及Ember对象模型的其他主要功能。

## 如何定义类

要定义一个新的Ember类，需要调用EmberObject上的extend（）方法下面是具体语法：

{% code-tabs %}
{% code-tabs-item title="定一个一个Classes，名为people.js" %}
```javascript
import EmberObject from '@ember/object';

export default EmberObject.extend({
    name: '钱鹏',
    age: 23,
    gender: '男',
    phone: 18994737968,
    sayHi() {
        window.console.info('Hi，我是Pharbers的钱鹏，很高兴认识你。')
    }
});

```
{% endcode-tabs-item %}
{% endcode-tabs %}

## 实例化刚才声明的people Classes

{% code-tabs %}
{% code-tabs-item title="调用刚才的people Classes" %}
```javascript
import People from 'people';

let p = People.create();
p.sayHi(); // console Hi，我是Pharbers的钱鹏，很高兴认识你。
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## 定义Component

上一章讲过Component也是基于Ember Object，那么它也是可被声明创建的，下面是具体code

{% code-tabs %}
{% code-tabs-item title="image.js" %}
```javascript
import Component from '@ember/component';

export default Component.extend({
    imagUrl: '',
    isShow: false
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

一般情况下Component不会单独创建的，但是也有例外，比如当你的子组件需要依赖于父组件的时候，这个是你可以进行继承的方式进行code，下面是具体实现

{% code-tabs %}
{% code-tabs-item title="image-info.js" %}
```javascript
import ImageComponent from 'image';

export default ImageComponent.extend({
    imageName: '',
    imageWith: 20,
    imageHeight: 20
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

## 初始化的操作

{% code-tabs %}
{% code-tabs-item title="init.js" %}
```javascript
import EmberObject from '@ember/object';

export default EmberObject.extend({
    init() {
        this._super(...arguments);
        window.console.info('init()')
    }
});
```
{% endcode-tabs-item %}
{% endcode-tabs %}

在类被create的时候，就会进入Init\(\)的这个函数，由于init这个是EmberObject的，我们只是重新的override了一下，所以我们要加上this.\_super\(\)这句话，来触发基类的方法，来保证函数状态不丢失。

## 如何访问和设置对象属性

{% code-tabs %}
{% code-tabs-item title="setOrGet.js" %}
```javascript
import EmberObject from '@ember/object';

const ObjectInstances = EmberObject.create({
    name: '张三',
    age: 10
});

window.console.info(ObjectInstances.get('name')) // console 张三
ObjectInstances.set('name', '李四')
window.console.info(ObjectInstances.get('name')) // console 李四

```
{% endcode-tabs-item %}
{% endcode-tabs %}

在这里可以看到，我没有直接声明Classes，而是直接create，在EmberObject中是可以直接创建实例，不必写显示声明一定要是个classes，但是要注意，**通过该方式创建的Classes是Singleton** 而且调用时不必再次create，直接用就好。



