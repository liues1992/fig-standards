# 基础代码规范

This section of the standard comprises what should be considered the standard
coding elements that are required to ensure a high level of technical
interoperability between shared PHP code.

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD",
"SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be
interpreted as described in [RFC 2119].

[RFC 2119]: http://www.ietf.org/rfc/rfc2119.txt
[PSR-0]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-0.md
[PSR-4]: https://github.com/php-fig/fig-standards/blob/master/accepted/PSR-4-autoloader.md

## 1. 概述

- 文件**必须（MUST）**只使用 `<?php` 和 `<?=` 标签.

- PHP代码文件**必须（MUST）**只使用不带BOM的UTF-8编码。

- Files SHOULD *either* declare symbols (classes, functions, constants, etc.)
  *or* cause side-effects (e.g. generate output, change .ini settings, etc.)
  but SHOULD NOT do both.

- 命名空间和类**必须（MUST）**遵循自动加载规范[[PSR-0], [PSR-4]]。

- 类名**必须（MUST）**是首字母大写驼峰式（`StudlyCaps`）命名。

- 类常量**必须**是全大写，用下划线分开。

- 方法**必须**x是首字母小写驼峰式（`camelCase`）命名。

## 2. 文件

### 2.1. PHP标签

PHP code MUST use the long `<?php ?>` tags or the short-echo `<?= ?>` tags; it
MUST NOT use the other tag variations.

### 2.2. 字符编码

PHP code MUST use only UTF-8 without BOM.

### 2.3. 副作用

A file SHOULD declare new symbols (classes, functions, constants,
etc.) and cause no other side effects, or it SHOULD execute logic with side
effects, but SHOULD NOT do both.

The phrase "side effects" means execution of logic not directly related to
declaring classes, functions, constants, etc., *merely from including the
file*.

"Side effects" include but are not limited to: generating output, explicit
use of `require` or `include`, connecting to external services, modifying ini
settings, emitting errors or exceptions, modifying global or static variables,
reading from or writing to a file, and so on.

The following is an example of a file with both declarations and side effects;
i.e, an example of what to avoid:

~~~php
<?php
// side effect: change ini settings
ini_set('error_reporting', E_ALL);

// side effect: loads a file
include "file.php";

// side effect: generates output
echo "<html>\n";

// declaration
function foo()
{
    // function body
}
~~~

The following example is of a file that contains declarations without side
effects; i.e., an example of what to emulate:

~~~php
<?php
// declaration
function foo()
{
    // function body
}

// conditional declaration is *not* a side effect
if (! function_exists('bar')) {
    function bar()
    {
        // function body
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

### 4.1. 常量

For example:
类常量**必须（MUST）**是全部大写，下划线作为分隔符。
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

This guide intentionally avoids any recommendation regarding the use of
`$StudlyCaps`, `$camelCase`, or `$under_score` property names.

Whatever naming convention is used SHOULD be applied consistently within a
reasonable scope. That scope may be vendor-level, package-level, class-level,
or method-level.

### 4.3. 方法

方法名必须是首字母小写驼峰式`camelCase()`。


