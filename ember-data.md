---
description: Ember Data是这个框架中比较难理解库，同时也很重要
---

# Ember Data

**建议吧Ember其他的学会后在看这个，因为这部分官方没有太多的学习资料，大部分需要阅读源码或者与别人交流来学习**

## 什么是Ember Data

Ember Data是一个很健壮的模型数据管理的库应用于Ember.js中。

Ember Data本身与持久性机制无关，它只是提供了一套高级的API供你去调用和扩展，所以它与HTTP上的JSON API以及流式WebSocket或本地IndexedDB存储一样，只需要关注与本身的逻辑就好。

它提供了许多你可以在服务器端ORM（例如Ruby的ActiveRecord）中找到的工具，而且这些API专门针对浏览器中JavaScript的独特环境而设计。

那Ember Data从头开始使用Promises / A +规范，并且使用**Promise**来管理加载和保存记录，因此与JavaScript API的集成非常简单。

**Ember Data 2.0和更高版本不再支持Internet Explorer 8。**

在Ember Data中，Stroe负责管理模型的生命周期。每次你需要一个模型或一系列模型时，你都会去访问Stroe。

更加详细的用法请去 [传送门](https://github.com/emberjs/data) 查阅。

## Adapter概念

处理所有对外的 HTTP 请求。在代码层面，不会直接通过 adapter 来发出请求，而是通过 store 提供的接口将请求代理给 adapter，但是 store 不关心请求的具体实现，它只提供接口并将请求的细节传递给 adapter，具体发送请求的逻辑是在 adapter 内部实现的。

## Serializer概念

Adapter 发请求/收响应时需要对 payload（数据载荷）进行序列化的操作，简单来说就是 Object 和 JSON 之间的相互转换，以及 Object 的数据结构的转换。这部分的工作 adapter 会代理给配套的 serializer 来处理。

## Store概念

用户在本地创建的数据以及通过 adapter 请求到的数据都会按照 Model（数据模型）分门别类的存储在一个本地的内存式的数据仓库里，这个仓库可以看作一个简易版的关系型数据库，可以对数据进行创建/修改/查询/删除/关系处理等操作，这些本地化的操作都由一个统一的 interface（接口）来实现，也就是 store；同时，一些本地操作也有对应的持久化请求（也就是发送给服务器的请求），store 也负责代理这些请求给对应的 adapter

上面说的都是Ember Data的中的最重要的，所以一定要理解。

## 基本的API

Ember Data所有的Api都在[这里](https://emberjs.com/api/ember-data/release/modules/ember-data)，建议你都看一遍，下面我会讲一下常用的。

其实仔细的去看Api就会发现，里面大部分都是跟上面讲的脱不开身，都是围绕着三要素 Adapter、Serializer、Store。

### Adapter

Ember Data中有这几种 适配器

1. Adapter
2. JSONAPIAdapter
3. RESTAdapter

[Adapter](https://emberjs.com/api/ember-data/2.18/classes/DS.Adapter) 是最基础的一个适配器，它相当于所有适配器的一个基类，官方的说法是，如果你要写自己的适配器，最好从Adapter入手。

[JSONAPIAdapter](https://emberjs.com/api/ember-data/2.18/classes/DS.JSONAPIAdapter) 一看名字就知道，这个Adapter是完全符合[JSONAPI](http://jsonapi.org/)规范的，顺便一提的是，现在的Ember Data 默认的通讯协议是JSONAPI，这是一个标准，未来我们会完全符合这个标准，那不符合这个标准的时候应该怎么办呢？要么自己扩展Adapter，要么就是使用下面这一种。

[RESTAdapter](https://emberjs.com/api/ember-data/2.18/classes/DS.RESTAdapter) 上面的JSONAPIAdapter是专门给JSONAPI风格用的，那这种就是给RESTfull风格用的Adapter，现在的后端协议大部分跟RESTfull很像，尤其是暴露给外部供人调用的接口。

Adapter 几乎就是负责请求的逻辑这一块，像什么设置接口地址或者前缀这些操作也都在这里进行。

### Serializer

Ember Data中有这几种 序列化

1. Serializer
2. JSONAPISerializer
3. JSONSerializer
4. RESTSerializer

这几个都是跟上面配套的，这里就简单的讲一下。

[Serializer](https://emberjs.com/api/ember-data/2.18/classes/DS.Serializer) 也是一个最基础的适配，跟Adapter一样，如果你要实现自己的序列化那就从这里入手，去扩展这个接口。

[JSONAPISerializer](https://emberjs.com/api/ember-data/2.18/classes/DS.JSONAPISerializer)  看名字也知道这个是跟JSONAPIAdapter配套使用的，主要接收和处理符合JSONAPI规范的数据，通过payload把数据取出来做一些操作，让其完全不符JSONAPI的规范。

[RESTSerializer](https://emberjs.com/api/ember-data/2.18/classes/DS.RESTSerializer)  用于处理符合RESTfull风格的数据，用法与JSONAPISerializer差不多，都是将payload数据取出来把不符合RESTfull的部分编程完全符合。

[JSONSerializer](https://emberjs.com/api/ember-data/2.18/classes/DS.JSONSerializer)  处理后端协议完全不符合JSONAPI与RESTfull这2种的Serializer，方法与上面一样都是从payload中取出数据将其变成符合JSONAPI或RESTfull风格的数据。

### Store

这个是一个数据仓储，它提供了很多高级的api与数据模型，下面我来介绍下基本的。

#### [DS.Model](https://emberjs.com/api/ember-data/2.18/classes/DS.Model)

这是Ember Data模型的公共API。如果你在应用程序中使用Ember Data，那么这是你必须使用的类，因为他会通过数据类型进行双向的数据绑定，同时Model也实现了很多重要的功能，如属性的对应关系、数据的加载状态、保存于删除接口等。

#### [各种查询接口](https://emberjs.com/api/ember-data/2.18/classes/DS.Store)

看官网吧，不懂的再问我。

