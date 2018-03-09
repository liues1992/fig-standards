自动加载规范
====================

> **已废弃** - PSR-0在2014年10月21日被废弃。现在推荐使用[PSR-4]作为替代品。

[PSR-4]: http://www.php-fig.org/psr/psr-4/

本文描述了通用自动加载器 (autoloader) 必须遵循的规范。

规范说明
---------

* 完全限定的命名空间和类**必须**遵循这样的结构：`\<组织名称>\(<命名空间>\)*<类名>`
* 命名空间**必须**包含一个`组织名称`作为顶级命名空间。
* 命名空间**可以**有多个子命名空间。
* 当从文件系统加载相应文件时，命名空间分隔符会被转换为`DIRECTORY_SEPARATOR`（文件系统中的目录分隔符）。
* **类名**中的下划线（`_`）会被转换为`DIRECTORY_SEPARATOR`（文件系统中的目录分隔符）。命名空间中的下划线(`_`)没有特殊含义。
* 当从文件系统加载相应完全限定的命名空间和类时，会加上一个`.php`后缀。
* `组织名称`, `命名空间`, 和 `类名`中的字母可以是大写或者小写。

示例
--------

* `\Doctrine\Common\IsolatedClassLoader` => `/path/to/project/lib/vendor/Doctrine/Common/IsolatedClassLoader.php`
* `\Symfony\Core\Request` => `/path/to/project/lib/vendor/Symfony/Core/Request.php`
* `\Zend\Acl` => `/path/to/project/lib/vendor/Zend/Acl.php`
* `\Zend\Mail\Message` => `/path/to/project/lib/vendor/Zend/Mail/Message.php`

命名空间和类名中的下划线
-----------------------------------------

* `\namespace\package\Class_Name` => `/path/to/project/lib/vendor/namespace/package/Class/Name.php`
* `\namespace\package_name\Class_Name` => `/path/to/project/lib/vendor/namespace/package_name/Class/Name.php`


这里设定的规范是保证自动加载器互通性的最低标准规范。你可以用下述的SplClassLoader样例来检测你自己的实现是否遵循规范。

代码实现示例
----------------------

以下示例函数展示了如何按照规范进行自动加载。

~~~php
<?php

function autoload($className)
{
    $className = ltrim($className, '\\');
    $fileName  = '';
    $namespace = '';
    if ($lastNsPos = strrpos($className, '\\')) {
        $namespace = substr($className, 0, $lastNsPos);
        $className = substr($className, $lastNsPos + 1);
        $fileName  = str_replace('\\', DIRECTORY_SEPARATOR, $namespace) . DIRECTORY_SEPARATOR;
    }
    $fileName .= str_replace('_', DIRECTORY_SEPARATOR, $className) . '.php';

    require $fileName;
}
spl_autoload_register('autoload');
~~~

SplClassLoader 示例
-----------------------------

以下gist是一个SplClassLoader示例，如果你遵循了规范，可以用它实现自动加载类文件。这是目前推荐的PHP 5.3的类文件载入方式。

* [http://gist.github.com/221634](http://gist.github.com/221634)

