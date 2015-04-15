系统学习PHP与面向对象、设计模式
====
本文由 [xujiajun][xujiajun] 整理、编辑并在 [CC BY-SA 3.0][CC] 协议下发布，主要为了给自己和各位朋友作为系统学习PHP与面向对象、设计模式的参考资料。更多请关注 [superu.org][superu]
[CC]: http://zh.wikipedia.org/wiki/Wikipedia:CC "Wiki: CC"
[xujiajun]:http://xujiajun.cn
[superu]:http://superu.org
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
- &nbsp;&nbsp;[3.7、使用拦截器](#interceptor)
- &nbsp;&nbsp;[3.8、析构方法](#destruct)
- &nbsp;&nbsp;[3.9、克隆对象](#clone)
- [4、对象工具](#object-tool)
- &nbsp;&nbsp;[4.1、PHP与包](#php-package)
- &nbsp;&nbsp;[4.2、类函数和对象函数](#class-object-func)
- &nbsp;&nbsp;[4.3、反射API](#reflect-api)
- &nbsp;&nbsp;&nbsp;&nbsp;[4.3.1、入门](#reflect-intro)
- &nbsp;&nbsp;&nbsp;&nbsp;[4.3.2、类检测](#reflect-class)
- &nbsp;&nbsp;&nbsp;&nbsp;[4.3.3、方法检测](#reflect-method)
- &nbsp;&nbsp;&nbsp;&nbsp;[4.3.4、参数检测](#reflect-parameters)
- &nbsp;&nbsp;&nbsp;&nbsp;[4.3.5、使用反射API](#use-reflection-api)
- [5、对象与设计](#object-design)
- &nbsp;&nbsp;[5.1、面向对象设计和过程式编程](#diff-object-process)
- &nbsp;&nbsp;[5.2、定义类](#choose-object)
- &nbsp;&nbsp;[5.3、多态](#polymorphism)
- &nbsp;&nbsp;[5.4、封装](#encapsulation)

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

<h5 id="interceptor">3.7、使用拦截器</h5>

拦截器方法：

|方法                        |      描述                         |
|----------------------------|---------------------------------- |
|  __get($property)          |访问未定义的属性被调用             |
|  __set($property)           |对未定义的属性赋值时被调用        |
| __isset($property)          |对未定义的属性调用isset()时被调用 |
|  __unset($property)          |对未定义的属性调用unset()时被调用|
|  __call($method,$arg_array)  |调用未定义的方法时被调用         |

example:

```php

//__get
class Person
{
    
    function __get($argument)
    {
        $method = "get".ucfirst($argument);
        if (method_exists($this, $method)) {
             return $this->$method();
        }
    }

    function getName()
    {
        return "xujiajun";
    }
}


$p = new Person();
echo $p->name; //输出xujiajun

注意：如果方法不存在，则什么也不做。


//__isset:

function __isset($argument)
{
   $method = "get".ucfirst($argument);
        if (method_exists($this, $method)) {
             return $this->$method();
   }
}

if (isset($p->name)) {
    return $p->getName();
}
```

```php

//__set

class Person
{
    private $_name;

    function __set($argument,$value)
    {
        $method = "set".ucfirst($argument);
        if (method_exists($this, $method)) {
             return $this->$method($value);
        }
    }

    function setName($name)
    {
        $this->_name = $name;
        if (!$this->_name) {
            $this->_name = strtoupper($this->_name);
        }
    }
}


$p = new Person();
$p->name = "xujiajun";//注意 这个时候$_name 已经变成 xujiajun


//__unset 和__set向对应

function __unset($property)
{
    $method = "set".ucfirst($argument);
    if (method_exists($this, $method)) {
        return $this->$method(null);
    }
}
```

```php
//__call
class PersonWriter
{
    function writeName(Person $p)
    {
        return $p->getName()."~\n";
    }
}

class person
{
    private $_writer;

    function __construct(PersonWriter $writer)
    {
        $this->_writer = $writer;
    }

    function __call($medthodName,$args)
    {
        if (method_exists($this->_writer, $medthodName)) {
            return $this->_writer->$medthodName($this);
        }
    }

    function getName()
    {
        return "xujiajun";
    }
}

$p = new Person(new PersonWriter());
echo $p->writeName(); //输出xujiajun~
```

<h5 id="destruct">3.8、析构方法</h5>

比如有一个类需要把其自身的信息写入数据库。这时可以使用__destruct()方法在对象实例被删除时确保把自己保存在数据库中:
```php

class Person
{
    private $name;
    private $age;
    private $id;

    function __construct($name,$age)
    {
        $this->name = $name;
        $this->age = $age;
    }
    
    function __destruct()
    {
        if(!empty($this->id))
        {
        //保存信息
            echo "saving person info";
        }
    }
    
    function setId($id)
    {
        $this->id = $id;
    }
}
$p = new Person("xujiajun",18);
$p->setId(18);
unset($p);//输出saving person info
```
注意：析构方法和__call一样这些都是魔术方法。需慎用。

<h5 id="clone">3.9、克隆对象</h5>

```php
class CopyMe
{
};
$firstClass = new CopyMe();
$secondClass = clone $firstClass;
//现在$firstClass、$secondClass是两个不同的对象了
``` 

__clone的使用

```php
class Person
{
    private $name;
    private $age;
    private $id;
    
    function __construct($name,$age)
    {
        $this->name = $name;
        $this->age = $age;
    }
    function __clone()
    {
        $this->id = 0;
    }
}

$p = new Person("xujiajun",18);
$p2 = clone $p;// 这个时候 $p2的id为0,name:xujiajun,age:18
```

<h2 id="object-tool">4、对象工具</h2>

<h5 id="php-package">4.1、PHP与包</h5>

PHP没有支持"包"机制,但我们应该将代码组织类似“包”的结构。

低版本的PHP5，我们可以通过包结构的文件系统来组织类。

require_once 'util/xujiajun1.php';

require_once 'util2/xujiajun2.php';

PHP5.3命名空间引入

example:

```php

//foo.php:

<?php 

namespace foo;

class xujiajun
{
    static function says()
    {
        echo "hi,namespace";
    }
}
?>

//bar.php
<?php

namespace bar;

require_once 'foo.php';

class xujiajun
{
    static function says()
    {
        echo "@hi,namespace2";
    }
}

echo \foo\xujiajun::says();
echo \bar\xujiajun::says();

//输出hi,namespace@hi,namespace2
?>
```

<h5 id="class-object-func">4.2、类函数和对象函数</h5>

PHP提供了一系列强大的函数来检测和对象

查找类
example：

```php
//class_exists()函数接受表示类的字符串，检查并返回布尔值。

$className = "superu";

if (!class_exists($className))
{
    throw new Exception("No such class $className");
}
//当然，我们无法确定该类的构造方法是否需要参数。在这个级别的安全上，应该求助反射api
```

PHP有很多用于检测对象类型的基本工具。首先，可以使用get_class()函数检查对象的类,他接受任何对象作为参数。

example:

```php
$person = new Xujiajun();

if(get_class($person) == "Xujiajun")
{
    print "$person is a Xujiajun object\n";
}
```

我们有时候只想确定一个类的类型,比如只想知道是不是Person这个类的，我们不关心是不是Xujiajun还是Superu。
为此，PHP提供了instanceof这个操作符。

example:

```php
$person = new Person();

if($person instanceof Person)
{
    echo "$person is a Person object\n";
}
```

我们如果需要知道类中的方法，怎么办？PHP提供了`get_class_methods()`函数得到一个类中的所有方法列表。

example:

```php

<?php 
class Xujiajun
{
    public function getAge()
    {
        # code...
    }

    public function getFullName()
    {
        # code...
    }
}

$p = new Xujiajun();

var_dump(get_class_methods($p));

//输出
    array(2) {
      [0] =>
      string(6) "getAge"
      [1] =>
      string(11) "getFullName"
    }
```

注意：只有声明成`public`的方法才会显示哦。

如果我们要检测某一个方法是否存在，用以上这个`get_class_method`当然可以做到：

```php
if( in_array($method,get_class_methods($p)))
{
}
```

其实PHP有更加专业的工具:`method_exists`和`is_callable`,

example:

```php

//is_callable()
if (is_callable(array($p, "getAge"))) {
    echo $p->getAge(); // 18
}

//method_exists()
if (method_exists($p, "getAge")) {
    echo $p->getAge();// 18
}
```

注意以上两者区别：如果getAge方法改成private、protected,`is_callable`返回是false，而`method_exists`返回true

了解类属性
我们既然可以查询类的方法，当然我们也可以查询类的属性。PHP提供了`get_class_vars`函数，参数接收类名。

example:

```php

class Xujiajun
{
 public $age = "18";
}
var_dump(get_class_vars('Xujiajun'));

//输出结果
    array(1) {
      'age' =>
      string(2) "18"
    }
```

了解继承

类函数也允许我们绘制继承关系。我们可以用`get_parent_class()`来找到一个类的父类。参数为一个类名或者对象。

example:

```php

class Person
{
}
class Xujiajun extends Person
{
}
var_dump(get_parent_class(new Xujiajun));//string(6) "Person"

```
另外也可以用`is_subclass_of`来检测类是否是另一个类的派生类。它需要一个子类对象(或者类)和父类的名字。

example：

```php
var_dump(is_subclass_of('Xujiajun', 'Person'));//bool(true)

```

方法调用

比如现在我们要字符串动态调用某一个方法：

```php
$p = getPerson();//获取Person对象
$method = "getAge";//定义方法名
echo $p->$method();
```
其实，我们可以通过PHP提供的`call_user_func()`达到相同目的。

example:

```php
class Xujiajun
{
    public function getAge($age = 0)
    {
        return 18;
    }
}
var_dump(call_user_func(array(new Xujiajun,'getAge')));//18

//加参数
var_dump(call_user_func(array(new Xujiajun,'getAge'),2));//20
```
当然 `call_user_func_array()` 更加好用,使用上相同,参数支持数组传参。

<h5 id="reflect-api">4.3、反射API</h5>

<h5 id="reflect-intro">4.3.1、入门</h5>
PHP中的反射API就像Java中的java.lang.reflect包一样。它由一系列可以分析属性、方法和类内置类组成。

反射API部分列参考

类       |描述
---------|---------------------------------
Relection|为类的摘要信息提供静态函数export()
RelectionClass|类信息和工具
RelectionMethod|类方法信息和工具
RelectionParameter|方法参数信息
RelectionProperty|类属性信息
RelectionFunction|函数信息和工具
RelectionExcetion|错误类
RelectionExtension|PHP扩展信息

利用这些反射API的类，可以运行访问对象、函数和脚本中的扩展信息。反射API非常强大,我们应该经常使用API而少使用类和对象函数。

example:

```php

class Person
{
    public function getName()
    {
    }
}

class Xujiajun extends Person
{

    public $age = "18";

    public function getAge($arg = 0)
    {
        return 18+$arg;
    }
}

$reflector = new ReflectionClass('Xujiajun');
$properties = Reflection::export($reflector);
var_dump($properties);

//输出类似
    Class [ <user> class Xujiajun extends Person ] {
      @@ /private/var/www/demo/foo.php 11-25
    
      - Constants [0] {
      }
    
      - Static properties [0] {
      }
    
      - Static methods [0] {
      }
    
      - Properties [1] {
        Property [ <default> public $age ]
      }
    
      - Methods [2] {
        Method [ <user> public method getAge ] {
          @@ /private/var/www/demo/foo.php 16 - 19
    
          - Parameters [1] {
            Parameter #0 [ <optional> $arg = 0 ]
          }
        }
    
        Method [ <user, inherits Person> public method getName ] {
          @@ /private/var/www/demo/foo.php 5 - 8
        }
      }
    }
```
从例子中可以看出，Relection::export()提供了Xujiajun这个类的几乎所有信息。
如果我们直接var_dump()一个对象的话，前提要实例化它，而且也不会有细节提供。可见，反射API提供了更高层次的功能。

<h5 id="reflect-class">4.3.2、类检测</h5>

example：
```php
interface Person
{
    public function getName();
}

$reflector = new ReflectionClass('Person');

var_dump($reflector->isInterface());//bool(true)
```
<h5 id="reflect-method">4.3.3、检查方法</h5>

ReflectionClass我们用来检查类，那么检查类中的方法可以用`RelectionMethod`

获取`RelectionMethod`对象的方式有两种：

0、从RelectionClass::getMethods()获得RelectionMethod对象数组

1、如果是特定的类方法,RelectionClass::getMethod()接受一个方法名作为参数并返回相应的RelectionMethod对象。

example:

```php

class Xujiajun
{
    public function getName()
    {
        
    }
}
$reflector = new ReflectionClass('Xujiajun');
$methods = $reflector->getMethods();
var_dump($methods[0]->isPublic());//bool(true)
```
<h5 id="reflect-parameters">4.3.4、检查方法参数</h5>

在PHP5中声明类方法时可以限制参数中对象类型，因此检查方法的参数变得非常必要。

example:

```php
class Person
{
    public function __construct(Exception $a)
    {

    }
    public function getName()
    {

    }
}

$reflector = new ReflectionClass('Person');

$methods = $reflector->getMethod('__construct');
$params = $methods->getParameters();

foreach ($params as $key => $param) {
    echo argData($param);//$a must be a Foo object
}

function argData(ReflectionParameter $arg)
{
    $details = "";

    $name = $arg->getName();
    $class = $arg->getClass();
    if (!empty($class)) {
        $className = $class->getName();
        $details .= "\$$name must be a $className object\n";
    }

    return $details;
}
```

<h5 id="use-reflection-api">4.3.5、使用反射API</h5>

example：

```php

class Person
{
    public $name;

    public function __construct($name)
    {
        $this->name = $name;
    }
}

interface Module
{

}

class FtpModule implements Module
{
    function setHost($host)
    {
        echo "FtpModule:setHost: $host\n";
    }

    function setUser($user)
    {
        echo "FtpModule:setUser: $user\n";
    }

    function excute()
    {

    }
}

class  PersonModule implements Module
{
    function setPerson(Person $person)
    {
        echo "PersonModule::setPerson: {$person->name}\n";
    }

    function excute()
    {

    }
}

class ModuleRunner
{

    private $configData = array(
        'PersonModule' => array(
            'person' => 'anon'
        ),
        'FtpModule' => array(
            'host' => 'superu.org',
            'user' => 'xujiajun'
        )
    );

    public function init()
    {
        $interface = new ReflectionClass('Module');
        foreach ($this->configData as $moduleName => $params) {

            $moduleClass = new ReflectionClass($moduleName);
            if (!$moduleClass->isSubclassOf($interface)) {
                throw new Exception("unknow module type: $moduleClass");
            }

            $module = $moduleClass->newInstance();
            foreach ($moduleClass->getMethods() as $method) {
                $this->handleMethod($module,$method,$params);
            }
        }

    }

    private function handleMethod(Module $module, ReflectionMethod $method, $params)
    {
        $name = $method->getName();
        $args = $method->getParameters();

        if (substr($name, 0,3) != 'set' or count($args) != 1) {
            return false;
        }

        $property = strtolower(substr($name,3));
        if (!isset($params[$property])) {
            return false;
        }

        $argClass = $args[0]->getClass();
        if (empty($argClass)) {
            $method->invoke($module,$params[$property]);
        } else {
            $method->invoke($module,$argClass->newInstance($params[$property]));
        }
    }

}

$test = new ModuleRunner();
$test->init();

//输出:
// PersonModule::setPerson: anon
// FtpModule:setHost: superu.org
// FtpModule:setUser: xujiajun
```
<h2 id="object-design">5、对象与设计</h2>

<h5 id="diff-object-process">5.1、面向对象设计和过程式编程</h5>

Q:面向对象和传统的过程式编程有声明不同呢？很多人认为不同之处是OOP包含对象？

A:事实上这种说法并不准确,在PHP,你经常发现过程式编程也使用对象，也会出现类中包含过程式代码的情况。类的出现并不能说明使用了面向对象设计,面向对象和过程式一个核心区别是如何分配职责。

example:

```php
//读取key:value

funciton readParams($sourceFile)
{
    $params = array();
    //code...
    return params;
}

function writeParams($params,$sourseFile)
{
    //写入文本参数到sourseFile
}

$file = "./xujiajun.txt";
$array['key1'] = "xujiajun";
$array['key2'] = "徐佳军";

writeParams($array,$file);
$output = readParams($file);
print_r($output);

```
这段代码较为紧凑且容易维护。

现在我们被告知这个工具支持如下所有所示的XML格式：

```XML
<params>
    <param>
        <key>my key</key>
        <key>my val</key>
    </param>
</params>

```
如果参数文件以.xml结尾，就应该以XML模式读取参数文件。这个时候，我们有两个办法：
①在控制代码中检查文件的扩展名
②在读写函数中检测

这里我们选择第二种:

```PHP

function readParams($source)
{
    $params = array();
    if(preg_match("/\.xml$/i",$source)){
        //从source读XML参数
    } else {
        //从source读文本参数
    }
}

function writeParams($params,$sourse)
{
    if(preg_match("/\.xml$/i",$source)){
        //写入XML参数到$source
    } else {
        //写入文本参数到$source
    }
}
```

我们在两个函数中都要检测XML的扩展名,这样的重复性代码会产生问题。如果我们还要支持其他格式的参数，就要始终保持readParams()和WriteParams函数的一致性。

那么，我们用类来解决看看:

```php
abstract class ParamHandle
{
    protected $source;
    protected $params = array();
    
    function __construct($source)
    {
        $this->source = $source;
    }
    
    function addParam($key,$val)
    {
        $this->params[$key] = $val;
    }
    
    function getAllParams()
    {
        return $this->params;
    }
    
    static function getInstance($filename)
    {
        if(preg_match("/\.xml$/i",$filename)){
            return new XmlParamHander($filename);
        }
        
        return new TextParamHander($filename);
    }
    
    abstract function write();
    abstract function read();
}

//Xml
class XmlParamHander extends ParamHander
{
    function write()
    {
    }
    
    function read()
    {
    }
}

//Text
class TextParamHander extends ParamHander
{
    function write()
    {
    }
    
    function read()
    {
    }
}
```
这些类简单地提供了write()和read()方法的实现。每个类都根据适当的文件格式进行读写。

```php

//Xml
$test = ParamHander::getInstance("./xujiajun.xml");
$test->addParam("key1","val1");
$test->write();

//Text
$test = ParamHander::getInstance("./xujiajun.text");
$test->read();
```
<h5 id="choose-object">5.2、定义类</h5>

定义类的界限往往比我们想象更加困难，特别是系统不断发展时,最好的办法是分清职责。但是注意设计原则并不是一成不变的。

<h5 id="polymorphism">5.3、多态</h5>

多态或称“类切面”是面向对象系统的基本特征之一。

example:

```php
//获取摘要
function getSummary()
{
    $base = "$this->title: $this->name";
    if ($this->type == 'book'){
        $base .= 'pageCount: $this->pageNum';
    } else if ($this->type = 'cd'){
        $base .= 'Playing Time: $this->playLength';
    }
}

//写到这里，看出什么来了吗？暗示我们有两个子类原型`CdProduct`和`BookProduct`
```

<h5 id="encapsulation">5.4、封装</h5>

简单来说，封装就是对客户端代码隐藏数据和功能。封装也是面向对象的重要概念之一。

要实现封装，最简单的办法是将属性定义为private或者protected。通过对客户端代码隐藏属性，我们创建了一个接口并防止在偶然情况下污染对象中的数据。

多态是另外一种封装。
