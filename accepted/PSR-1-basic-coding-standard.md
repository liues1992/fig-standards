# 基础代码规范

此规范包含了一些基本编码要素，以便共享的 PHP 代码 能代码实现高度技术互通性。

以下关键词的定义和 [RFC 2119][] 保持一致： 必须（MUST）, 不能（MUST NOT）, 必须（REQUIRED）, 应该（SHALL）, 不应该（SHALL NOT）, 应该（SHOULD）,
不应该（SHOULD NOT）, 推荐（RECOMMENDED）, 可以（MAY）, 可选（OPTIONAL）。

[RFC 2119]: http://www.ietf.org/rfc/rfc2119.txt
[PSR-0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
[PSR-4]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md

## 1. 概述

- 文件**必须（MUST）**只使用 `<?php` 和 `<?=` 标签.

- PHP代码文件**必须（MUST）**只使用不带BOM的UTF-8编码。

- 一个文件 **应该** 要么声明符号（类，函数，常量等），要么产生副作用（例如产生输出，改变 .ini 配置），但是 **不应该** 两者都做。

- 命名空间和类**必须**遵循自动加载规范[[PSR-0], [PSR-4]]。

- 类名**必须**是首字母大写驼峰式（`StudlyCaps`）命名。

- 类常量**必须**是全大写，用下划线分开。

- 方法**必须**x是首字母小写驼峰式（`camelCase`）命名。

## 2. 文件

### 2.1. PHP标签

PHP 代码**必须**使用长标签 `<?php ?>` 或者短标签 `<?= ?>`，**不能** 使用其他标签变种。

### 2.2. 字符编码

PHP 代码**必须**使用不带 BOM 的 UTF-8 编码。

### 2.3. 副作用

一个文件要么声明新符号（类，函数，常量等），要么执行产生副作用的逻辑，但是 **不应该** 两者都做。

「副作用」 意味着逻辑的执行和类，方法，常量没有直接关联，例如，*只在include这个文件时执行逻辑。*

「副作用」 包括但不限于：产生输出，显式地使用 `require` 或者 `include`，连接外部服务，修改ini设置，产生错误或者异常，修改全局变量或者静态变量，读写文件等等。

以下是一个既有声明又有副作用的例子，应当是尽量避免的。

~~~php
<?php
// 副作用：改变 ini 设置
ini_set('error_reporting', E_ALL);

// 副作用：加载一个文件
include "file.php";

// 副作用：产生输出
echo "<html>\n";

// 声明
function foo()
{
    // 函数体
}
~~~

以下是一个文件只有声明没有副作用的例子。可以作为一个范例。

~~~php
<?php
// 声明
function foo()
{
    // 函数体
}

// 条件性声明 *不是* 副作用
if (! function_exists('bar')) {
    function bar()
    {
        // 函数体
    }
}
~~~

## 3. 命名空间和类名

Namespaces and classes MUST follow an "autoloading" PSR: [[PSR-0], [PSR-4]].

This means each class is in a file by itself, and is in a namespace of at
least one level: a top-level vendor name.

Class names MUST be declared in `StudlyCaps`.

Code written for PHP 5.3 and after MUST use formal namespaces.

For example:

~~~php
<?php
// PHP 5.3 及以后:
namespace Vendor\Model;

class Foo
{
}
~~~

Code written for 5.2.x and before SHOULD use the pseudo-namespacing convention
of `Vendor_` prefixes on class names.

~~~php
<?php
// PHP 5.2.x 及以前:
class Vendor_Model_Foo
{
}
~~~

## 4. 类的常量属性和方法

The term "class" refers to all classes, interfaces, and traits.
术语『类』包括class，interface 和 trait。

### 4.1. 常量

类常量**必须**是全部大写，下划线作为分隔符。
例如：

~~~php
<?php
namespace Vendor\Model;

class Foo
{
    const VERSION = '1.0';
    const DATE_APPROVED = '2012-06-01';
}
~~~

### 4.2. 属性

这个指南刻意没有去规定属性的命名风格应该是大写驼峰 (`$StudlyCaps`)，小写驼峰 (`$camelCase`) 还是下划线 (`$under_score`)。

但是不管是什么命名风格，**应该**在一定范围内保持一致。这个范围可以是组织名称级别，包级别，类级别或者方法级别。

### 4.3. 方法

方法名必须是首字母小写驼峰式`camelCase()`。


