系统学习PHP与面向对象、设计模式
====
编辑、整理 By [xujiajun](http://github.com/xujiajun)
- - - 
前言
----
如何编辑本文？[请点击这里](https://github.com/xujiajun/Learning-PHP/edit/master/README.md)

如何fork本文？点击右上角"Fork" 按钮.

如何发pull Requests 作出贡献? [请点击这里] (https://github.com/xujiajun/Learning-PHP/pulls)

<h2>目录</h2>
- [1、PHP简介](#php-intro)
- [2、PHP对象基础](#php-obj)

<h2 id="php-intro">1、PHP简介</h2>

**① 什么是PHP?**

PHP:超文本预处理器

PHP 是一种服务器端的脚本语言，类似 ASP

PHP 脚本在服务器上执行

PHP 支持很多数据库（MySQL、Informix、Oracle、Sybase、Solid、PostgreSQL、Generic ODBC 等等）

PHP 是一个开源的软件（open source software，OSS）

PHP 可免费下载使用

**②基本语法**

PHP的脚本块以<?php开始，以 ?> 结束。您可以把 PHP 的脚本块放置在文档中的任何位置。
当然，在支持简写的服务器上，您可以使用 [[<? 和 ?>]] 来开始和结束脚本块。
不过，为了达到最好的兼容性，我们推荐您使用标准形式 (<?php)，而不是简写形式。

<h2 id="php-obj">2、PHP对象基础</h2>

① 编写第一个类
```php
class ShopProduct {
    //类体
}
```
② 第一个对象（或者两个）

```php
$product1 = new ShopProduct();
$product2 = new ShopProduct();
```
<strong>new</strong> 操作符和作为他唯一操作数的类名一起被调用，并生成类的实例。
本例中$product1和$product2同一个类生成的相同类型的不同对象

③ 类属性
puclic(公开访问)、protected（仅子类、父类可以访问）、private（仅本类才能访问）

```php
class ShopProduct
{
  public $title = "default";
  public $price = 10;
  public $fristName = "Super";
  public $secondName = "U";
}
```
④访问属性
我们可以用->来访问属性变量，如下：

```php
$product1 = new ShopProduct();
echo $product1->price;//这边输出 10
```
⑤设置属性
因为属性被定义成public,所以我们可以给属性附值：

```php
$product1->price = 20;
echo $product1->price;//这边输出 20
```

当我们要获取名字(full name)：我们可以这样做：

```php
echo $product1->firstName." ".$product1->secondName(); //super U
```

太麻烦了实在。如果能让对象代替我们处理这件苦差事就好了。请看下面的使用方法。

⑥使用方法

格式如下

```php
public function myMethod()
{
//...
}
```

ShopProduct类 可以改成这样：

```php
class ShopProduct
{
  public $title = "default";
  public $price = 10;
  public $fristName = "Super";
  public $secondName = "U";
  
  //注意类方法也可以声明成public\protected\private
  public function getFullName()
  {
     return  $product1->firstName." ".$product1->secondName(); 
  }
}
```

如何使用？

```php
$product1 = new ShopProduct();
echo $product1->getFullName();  //输出super U，刚才的问题得到了解决。

```




