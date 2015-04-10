系统学习PHP与面向对象、设计模式
====
编辑、整理 By [xujiajun](http://xujiajun.cn)
- - - 
前言
----
如何编辑本文？[请点击这里](https://github.com/xujiajun/Learning-PHP/edit/master/README.md)

如何fork本文？点击右上角"Fork" 按钮.

如何发pull Requests 作出贡献? [请点击这里] (https://github.com/xujiajun/Learning-PHP/pulls)

<h2>目录</h2>
- [1、PHP简介](#php-intro)
- &nbsp;&nbsp;[1.1、什么是PHP?](#what-is-PHP)
- &nbsp;&nbsp;[1.1、PHP基本语法](#PHP-syntax)
- [2、PHP对象基础](#php-obj)
- &nbsp;&nbsp;[2.1、编写第一个类](#first-class)
- &nbsp;&nbsp;[2.2、第一个对象（或者两个）](#first-object)
- &nbsp;&nbsp;[2.3、类属性](#class-attribute)
- &nbsp;&nbsp;[2.4、访问属性](#access-attribute)
- &nbsp;&nbsp;[2.5、设置属性](#set-attribute)
- &nbsp;&nbsp;[2.6、函数（方法）使用](#create-func)
- &nbsp;&nbsp;[2.7、构造函数](#construct-func)
- &nbsp;&nbsp;[2.8、基本类型和PHP类型检查函数](#base-type)
- &nbsp;&nbsp;[2.9、继承](#extends)
- [3、高级特性](#advanced-feature)
- &nbsp;&nbsp;[3.1、静态方法和属性](#static)
- &nbsp;&nbsp;[3.2、常量属性](#const)
- &nbsp;&nbsp;[3.3、抽象类](#abstract-class)
- &nbsp;&nbsp;[3.4、接口](#interface)
- &nbsp;&nbsp;[3.5、错误处理](#error-process)
- &nbsp;&nbsp;[3.6、Final类和方法](#final)

<h2 id="php-intro">1、PHP简介</h2>

<h5 id="what-is-PHP">1.1、什么是PHP?</h5>

PHP:超文本预处理器

PHP 是一种服务器端的脚本语言，类似 ASP

PHP 脚本在服务器上执行

PHP 支持很多数据库（MySQL、Informix、Oracle、Sybase、Solid、PostgreSQL、Generic ODBC 等等）

PHP 是一个开源的软件（open source software，OSS）

PHP 可免费下载使用

<h5 id="PHP-syntax">1.2、PHP基本语法</h5>

PHP的脚本块以<?php开始，以 ?> 结束。您可以把 PHP 的脚本块放置在文档中的任何位置。
当然，在支持简写的服务器上，您可以使用 [[<? 和 ?>]] 来开始和结束脚本块。
不过，为了达到最好的兼容性，我们推荐您使用标准形式 (<?php)，而不是简写形式。

<h2 id="php-obj">2、PHP对象基础</h2>

<h5 id="first-class">2.1、编写第一个类</h5>
```php
class ShopProduct {
    //类体
}
```
<h5 id="first-object">2.2、第一个对象（或者两个）</h5>

```php
$product1 = new ShopProduct();
$product2 = new ShopProduct();
```
<b>new</b> 操作符和作为他唯一操作数的类名一起被调用，并生成类的实例。
本例中$product1和$product2同一个类生成的相同类型的不同对象

```关于类和对象关系 请移步```[点击观看视频](http://superu.org/course/6/learn#lesson/14)
<h5 id="class-attribute">2.3、类属性</h5>
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
<h5 id="access-attribute">2.4、访问属性</h5>
我们可以用->来访问属性变量，如下：

```php
$product1 = new ShopProduct();
echo $product1->price;//这边输出 10
```
<h5 id="set-attribute">2.5、设置属性</h5>
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

<h5 id="create-func">2.6、函数（方法）使用</h5>

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

<h5 id="construct-func">2.7、构造函数</h5>

小需求：现在要创建一个fullName分别为Super2 U2、Super3 U3的对象。并分别得到他的fullName值,我们可以这么做：

```php
$product2 = new ShopProduct();
$product2->fristName = "Super2"
$product2->secondName = "U2";
echo $product2->getFullName();

$product3 = new ShopProduct();
$product3->fristName = "Super3"
$product3->secondName = "U3";
echo $product3->getFullName();
```

ok done.

有没有觉得太繁琐？有没有能自动调用的方法。答案是肯定的。引出我们的构造方法：

```php
class ShopProduct
{
  public $title = "default";
  public $price = 10;
  public $fristName = "Super";
  public $secondName = "U";
  
  function __construct($title, $price, $firstName, $secondName)
  {
      $this->title = $title;
      $this->price = $price;
      $this->firstName = $firstName;
      $this->secondName = $secondName;
  }
  
  public function getFullName()
  {
     return  $product1->firstName." ".$product1->secondName(); 
  }
}
```
注意关键词 <b>__construct</b>,他会在创建对象时候，自动去调用。

让我们try it.改造上面的小需求：

```php
$product2 = new ShopProduct(‘default’,10,'Super2'，'U2');
echo $product2->getFullName();

$product3 = new ShopProduct(‘default’,10,'Super3','U3');
echo $product3->getFullName();
```
ok done.是不是简洁了很多。

<h5 id="base-type">2.8、基本类型和PHP类型检查函数</h5>

<table>
<tr>
    <th>类型检查函数</th>
    <th>类型</th>
    <th>描述</th>
</tr>
<tr>
    <td>is_bool()</td>
    <td>布尔型</td>
    <td>值为true或者false</td>
</tr>
<tr>
    <td>is_integer()</td>
    <td>整型</td>
    <td>整数</td>
</tr>
<tr>
    <td>is_double()</td>
    <td>双精度型</td>
    <td>浮点数</td>
</tr>
<tr>
    <td>is_string()</td>
    <td>字符串</td>
    <td>字符数据</td>
</tr>
<tr>
    <td>is_object()</td>
    <td>对象</td>
    <td>对象</td>
</tr>
<tr>
    <td>is_array()</td>
    <td>数组</td>
    <td>数组</td>
</tr>
<tr>
    <td>is_resource()</td>
    <td>资源</td>
    <td>用于识别和处理外部资源的（如数据库或文件）句柄</td>
</tr>
<tr>
    <td>is_null()</td>
    <td>NULL</td>
    <td>未分配的值</td>
</tr>
</table>

<h5 id="extends">2.9、继承</h5>
继承是从一个类得到一个或者多个类的机制。

例子：


```php
class ShopProduct
{
  public $title = "default";
  public $price = 10;
  public $fristName = "Super";
  public $secondName = "U";
  public $playLength;
  
  function __construct($title, $price, $firstName, $secondName,$playLength)
  {
      $this->title = $title;
      $this->price = $price;
      $this->firstName = $firstName;
      $this->secondName = $secondName;
      $this->playLength = $playLength;
  }
  //注意类方法也可以声明成public\protected\private
  public function getFullName()
  {
     return  $this->firstName." ".$this->secondName(); 
  }
}
```

```php
Class CdProduct extends ShopProduct
{
    function getplayLength()
    {
        return $this->playLength;
    }
}
```
这样CdProduct除继承父类ShopProduct所有特性外，还自己多了个getplayLength的方法

<h2 id="advanced-feature">3、高级特性</h2>

<h5 id="static">3.1、静态方法和属性</h5>
我们不仅可以通过对象来访问方法和属性，还可以通过类来访问它们。这样的方法和属性是“静态的”
<b>static</b>关键词来声明。

example:

```php
class StaticExample
{
    static public $aNum;
    static public function sayHi()
    {
        echo "hi,xujiajun :)"
    }
}
```
如何访问？

因为通过类而不是实例来访问静态元素，所以访问静态元素时，不需要引用对象的变量，用::(双冒号)来连接
StaticExample::$aNum;
echo StaticExample::sayHi(); //输出 hi,xujiajun :)

在StaticExample内部，用关键词<b>self</b>关键词：

```php
class StaticExample
{
    static public $aNum = 0;
    static public function sayHi()
    {
        self::$aNum++;
        echo "hi,xujiajun :)".self::$aNum."\n";
    }
}
```

<h5 id="const">3.2、常量属性</h5>

example:

```php
class ShopProduct
{
    const AVAILABLE = 0;
}
```

Q:如何使用？

A:Shopproduct::AVAILABLE;

Q:什么时候需要使用他？

A当需要类的所有实例中都能访问某个属性，并且属性值无需改变时，应该使用常量。

<h5 id="abstract-class">3.3、抽象类</h5>

注意抽象类不能被直接实例化。

抽象类中只定义（或者部分实现）子类需要的方法。子类可以继承他并且通过实现其中的抽象方法，使其具体化。

使用<b>abstract</b>关键词来定义一个抽象类。

example:

```php
abstract class ShopProductWriter
{
    protected $product = array();
    
    public function addProduct(ShopProduct $shopProduct)
    {
        $this->products[] = $shopProduct;
    }
}
```

在声明抽象方法不是以方法体结束，以分号结束。

```php
abstract class ShopProductWriter
{
    protected $product = array();
    
    public function addProduct(ShopProduct $shopProduct)
    {
        $this->products[] = $shopProduct;
    }
    
    abstract public function write();
}
```
创建抽象方法后，要确保所有子类中都实现该方法，但实现的细节可以先不确定。

```php
class ErrorWriter extends ShopProductWriter{}; 
//Fatal error: Class ErrorWriter contains 1 abstract method and must therefore be declared abstract or implement the remaining methods (ShopProductWriter::write) in ...
```
改成如下，就ok了:
```php
class TextProductWriter extends ShopProductWriter
{
    public function write()
    {
    }
}
```
<h5 id="interface">3.4、接口</h5>

抽象类提供了具体的实现的标准，而接口则是纯粹的模板

example:

```php
interface Chargeable
{
    public function getPrice();
}
```

任何实现接口都要实现接口中所定义的所有方法，否则该类必须声明为abstract

关键词<b>implements</b>来实现某一个接口。

example:

```php
class ShopProduct implements Chargeable
{
    //...
    public function getPrice()
    {
        return ($this->price - $this->discount);  
    }
}
```

一个类可以实现一个父类。多个接口
example:

```php

interface run
{
    //...
}

interface fly
{
    //...
}

class People
{
    //...
}

class Xujiajun extends People implements run,fly
{
    //...
}
```
这里 Xujiajun这个类 继承了People类，实现了不止一个接口

注意：PHP只支持继承一个父类，因此extends关键词只能在一个类名之前。

<h5 id="error-process">3.5、错误处理</h5>

文件放错地方、数据库服务区未初始化、URL变动、XML文件损坏、权限设置得不对、磁盘空间限制等，这些问题，时常发生。
一个类里面 我们会充满了错误处理的代码。

<b>异常</b> 。这是一种完全不同的处理错误的方式。异常能解决刚提到的所有问题。

Exception类的public的方法

<table>
<tr>
        <th>方法</th>
        <th>描述</th>
</tr>
<tr>
    <td>getMessage()</td>
    <td>获得传递给构造方法的消息字符串</td>
</tr>
<tr>
    <td>getCode()</td>
    <td>获得传递给构造方法的错误代码</td>
</tr>
<tr>
    <td>getFile()</td>
    <td>获得产生异常的文件</td>
</tr>
<tr>
    <td>getLine()</td>
    <td>获得异常生成的行数</td>
</tr>
<tr>
    <td>getTrace()</td>
    <td>获得一个多维数组，追踪导致异常的方法调用，包含文件、类、文件、参数数据</td>
</tr>
<tr>
    <td>getTraceAsString()</td>
    <td>获得getTrace(返回的字符串版本</td>
</tr>
<tr>
    <td>__toString()</td>
    <td>在字符串中使用Exception对象时自动调用。返回一个描述异常细节的字符串</td>
</tr>
</table>

①抛出异常

关键词<b>throw和Exception对象</b>来抛出异常。

example:

```php
function write ()
{
    if (!is_writeable($this->file)) {
        throw new Exception("file '{$this->file}' is not writeable!");
    }
}
```

如何捕获异常？

try...catch..

example:

```php

try {
    $conf = new Conf(dirname(__FILE__)."/xujiajun.xml");
    $conf->write();
} catch (Exception $e) {
    die($e->__toString());
}

```

②异常子类化

exmaple:

```php
class XmlException extends Exception{}
```
通过这种方式你可以扩展异常类的功能和定义新的异常类型。

<h5 id="final">3.6、Final类和方法</h5>

Q:什么情况用到Final？

A: 如果希望类和方法完全确定不变的功能，担心覆写它会破坏这个功能。

example:

```php
final class Superu
{
}

下面尝试生成SuperU子类

class SuperuChild extends SuperU
{
}

将会报错。
```

但是，注意如果<b>final</b>关键词 放在<b>SuperU</b>这个类的方法里面，继承是不会报错的：

```php

class Superu
{
   final function getName();
}

class SuperUChild extends SuperU
{
}
```

但是，如果你要覆写SuperU类的getName方法，还是会报错的。

注意：高质量的面向对象代码往往强调定义明确的接口。声明类或方法为final，会减少其灵活性。不过有时候我们确实需要这样做。
