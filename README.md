# Open Source Engineering Lab

> 每周一条技术演进主线；先搞懂为什么修改，再验证怎样修改。

本仓库用于系统学习 **QEMU/KVM、Linux Kernel、DPDK、Ceph、OpenXiangShan** 的真实工程设计与补丁演进。不是热点新闻收集站，不以阅读的 PR 数量考核学习。

## 学习原则

- **一周只做一条主线。** 从最初可验证的设计/基线，到维护者讨论、关键补丁、回归与最新状态。
- **证据链优先。** 结论必须链接原始设计文档、邮件讨论、Issue、PR、提交或当前代码；区分 merged / open / rejected / proposal。
- **先推理再读答案。** 对每个演进节点回答：原来解决了什么？为什么不够？新设计引入何种成本/风险？什么测试能揭穿错误？
- **实践闭环。** 至少产出一份执行路径图、一个可复现的测试或微型参考模型，以及一份自我评审。
- **历史诚实。** 找到的最早 PR 不是必然的“最初设计”。未查实的初版、版本归属、性能提升一律标明。
- **避免主线发散。** KVM/Linux 与香山为优先轨道，DPDK/Ceph 作为案例池；每周最多选一个。

## 本周主线（2026-11-02 起）

**W01 · XiangShan MMU：SFENCE/HFENCE 的正确性、精准失效与回归**

- [阅读路线、补丁谱系、实验与验收](tracks/xiangshan-fence-evolution/W01.md)
- 上游仓库：https://github.com/OpenXiangShan/XiangShan
- 关键词：HFENCE.GVMA、SFENCE.VMA、VS-stage / G-stage、PageTableCache、L1TLB、VMID、ASID、PBMT、MPRV
- 起点：2024 年可验证的 Fence Bug；当前节点：2026 年 10 月公开、尚未合并的上下文修复。**这不是声称 2024 年是虚拟化 MMU 最初引入的时间。**

## 待选主题池（只做选题，不展开）

| 社区 | 候选演进主题 | 需要回答的问题 | 起始证据 |
| --- | --- | --- | --- |
| Linux/KVM Arm64 | 通用 Stage-2 页表基础设施与后续维护 | 为什么抽离 map/unmap？后续为何拆分销毁路径？ | https://lists.infradead.org/pipermail/linux-arm-kernel/2020-August/593341.html |
| QEMU / Linux virtio-net | 多队列从早期 RFC 到 QEMU+vhost 支持 | 为什么单队列不够？为什么需要多 TAP/vhost？ | https://lists.gnu.org/archive/html/qemu-devel/2013-01/msg04719.html |
| DPDK | mempool cache 大小与 refill/flush 语义 | 为什么实际容量偏离配置？为什么反复修订？ | https://mails.dpdk.org/archives/dev/2024-October/302815.html |
| Ceph | BlueStore RocksDB Column Family 分片 | 为什么从默认 CF 转为 sharding？老 OSD 如何迁移？ | https://docs.ceph.com/en/latest/rados/configuration/bluestore-config-ref/ |
| XiangShan（后续） | H-TLB sector compression 与并行 HPTW | 5.1% 虚拟化 checkpoint 收益如何验证 PPA 代价？ | https://github.com/OpenXiangShan/XiangShan/pull/6778 |

以上是**候选，不是已完成的技术谱系**；在正式选择下一周前还须核实原始设计、所有关键版本、合并状态和当前代码。

## 单期交付标准

一份 Wxx.md 至少包含：问题与边界、可验证的历史版本、重要源码/补丁与维护者观点、现行状态、最小实验计划、反例、性能/复杂度取舍、来源索引、未解决问题。

“看懂了”不算验收；能独立解释设计变更、构造反例并用代码/波形/数据验证才算。
