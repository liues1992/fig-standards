# PHP 规范建议

根据[PSR工作章程][workflow]，每个PSR都有一个状态。一个提案通过“准入投票”后被列为“草案”。只要PSR的状态不是“已接受”，就可以进行更改。“草案”状态可以大幅度改动，但是“评审中”状态只能有小幅改动。

如[PSR工作章程][workflow]所述，提案的“编辑”是PSR的主要贡献者，他们需要得到两个投票成员的支持。一个作为“协助者”负责管理评审以及投票进程，一个作为“支持者”。

## 状态索引

### 已接受

| 编号 | 标题                          | 编辑                         |  Coordinator            | Sponsor          |
|:---:|--------------------------------|--------------------------------|-------------------------|------------------|
| 1   | [基本编码规范][psr1]  | Paul M. Jones                  | _N/A_                   | _N/A_            |
| 2   | [编码风格指南][psr2]     | Paul M. Jones                  | _N/A_                   | _N/A_            |
| 3   | [日志接口][psr3]       | Jordi Boggiano                 | _N/A_                   | _N/A_            |
| 4   | [自动加载规范][psr4]   | Paul M. Jones                  | Phil Sturgeon           | Larry Garfield   |
| 6   | [缓存接口][psr6]      | Larry Garfield                 | Paul Dragoonis          | Robert Hafner    |
| 7   | [HTTP消息接口][psr7] | Matthew Weier O'Phinney        | Beau Simensen           | Paul M. Jones    |
| 11  | [容器接口][psr11]   | Matthieu Napoli, David Négrier | Matthew Weier O'Phinney | Korvin Szanto    |
| 13  | [超媒体链接][psr13]      | Larry Garfield                 | Matthew Weier O'Phinney | Marc Alexander   |
| 15  | [HTTP处理器][psr15]         | Woody Gilk                     | _N/A_                   | Matthew Weier O'Phinney |
| 16  | [简单缓存][psr16]          | Paul Dragoonis                 | Jordi Boggiano          | Fabien Potencier |

### 评审中

| 编号 | 标题                                | 编辑                     |
|:---:|--------------------------------------|--------------------------------|
| 12  | [扩展编码风格指南][psr12] | Korvin Szanto                  |

### 草稿阶段

| 编号 | 标题                                | 编辑                     |
|:---:|--------------------------------------|--------------------------------|
| 17  | [HTTP工厂][psr17]              | Woody Gilk                     |
| 18  | [HTTP客户端][psr18]                 | Tobias Nylhom                  |

### 已丢弃

| 编号 | 标题                                | 编辑                      |
|:---:|--------------------------------------|--------------------------------|
| 5   | [PHPDoc规范][psr5]              | Mike van Riel                  |
| 8   | [Huggable Interface][psr8]           | Larry Garfield                 |
| 9   | [Security Advisories][psr9]          | Michael Hess                   |
| 10  | [Security Reporting Process][psr10]  | Michael Hess                   |
| 14  | [事件管理器][psr14]               | Chuck Reeves                   |

### 已废弃

| 编号 | 标题                          | 编辑                  |
|:---:|--------------------------------|-------------------------|
| 0   | [自动加载规范][psr0]   | Matthew Weier O'Phinney |

## 编号索引

| 状态 | 编号 | Title                                | 编辑                      |
|--------|:---:|--------------------------------------|--------------------------------|
| X      | 0   | [自动加载规范][psr0]         | Matthew Weier O'Phinney        |
| A      | 1   | [基本编码规范][psr1]        | Paul M. Jones                  |
| A      | 2   | [编码风格指南][psr2]           | Paul M. Jones                  |
| A      | 3   | [日志接口][psr3]             | Jordi Boggiano                 |
| A      | 4   | [自动加载标准][psr4]         | Paul M. Jones                  |
| B      | 5   | [PHPDoc规范][psr5]              | Mike van Riel                  |
| A      | 6   | [缓存接口][psr6]            | Larry Garfield                 |
| A      | 7   | [HTTP消息接口][psr7]       | Matthew Weier O'Phinney        |
| B      | 8   | [Huggable Interface][psr8]           | Larry Garfield                 |
| B      | 9   | [Security Advisories][psr9]          | Michael Hess                   |
| B      | 10  | [Security Reporting Process][psr10]  | Michael Hess                   |
| A      | 11  | [容器接口][psr11]         | Matthieu Napoli, David Négrier |
| R      | 12  | [扩展编码风格指南][psr12] | Korvin Szanto                  |
| A      | 13  | [超媒体链接][psr13]            | Larry Garfield                 |
| B      | 14  | [事件管理][psr14]               | Chuck Reeves                   |
| A      | 15  | [HTTP处理器][psr15]               | Woody Gilk                     |
| A      | 16  | [简单缓存][psr16]                | Paul Dragoonis                 |
| D      | 17  | [HTTP工厂][psr17]              | Woody Gilk                     |
| D      | 18  | [HTTP客户端][psr18]                 | Tobias Nyholm                  |

**说明:** A = 已接受（Accepted） | D = 草案（Draft） | R = 评审（Review） | X = 已废弃（Deprecated） | B = 已丢弃（Abandoned）

[workflow]: https://github.com/liues1992/fig-standards/blob/master/bylaws/002-psr-workflow.md
[psr0]: https://github.com/liues1992/fig-standards/blob/master/accepted/PSR-0.md
[psr1]: https://github.com/liues1992/fig-standards/blob/master/accepted/PSR-1-basic-coding-standard.md
[psr2]: https://github.com/liues1992/fig-standards/blob/master/accepted/PSR-2-coding-style-guide.md
[psr3]: https://github.com/liues1992/fig-standards/blob/master/accepted/PSR-3-logger-interface.md
[psr4]: https://github.com/liues1992/fig-standards/blob/master/accepted/PSR-4-autoloader-meta.md
[psr5]: https://github.com/phpDocumentor/fig-standards/tree/master/proposed/phpdoc.md
[psr6]: https://github.com/liues1992/fig-standards/blob/master/accepted/PSR-6-cache.md
[psr7]: https://github.com/liues1992/fig-standards/blob/master/accepted/PSR-7-http-message.md
[psr8]: https://github.com/liues1992/fig-standards/blob/master/proposed/psr-8-hug/
[psr9]: https://github.com/liues1992/fig-standards/blob/master/proposed/security-disclosure-publication.md
[psr10]: https://github.com/liues1992/fig-standards/blob/master/proposed/security-reporting-process.md
[psr11]: https://github.com/liues1992/fig-standards/blob/master/accepted/PSR-11-container.md
[psr12]: https://github.com/liues1992/fig-standards/blob/master/proposed/extended-coding-style-guide.md
[psr13]: https://github.com/liues1992/fig-standards/blob/master/accepted/PSR-13-links.md
[psr14]: https://github.com/liues1992/fig-standards/blob/master/proposed/event-manager.md
[psr15]: https://github.com/liues1992/fig-standards/blob/master/accepted/PSR-15-request-handlers.md
[psr16]: https://github.com/liues1992/fig-standards/blob/master/accepted/PSR-16-simple-cache.md
[psr17]: https://github.com/liues1992/fig-standards/tree/master/proposed/http-factory/
[psr18]: https://github.com/liues1992/fig-standards/tree/master/proposed/http-client/


