系统学习PHP与面向对象
====
本教程由 [xujiajun][xujiajun] 整理、编辑并在 [CC BY-SA 3.0][CC] 协议下发布，主要为了给自己和各位朋友作为系统学习PHP与面向对象的参考资料。更多请关注 [superu.org][superu]
[CC]: http://zh.wikipedia.org/wiki/Wikipedia:CC "Wiki: CC"
[xujiajun]:http://xujiajun.cn
[superu]:http://superu.org
- - - 
前言
----
点击右上角的 **[Watch](https://github.com/xujiajun/PHP-Objects-guidance/subscription)** 进行订阅，点击 Star 进行收藏。[点击讨论](https://github.com/xujiajun/PHP-Objects-guidance/issues)

<h2>目录</h2>
- [1、PHP简介](Introduction.md)
- &nbsp;&nbsp;[1.1、什么是PHP?](#what-is-PHP)
- &nbsp;&nbsp;[1.1、PHP基本语法](#PHP-syntax)
- [2、PHP对象基础](Object.md)
- &nbsp;&nbsp;[2.1、编写第一个类](#first-class)
- &nbsp;&nbsp;[2.2、第一个对象（或者两个）](#first-object)
- &nbsp;&nbsp;[2.3、类属性](#class-attribute)
- &nbsp;&nbsp;[2.4、访问属性](#access-attribute)
- &nbsp;&nbsp;[2.5、设置属性](#set-attribute)
- &nbsp;&nbsp;[2.6、函数（方法）使用](#create-func)
- &nbsp;&nbsp;[2.7、构造函数](#construct-func)
- &nbsp;&nbsp;[2.8、基本类型和PHP类型检查函数](#base-type)
- &nbsp;&nbsp;[2.9、继承](#extends)
- [3、高级特性](Advanced-feature.md)
- &nbsp;&nbsp;[3.1、静态方法和属性](#static)
- &nbsp;&nbsp;[3.2、常量属性](#const)
- &nbsp;&nbsp;[3.3、抽象类](#abstract-class)
- &nbsp;&nbsp;[3.4、接口](#interface)
- &nbsp;&nbsp;[3.5、错误处理](#error-process)
- &nbsp;&nbsp;[3.6、Final类和方法](#final)
- &nbsp;&nbsp;[3.7、使用拦截器](#interceptor)
- &nbsp;&nbsp;[3.8、析构方法](#destruct)
- &nbsp;&nbsp;[3.9、克隆对象](#clone)
- [4、对象工具](Object-tool.md)
- &nbsp;&nbsp;[4.1、PHP与包](#php-package)
- &nbsp;&nbsp;[4.2、类函数和对象函数](#class-object-func)
- &nbsp;&nbsp;[4.3、反射API](#reflect-api)
- &nbsp;&nbsp;&nbsp;&nbsp;[4.3.1、入门](#reflect-intro)
- &nbsp;&nbsp;&nbsp;&nbsp;[4.3.2、类检测](#reflect-class)
- &nbsp;&nbsp;&nbsp;&nbsp;[4.3.3、方法检测](#reflect-method)
- &nbsp;&nbsp;&nbsp;&nbsp;[4.3.4、参数检测](#reflect-parameters)
- &nbsp;&nbsp;&nbsp;&nbsp;[4.3.5、使用反射API](#use-reflection-api)
- [5、对象与设计](Object-and-design.md)
- &nbsp;&nbsp;[5.1、面向对象设计和过程式编程](#diff-object-process)
- &nbsp;&nbsp;[5.2、定义类](#choose-object)
- &nbsp;&nbsp;[5.3、多态](#polymorphism)
- &nbsp;&nbsp;[5.4、封装](#encapsulation)
- &nbsp;&nbsp;[5.5、忘记细节](#program-interface)
