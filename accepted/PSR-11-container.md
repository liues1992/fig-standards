# 容器接口

此文描述了依赖注入容器的通用接口。

`ContainerInterface`的目标：制定PHP框架和库中，从容器获得对象和参数的的标准（在此文中叫做条目`entry`）。

以下关键词的定义和[RFC 2119][]保持一致： 必须（"MUST"）, 不能（"MUST NOT"）, 必须（"REQUIRED"）, 应该（"SHALL"）, 不应该（"SHALL NOT"）, 应该（"SHOULD"）,
不应该（"SHOULD NOT"）, 推荐（"RECOMMENDED"）, 可以（"MAY"）, 可选（"OPTIONAL"）

`实现者`（`implementor`）指的是任何一个实现了 `ContainerInterface` 的依赖注入相关的框架和类库。`用户`（`user`）指的是依赖注入容器（DIC）的使用者。

[RFC 2119]: http://tools.ietf.org/html/rfc2119

## 1. 规范

### 1.1 基础说明

#### 1.1.1 条目标识符

一个条目表示符是一个合法的PHP字符串，长度至少为1，在一个容器实例中唯一表示了一条数据。条目标识符对容器调用者是不透明的，也就是说调用者**不应该（SHOULD NOT）**假设字符串有任何语法结构。

#### 1.1.2 从容器中读取数据

- `Psr\Container\ContainerInterface` 暴露两个方法：`get` 和 `has`。
- `get`严格接收一个参数：一个 **必须（MUST）** 是字符串的条目标识符。
  `get`可以返回任何值，在容器条目未找到时，抛出一个`NotFoundExceptionInterface`异常。两次连续的`get`调用 **应该（SHOULD）** 返回同样的值，但是根据实现者或者用户的配置，返回不同的值也是可能的，所以用户 **不应该（SHOULD NOT）** 依赖两次调用返回相同值的行为。

- `has` takes one unique parameter: an entry identifier, which MUST be a string.
  `has` MUST return `true` if an entry identifier is known to the container and `false` if it is not.
  If `has($id)` returns false, `get($id)` MUST throw a `NotFoundExceptionInterface`.
- `has`严格接收一个参数：一个**必须（MUST）**是字符串的条目标识符。

### 1.2 异常

容器所抛出的异常**应该（SHOULD）**实现
[`Psr\Container\ContainerExceptionInterface`](#container-exception).

`get`被调用，而条目未找到时，**必须（MUST）**抛出一个实现了此接口的异常：
[`Psr\Container\NotFoundExceptionInterface`](#not-found-exception).

### 1.3 推荐用法

Users SHOULD NOT pass a container into an object so that the object can retrieve *its own dependencies*.
This means the container is used as a [Service Locator](https://en.wikipedia.org/wiki/Service_locator_pattern)
which is a pattern that is generally discouraged.

Please refer to section 4 of the META document for more details.

## 2. 包

The interfaces and classes described as well as relevant exceptions are provided as part of the
[psr/container](https://packagist.org/packages/psr/container) package.

Packages providing a PSR container implementation should declare that they provide `psr/container-implementation` `1.0.0`.

Projects requiring an implementation should require `psr/container-implementation` `1.0.0`.

## 3. 接口定义

<a name="container-interface"></a>
### 3.1. `Psr\Container\ContainerInterface`

~~~php
<?php
namespace Psr\Container;

/**
 * Describes the interface of a container that exposes methods to read its entries.
 */
interface ContainerInterface
{
    /**
     * Finds an entry of the container by its identifier and returns it.
     *
     * @param string $id Identifier of the entry to look for.
     *
     * @throws NotFoundExceptionInterface  No entry was found for **this** identifier.
     * @throws ContainerExceptionInterface Error while retrieving the entry.
     *
     * @return mixed Entry.
     */
    public function get($id);

    /**
     * Returns true if the container can return an entry for the given identifier.
     * Returns false otherwise.
     *
     * `has($id)` returning true does not mean that `get($id)` will not throw an exception.
     * It does however mean that `get($id)` will not throw a `NotFoundExceptionInterface`.
     *
     * @param string $id Identifier of the entry to look for.
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


