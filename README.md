# Big-React

从零实现 React v18 🎉🎉🎉

没什么能比自己亲手造个`React18`能让自己理解的更深了

## TODO List

### 工程类需求

| 类型 | 内容                               | 完成情况 | 备注 |
| ---- | ---------------------------------- | -------- | ---- |
| 架构 | monorepo                           | ✅       |      |
| 规范 | eslint                             | ✅       |      |
| 规范 | prettier                           | ✅       |      |
| 规范 | commitlint + husky                 | ✅       |      |
| 规范 | lint-staged                        | ✅       |      |
| 规范 | tsc                                | ✅       |      |
| 测试 | jest 环境搭建                      | ⬜️      |      |
| 规范 | tsc                                | ✅       |      |
| 构建 | babel 配置                         | ⬜️      |      |
| 构建 | Dev 环境包的构建                   | ⬜️      |      |
| 构建 | Prod 环境包的构建                  | ⬜️      |      |
| 部署 | Github Action 执行 lint 与 test    | ⬜️      |      |
| 部署 | Github Action 根据 tag 发布 npm 包 | ⬜️      |      |

### 框架需求

| 类型       | 内容                      | 完成情况 | 备注         |
| ---------- | ------------------------- | -------- | ------------ |
| React      | JSX 转换                  | ✅       |              |
| ReactDOM   | 浏览器环境 DOM 的增/删/改 | ⬜️      |              |
| ReactNoop  | ReactNoop Renderer        | ⬜️      |              |
| Reconciler | Fiber 架构                | ⬜️      |              |
| Reconciler | 事件模型                  | ⬜️      |              |
| Reconciler | Lane 模型                 | ⬜️      |              |
| Reconciler | Update 机制               | ⬜️      |              |
| Reconciler | reconcile 流程            | ⬜️      | 即 Diff 算法 |
| Reconciler | 同步调度流程              | ⬜️      |              |
| Reconciler | 异步调度流程              | ⬜️      |              |

## 更新日志

### v1

跑通 mount 时更新流程，包括如下需求点：

- JSX 转换
- Fiber 架构
- 同步调度流程
- 浏览器环境 DOM 的增/删/改
