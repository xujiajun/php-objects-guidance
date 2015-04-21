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

<h5 id="program-interface">5.5、忘记细节</h5>

Gang of Four 在《设计模式》总结了这个规则:

`为接口而不是实现而编程(Program to interface,not an implementation)`

