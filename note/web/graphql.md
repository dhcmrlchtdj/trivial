# GraphQL

---

http://graphql.org/
https://www.quora.com/What-problem-does-GraphQL-solve

---

今天又翻了下 GraphQL 的官网，还是没明白。

---

首先，GraphQL 要解决什么问题？怎么解决？

直接看官网列举的特性

- 客户端指定接口数据
- 避免 REST 造成的多次查询，实现请求合并
- 类型系统
- 新增数据不影响旧查询
- 强力的配套设施

解决的这些问题，有没有哪个是开发中非常痛的点呢？
以我目前的经验，开发维护时都不是非常痛的点。

- 接口返回的数据多了，这是常有的事情。但影响其实不大。
- 多次请求的问题会有，但很多时候可以通过优化接口避免。
- 类型系统很赞。但真要保证服务质量，动态语言如 node 也会上 validate 之类的吧。
- 旧服务的稳定，通常借由版本号保证。
- 配套设施赞。

怎么说呢，感觉都是有最好，没有也无所谓的功能。

---

然后是我的一些疑惑，怎么实现 GraphQL。

虽然说是有类型系统，但其实类型系统并不完全，还是要看实现里是如何定义数据的。
根据定义的不同，相同的前端请求，会返回不同的数据。
所以，感觉这里的类型系统要打一些折扣。

旧接口稳定性的问题，新增确实方便了，但删除并没有变化吧。
反而使用情况的统计是不是造成了一些困难。

合并请求是我最大的疑问。
GraphQL 到底是哪一层的设施？
对外直接对接了用户请求，对内呢？到数据库？到后端服务？
怎么和后端服务通信？怎么避免多次调用后端服务？
我脑袋里始终建立不了这种实现上的分层、概念映射。
网站上的例子都太过简单了。

---

# principled graphql

https://principledgraphql.com/

- integrity
    - one graph
    - federated implmentation
    - schema registry
- agility
    - demand-oriented schema
    - agile
        - it should be possible to change the graph many times a day
    - performance
    - metadata
- operation
    - access control
        - per-client
    - logging
        - trace
    - layer architecture
        - separate the graphql layer from the service layer

以为是 12factor 那种有启发性的东西。
结果，有点水啊。
