<p align="center"><img src="https://p3.ssl.qhimg.com/t0154d29702a432306d.png" alt="React-On-The-Way"></p>

# React-On-The-Way
基于React`V16.13.1`架构，从零实现React，相关配套文章

- <a href="https://juejin.im/post/5e9abf06e51d454702460bf6">🔥从0实现React 📖PART1 React的架构设计</a>

## 历史版本预览
通过切换`git tag`浏览不同完成度的项目，执行`npm start`启动该版本下的Demo

### 当前版本v5
在v3中我们实现了状态更新，直接在`FunctionComponent`函数体内触发更新会造成死循环，所以我们用计时器来触发。在业务中，我们一般是通过：

1. 回调函数（ex：onClick）
2. `useEffect hook`
3. `ClassComponent`生命周期钩子

来触发。既然我们已经实现了`useState hook`，这一版我们就实现`useEffect hook`，新增功能如下：

- [x] `useEffect hook`首屏及再次渲染的完整逻辑

### v4
之前只能更新单一节点，这次实现了大名鼎鼎的React Diff算法，可以更新多个兄弟子节点了😄，新增功能如下：
- [x] 节点支持`key`prop
- [x] `commit`流程支持`Deletion effectTag`处理
- [x] `reconcileChildrenArray`支持非首次渲染的diff算法

ps：支持`Deletion effectTag`处理是为了应对：

```javascript
// 首屏渲染的组件
[a, b, c] 
// 再次渲染的组件
[a, null, c] 
```
在这种情况下b fiber被标记为`Deletion effectTag`，对应的DOM节点需要删除

### v3
之前的版本只实现了首屏渲染的逻辑，即使在v2中实现了`useState`也只实现了`useState(initialValue)`带来的首屏渲染，在v3中我们终于实现状态更新啦，撒花🎉，新增功能如下：
- [x] `useState hook`对单一`HostComponent`的状态更新

ps：之所以只支持单一`HostComponent`，是因为还没有实现`key`以及`diff`算法，所以无法支持多个兄弟组件的更新

🐛当一个组件中使用多个`useState hook`且他们的更新函数同时触发，如示例中：

```javascript
// 会造成页面逐渐卡顿并最终崩溃的例子
function App({name}) {
  const [even, updateEven] = useState(0);
  const [odd, updateOdd] = useState(1);

  setTimeout(() => {
    updateEven(even + 2);
    updateOdd(odd + 2);  
  }, 2000);
  
  return (
    <ul>
      <li key={0}>{even}</li>
      <li key={1}>{odd}</li>
    </ul>
  )
}

```
react-on-the-way会造成页面逐渐卡顿并最终崩溃。原因是`updateEven`和`updateOdd`方法会分别开始一次新的更新流程。

在其中每次更新流程执行到`updateFunctionComponent`时会调用`App`函数，在函数内部会调用计时器并在2000ms后又调用这2个更新函数，从而又开启新的更新流程。更新流程的数量会指数增加并最终崩溃。

造成这个问题的原因是我们还没有实现React的任务优先级机制与任务的批处理。在React中，

- 同步模式下同一个事件函数内的同步更新会被批处理，只产生一次更新流程
- 异步模式下所有更新都会经过优先级调度

### v2
为了实现React的页面更新逻辑，需要改变状态（state），我们有2条路可选：

1. 实现`ClassComopnent setState`
2. 实现`FunctionComopnent useState`

考虑`hook`是React的趋势，我们优先实现`useState`，所以v2我们在第一版基础上增加了`FunctionComponent`相关首屏渲染，新增功能如下：
- [x] `FunctionComponent`类型组件的首屏渲染
- [x] `hook`架构体系
- [x] `useState hook`首屏渲染做的工作

### v1
我们的首要目标是实现React的页面更新逻辑，基于这个目标，我们首先实现了`HostComponent`的首屏渲染，新增功能如下：
- [x] Render-Commit整体架构体系
- [x] `HostComponent`的首屏渲染
