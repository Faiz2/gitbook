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
})

```
{% endcode-tabs-item %}
{% endcode-tabs %}

## 调用创建刚才声明的people Classes

{% code-tabs %}
{% code-tabs-item title="调用刚才的people Classes" %}
```javascript
import People from 'people';

let p = People.create();
p.sayHi(); // console Hi，我是Pharbers的钱鹏，很高兴认识你。
```
{% endcode-tabs-item %}
{% endcode-tabs %}

  
  


