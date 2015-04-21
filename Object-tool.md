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