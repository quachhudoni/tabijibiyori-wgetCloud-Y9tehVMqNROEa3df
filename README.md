[合集 - CAP(29)](https://github.com)

[1.聊聊分布式事务，再说说解决方案2017-10-17](https://github.com/savorboard/p/distributed-system-transaction-consistency.html)[2.CAP 8.0 版本发布通告 - CAP 7岁生日快乐！2023-12-21](https://github.com/savorboard/p/cap-8-0.html)[3.CAP 7.2 版本发布通告2023-08-08](https://github.com/savorboard/p/cap-7-2.html)[4.CAP 7.1 版本发布通告2023-03-06](https://github.com/savorboard/p/cap-7-1.html)[5.CAP 7.0 版本发布通告 - 支持延迟消息，性能炸了？2022-11-28](https://github.com/savorboard/p/cap-7-0.html)[6.CAP 6.2 版本发布通告2022-09-19](https://github.com/savorboard/p/cap-6-2.html)[7.CAP 6.1 版本发布通告2022-06-10](https://github.com/savorboard/p/cap-6-1.html)[8.CAP 6.0 版本发布通告 - 支持 OpenTelemetry2022-01-07](https://github.com/savorboard/p/cap-6-0.html)[9.CAP 5.2 版本发布通告2021-11-16](https://github.com/savorboard/p/cap-5-2.html)[10.CAP 5.1 版本发布通告 - 你期待的 Redis 来了2021-06-08](https://github.com/savorboard/p/cap-5-1.html)[11.CAP 5.0 版本发布通告2021-03-29](https://github.com/savorboard/p/cap-5-0.html)[12.CAP 3.1 版本发布通告2020-08-17](https://github.com/savorboard/p/cap-3-1.html)[13.CAP 3.0 版本发布通告2020-01-06](https://github.com/savorboard/p/cap-3-0.html)[14.CAP 2.6 版本发布通告2019-08-29](https://github.com/savorboard/p/cap-2-6.html)[15.CAP 2.5 版本发布通告2019-04-01](https://github.com/savorboard/p/cap-2-5.html)[16.CAP 2.4版本发布通告 - 支持版本隔离特性2019-01-07](https://github.com/savorboard/p/cap-2-4.html)[17.CAP 2.3版本发布通告 - 支持 MongoDB2018-08-31](https://github.com/savorboard/p/cap-2-3.html)[18..NET Core 事件总线,分布式事务解决方案：CAP2017-07-21](https://github.com/savorboard/p/cap.html):[狗急跳墙加速](https://goujijs.com)[19.CAP 介绍及使用【视频】2017-07-27](https://github.com/savorboard/p/7243609.html)[20.招募：Wiki 文档翻译小伙伴招募2018-03-08](https://github.com/savorboard/p/8528124.html)[21.分布式事务,EventBus 解决方案:CAP【中文文档】2017-08-07](https://github.com/savorboard/p/cap-document.html)[22.在 CAP 中使用 AOP ( Castle.DynamicProxy )2021-01-05](https://github.com/savorboard/p/cap-castle.html)[23.如何在你的项目中集成 CAP【手把手视频教程】2018-09-13](https://github.com/savorboard/p/cap-video-1.html)[24.在 ASP.NET Core 中自动启用 CAP 事务2021-10-09](https://github.com/savorboard/p/cap-auto-transaction.html)[25.CAP 8.1 版本发布通告2024-04-17](https://github.com/savorboard/p/18139824/cap-8-1)[26.CAP 8.2 版本发布通告2024-06-26](https://github.com/savorboard/p/18268210/cap-8-2)[27.一文带你了解CAP的全部特性，你学会了吗？2024-07-31](https://github.com/savorboard/p/18333869/cap-features)[28.CAP 8.3 版本发布通告2024-10-14](https://github.com/savorboard/p/18464574/cap-8-3)

29.CAP 8.4 版本发布通告09-30

收起

### 前言

今天，我们很高兴宣布 CAP 发布 8.4 版本正式版。从 8.3.0 版本以来，我们陆续发布了 5 个小版本，在这些版本中我们主要专注于提升系统性能、增强 Dashboard 功能、改进存储提供程序支持，并修复了一系列已知问题。

下面，让我们具体看一下这些版本带来的新特性和改进。

### 总览

可能有些人还不知道 CAP 是什么，老规矩来一个简介。

[CAP](https://github.com) 是一个用来解决微服务或者分布式系统中分布式事务问题的一个开源项目解决方案（[https://github.com/dotnetcore/CAP](https://github.com)）同样可以用来作为 EventBus 使用，该项目诞生于2016年，目前在 Github 已经有超过 6000+ Star 和 100+ 贡献者，以及在 NuGet超 1100 万的下载量，并在越来越多公司的和项目中得到应用。

如果你想对 CAP 更多了解，请查看我们的 [官方文档](https://github.com)。

在 8.3.1 到 8.4.0 版本中，我们主要带来了以下改进：

* 消息调度性能优化与可靠性提升
* Dashboard 操作体验增强
* 存储提供程序支持改进
* 消息传输层优化
* BUG 修复

### 消息调度性能优化与可靠性提升

**背景**：在分布式系统中，消息的调度和处理是核心环节。随着业务量的增长，如何高效、可靠地处理大量延迟消息和队列消息成为了关键挑战。

**SchedulerBatchSize 配置项** (#1689)

在 8.4.0 版本中，我们新增了 `SchedulerBatchSize` 配置选项，用于指定每个调度循环中获取的延迟或队列消息的最大数量。这使开发者能够根据实际硬件资源和业务负载精细调整调度器的处理能力，避免单次处理过多消息导致的内存压力。

**线程安全的消息调度机制** (#1638)

在 8.3.3 版本中，我们重构了消息调度机制，使其完全线程安全。这一改进解决了在高并发场景下可能出现的竞态条件问题，确保了消息调度的稳定性和数据一致性。同时，我们添加了相关的单元测试，进一步保障了代码质量。

**FlushAsync 函数引入** (#1629)

8.3.3 版本引入了 `FlushAsync` 函数，该函数在 `CommitAsync` 中使用 await 关键字调用。这确保了在事务提交时，所有待处理的消息都能被正确刷新到存储中，提高了数据持久化的可靠性。

**MongoDB 锁获取可靠性提升** (#1722)

在 8.4.0 版本中，我们改进了 MongoDB 锁获取机制，通过减少回滚错误显著提高了分布式锁的可靠性。这在使用 MongoDB 作为存储时，能够更好地处理高并发下的资源竞争问题。

### Dashboard 操作体验增强

**背景**：Dashboard 是 CAP 的重要组成部分，它提供了消息监控和管理的能力。随着使用场景的丰富，用户对操作便捷性的要求也越来越高。

**消息删除功能** (#1674)

在 8.4.0 版本中，Dashboard UI 现在支持删除单个或多个消息。这一功能极大地提升了运维效率，当需要清理异常消息或测试数据时，无需再通过数据库直接操作，降低了误操作风险。

**CAP 消息头优雅处理** (#1623)

8.3.2 版本改进了对 CAP 消息头的处理方式。现在，如果消息头中已存在 CAP 消息组头，系统会将其覆盖而不是抛出异常。这使得与现有系统的集成更加平滑，特别是在迁移或集成场景中。

### 存储提供程序支持改进

**背景**：CAP 支持多种数据库作为存储提供程序，不同数据库有其特定的优化需求和兼容性要求。

**MongoDB 索引优化** (#1702)

在 8.4.0 版本中，我们更新了 MongoDB 的索引策略，添加了基于 StatusName 和 ExpiresAt 的复合索引。这一优化显著提升了查询性能，特别是在处理过期消息和状态查询时。

**达梦数据库支持** (8.3.4)

8.3.4 版本迎来了社区贡献的 达梦 数据库存储提供程序。这扩大了 CAP 的数据库支持范围，为使用国产数据库的用户提供了更多选择。

**数据库表默认索引** (#1599)

从 8.3.1 版本开始，我们在创建数据库表时会自动添加默认索引，并调整查询 SQL 以利用这些优化索引。这一改进显著提升了大规模数据下的查询性能，特别是消息状态查询和过期消息清理等操作。

**MySQL 过期数据删除优化** (#1673)

在 8.3.5 版本中，我们修复了 MySQL 删除过期数据时的语法错误，并改进了删除语句的执行效率。这确保了数据清理操作的稳定性和性能。

### 消息传输层优化

**背景**：消息传输层是 CAP 连接不同消息系统的桥梁，其稳定性和性能直接影响整个系统的可靠性。

**标准化 Broker 命名与遥测改进** (#1717)

8.4.0 版本标准化了 Broker 命名规范，并改进了遥测数据收集。这使得在复杂的微服务环境中更容易追踪和诊断问题，提升了系统的可观测性。

**Kafka 配置保留** (#1686)

在 8.3.5 版本中，我们改进了 Kafka 配置处理逻辑。现在，当用户在 MainConfig 中配置了 MessageTimeout 和 RequestTimeout 时，CAP 将不再覆盖这些配置。这给予了开发者更大的灵活性，能够根据具体业务需求调整 Kafka 客户端行为。

**RabbitMQ 客户端升级** (#1645)

8.3.3 版本将 RabbitMQ.Client 升级到了 7.0 版本，享受了新版本带来的性能改进和新特性支持。

**RabbitMQ 队列绑定同步化** (#1670)

在 8.3.4 版本中，我们将 RabbitMQ 队列绑定从异步调用改为同步阻塞调用。这一改动解决了在某些场景下因异步调用时序问题导致的绑定失败情况。

**RabbitMQ 消息体安全处理** (#1727)

8.4.0 版本修复了在高并发场景下 RabbitMQ 消息体可能被不安全重用的问题。现在，系统会在后台处理前将消息体复制到专用缓冲区，确保了数据处理的安全性。

**Azure Service Bus 改进**

在 8.3.2 版本中，我们修复了 Azure Service Bus AutoCompleteMessages 功能导致的无效锁错误 (#1598)。同时在 8.3.1 版本中修复了 GroupConcurrent 在 Azure Service Bus 中不工作的问题 (#1597)，确保了消费者组的并发处理能力。

**Redis Streams 自定义异常处理** (#1618)

8.3.2 版本为 Redis Streams 引入了自定义异常处理支持。现在，当消费 Redis 流发生异常时，可以调用用户自定义的处理逻辑，提供了更大的灵活性。

### BUG 修复

除了上述功能改进外，在这些版本中我们还修复了一系列重要问题：

* **Blazor 应用程序挂起问题** (#1697)：修复了在 Blazor 应用中等待提交事务时可能出现的挂起现象
* **数据库异常处理改进** (#1691)：修复了延迟消息发送时数据库异常导致线程退出的问题
* **潜在死锁问题** (#1672)：修复了更新消息状态和删除过期消息时可能出现的死锁情况
* **PostgreSQL 兼容性** (#1643)：解决了 EFCore 在使用 PostgreSQL 且未设置 Persist Security Info = true 时的崩溃问题
* **PostgreSQL 大负载支持** (#1619)：修复了发送大负载数据时超过 PostgreSQL Include 设计限制导致的索引问题
* **RabbitMQ 拒绝函数调用错误** (#1608)：修复了 RabbitMQ 拒绝功能调用错误
* **密码信息泄露防护** (#1647)：消除了 RabbitMQ 调试日志中包含的密码配置信息，提升了安全性

### 总结

从 8.3.1 到 8.4.0 版本，CAP 在性能、可靠性和用户体验方面都取得了显著进步。我们优化了消息调度机制，增强了 Dashboard 的操作能力，改进了多种存储提供程序的支持，并修复了一系列重要问题。

感谢所有贡献者和用户的支持，特别感谢 @yang-xiaodong、@ustaserdar、@demorgi、@Savorboard、@findersky、@haoyk、@PoteRii、@amimelia、@li-zheng-hao、@MahmoudSamir101 等社区成员的宝贵贡献。

大家在使用的过程中遇到问题希望也能够积极的反馈，帮助CAP变得越来越好。😃

如果你喜欢这个项目，可以通过下面的连接点击 Star 给我们支持。

[![GitHub stars](https://img.shields.io/github/stars/dotnetcore/CAP.svg?label=github-cap-stars)](https://github.com)

如果你觉得本篇文章对您有帮助的话，感谢您的【推荐】。

---

> 本文地址：[https://github.com/savorboard/p/cap-8-4.html](https://github.com)
> 作者博客：[Savorboard](https://github.com)
> 本文原创授权为：署名 - 非商业性使用 - 禁止演绎，协议[普通文本](https://github.com) | 协议[法律文本](https://github.com)
