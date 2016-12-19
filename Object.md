##导航

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
  public $firstName = "Super";
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
echo $product1->firstName." ".$product1->secondName; //super U
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
  public $firstName = "Super";
  public $secondName = "U";
  
  //注意类方法也可以声明成public\protected\private
  public function getFullName()
  {
     return  $product1->firstName." ".$product1->secondName; 
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
$product2->firstName = "Super2"
$product2->secondName = "U2";
echo $product2->getFullName();

$product3 = new ShopProduct();
$product3->firstName = "Super3"
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
  public $firstName = "Super";
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
  public $firstName = "Super";
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
