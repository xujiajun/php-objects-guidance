##导航

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
