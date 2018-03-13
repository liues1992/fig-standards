# 容器接口

此文描述了依赖注入容器的通用接口。

`ContainerInterface`的目标：制定PHP框架和库中，从容器获得对象和参数的的标准（在此文中叫做条目`entry`）。

以下关键词的定义和[RFC 2119][]保持一致： 必须（MUST）, 不能（MUST NOT）, 必须（REQUIRED）, 应该（SHALL）, 不应该（SHALL NOT）, 应该（SHOULD）,
不应该（SHOULD NOT）, 推荐（RECOMMENDED）, 可以（MAY）, 可选（OPTIONAL）

`实现者`（`implementor`）指的是任何一个实现了 `ContainerInterface` 的依赖注入相关的框架和类库。`用户`（`user`）指的是依赖注入容器（DIC）的使用者。

[RFC 2119]: http://tools.ietf.org/html/rfc2119

## 1. 规范

### 1.1 基础说明

#### 1.1.1 条目标识符

一个条目标识符是一个合法的PHP字符串，长度至少为1，在一个容器实例中唯一标识一条数据。条目标识符对容器调用者是不透明的，也就是说调用者**不应该（SHOULD NOT）**假设字符串有任何语法结构。

#### 1.1.2 从容器中读取数据

- `Psr\Container\ContainerInterface` 暴露两个方法：`get` 和 `has`。
- `get`严格接收一个参数：一个 **必须（MUST）** 是字符串的条目标识符。
 `get`可以返回任何值，条目未在容器中找到时，抛出一个`NotFoundExceptionInterface`异常。两次连续的`get`调用 **应该（SHOULD）** 返回同样的值，但是根据实现者或者用户的配置，返回不同的值也是可能的，所以用户 **不应该（SHOULD NOT）** 依赖两次调用返回相同值的行为。

- `has` 严格接收一个参数：一个**必须（MUST）**是字符串的条目标识符。
  对应的条目在容器中存在时，`has` **必须（MUST）** 返回`true`，否则返回`false`。
  如果`has($id)`返回false，`get($id)` **必须（MUST）** 抛出`NotFoundExceptionInterface`异常。

### 1.2 异常

容器所抛出的异常**应该（SHOULD）**实现
[`Psr\Container\ContainerExceptionInterface`](#container-exception).

`get`被调用，而条目未找到时，**必须（MUST）**抛出一个实现了此接口的异常：
[`Psr\Container\NotFoundExceptionInterface`](#not-found-exception).

### 1.3 推荐用法

用户 **不应该（SHOULD NOT）** 把容器传给对象，让对象自行去取*它的依赖*，
这样的话容器就被用作了[服务定位器](https://en.wikipedia.org/wiki/Service_locator_pattern)，而这种模式一般是不推荐使用的。

请参照元文档的第四部分了解更多详情。

## 2. 包

相关的接口，类和异常都包含在了此软件包中：
[psr/container](https://packagist.org/packages/psr/container) 

提供PSR容器实现的包应该声明他们提供了`psr/container-implementation` `1.0.0`。

需要容器实现的项目应该require `psr/container-implementation` `1.0.0`。

## 3. 接口定义

<a name="container-interface"></a>
### 3.1. `Psr\Container\ContainerInterface`

~~~php
<?php
namespace Psr\Container;

/**
 * 容器接口暴露的读取条目的方法
 */
interface ContainerInterface
{
    /**
     * 根据标识符找到返回条目。
     *
     * @param string $id 条目标识符
     *
     * @throws NotFoundExceptionInterface  找不到这个标识符对应的条目。
     * @throws ContainerExceptionInterface 取条目时发生的错误。
     *
     * @return mixed 条目
     */
    public function get($id);

    /**
     * 如果能在容器中找到标识符对应的条目，返回true，否则返回false
     *
     * `has($id)` 返回true不意味着`get($id)`不会抛异常，
     * 但是保证`get($id)`不会抛`NotFoundExceptionInterface`异常。
     *
     * @param string $id 条目标识符。
     *
     * @return bool
     */
    public function has($id);
}
~~~

<a name="container-exception"></a>
### 3.2. `Psr\Container\ContainerExceptionInterface`

~~~php
<?php
namespace Psr\Container;

/**
 * 容器中的发生的异常的所遵循的接口
 */
interface ContainerExceptionInterface
{
}
~~~

<a name="not-found-exception"></a>
### 3.3. `Psr\Container\NotFoundExceptionInterface`

~~~php
<?php
namespace Psr\Container;

/**
 * 条目在容器中未找到
 */
interface NotFoundExceptionInterface extends ContainerExceptionInterface
{
}
~~~


