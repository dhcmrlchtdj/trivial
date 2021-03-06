# linkedin qps

---

http://www.infoq.com/cn/articles/how-linkedin-determines-the-capacity-limits-of-its-services

---

规划流量增长规模

- 以服务目前的配置最大可以承担多大的 QPS（每秒查询数）？
- 这些服务器能够处理比当前峰值高出 50% 的流量吗？
- 从基础设施来看，服务潜在的容量瓶颈是什么？

---

解决方案需要具备如下特点

- 利用生产环境来突破实验室的局限
- 使用真实的流量作为负载
- 最小化对用户体验造成的影响
- 低运营成本和开销
- 自动伸缩

---

- Redliner 在目标服务上运行压力测试，逐步增加流量，直到服务无法处理更多的流量为止，以此来评估服务的吞吐量。
- Redliner 自动从生产环境引入流量，并确保对用户只有很小的影响。

---

两个原则：影响最小化和完全自动化。
