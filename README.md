EventBus
========
EventBus is a publish/subscribe event bus optimized for Android.<br/>
<img src="EventBus-Publish-Subscribe.png" width="500" height="187"/>

EventBus...

EventBus 事件总线 总结:
	基于观察者模式 +反射 (或者apt生成代码) annotain-Processor 升级版?

要使用编译中生成的代码必须配置EventBubBuilder 中的’索引’  该类查找了订阅者所有订阅方法。

自己生成的EventBus最好 setDefaultInstance() 单例配置

观察者那肯定要有观察者和被观察者，而观察者关注某件事情，要实现观察者和被观察者之间的解耦，必须引用第三方。由第三方持有观察者和被观察者的引用。

核心方法
	register
	unregister
	post

核心变量:
	第三方机构
	Subscription包含订阅者订阅方法
Register核心 是下面两个方法
Post 核心	Map<EventType,List<Subscription>
unregister核心	Map<Subscriber,List<EventType>>


 * simplifies the communication between components
    * decouples event senders and receivers
    * performs well with Activities, Fragments, and background threads
    * avoids complex and error-prone dependencies and life cycle issues
 * makes your code simpler
 * is fast
 * is tiny (~50k jar)
 * is proven in practice by apps with 100,000,000+ installs
 * has advanced features like delivery threads, subscriber priorities, etc.

 [![Build Status](https://travis-ci.org/greenrobot/EventBus.svg?branch=master)](https://travis-ci.org/greenrobot/EventBus)

EventBus in 3 steps
-------------------
1. Define events:

    ```java  
    public static class MessageEvent { /* Additional fields if needed */ }
    ```

2. Prepare subscribers:
    Declare and annotate your subscribing method, optionally specify a [thread mode](http://greenrobot.org/eventbus/documentation/delivery-threads-threadmode/):  

    ```java
    @Subscribe(threadMode = ThreadMode.MAIN)  
    public void onMessageEvent(MessageEvent event) {/* Do something */};
    ```
    Register and unregister your subscriber. For example on Android, activities and fragments should usually register according to their life cycle:

   ```java
    @Override
    public void onStart() {
        super.onStart();
        EventBus.getDefault().register(this);
    }
 
    @Override
    public void onStop() {
        super.onStop();
        EventBus.getDefault().unregister(this);
    }
    ```

3. Post events:

   ```java
    EventBus.getDefault().post(new MessageEvent());
    ```

**Read the full [getting started guide](http://greenrobot.org/eventbus/documentation/how-to-get-started/).**

Add EventBus to your project
----------------------------
Please ensure that you are using the latest version by [checking here](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22org.greenrobot%22%20AND%20a%3A%22eventbus%22)

Gradle:
```gradle
compile 'org.greenrobot:eventbus:3.0.0'
```

Maven:
```xml
<dependency>
    <groupId>org.greenrobot</groupId>
    <artifactId>eventbus</artifactId>
    <version>3.0.0</version>
</dependency>
```

[Or download EventBus from Maven Central](http://search.maven.org/#search%7Cga%7C1%7Cg%3A%22org.greenrobot%22%20AND%20a%3A%22eventbus%22)

Homepage, Documentation, Links
------------------------------
For more details on EventBus please check [EventBus' website](http://greenrobot.org/eventbus). Here are some direct links you may find useful:

[Features](http://greenrobot.org/eventbus/features/)

[Documentation](http://greenrobot.org/eventbus/documentation/)

[Changelog](http://greenrobot.org/eventbus/changelog/)

[FAQ](http://greenrobot.org/eventbus/documentation/faq/)

How does EventBus compare to other solutions, like Otto from Square? Check this [comparison](COMPARISON.md).

License
-------
Copyright (C) 2012-2016 Markus Junginger, greenrobot (http://greenrobot.org)

EventBus binaries and source code can be used according to the [Apache License, Version 2.0](LICENSE).

More Open Source by greenrobot
==============================
[__greenrobot-common__](https://github.com/greenrobot/greenrobot-common) is a set of utility classes and hash functions for Android & Java projects.

[__greenDAO__](https://github.com/greenrobot/greenDAO) is an ORM optimized for Android: it maps database tables to Java objects and uses code generation for optimal speed.

[Follow us on Google+](https://plus.google.com/b/114381455741141514652/+GreenrobotDe/posts) or check our [homepage](http://greenrobot.org/) to stay up to date.
