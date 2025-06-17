## 线程同步/异步

| 维度 | 同步（Synchronous） | 异步（Asynchronous） |
| --- | --- |
| 定义	| 线程按顺序执行，一个操作必须等待前一个操作完成后才能开始。| 	操作无需等待前一个操作完成，可并发执行。调用方在发起操作后继续执行后续代码，结果通过回调、Future 等方式通知。| 
| 执行流程	| 线性执行，操作之间存在明确的先后顺序。| 	非线行执行，操作可重叠或并行进行。
| 阻塞特性	| 调用方线程会被阻塞，直到被调用的操作完成。| 	调用方线程不会被阻塞，可继续执行其他任务。
| 依赖关系	| 后一个操作依赖前一个操作的结果。| 	操作间通常无直接依赖，可独立执行。
| 实现方式	- 方法调用
          - synchronized 关键字
          - join() 方法
          - wait()/notify() 机制	| - 多线程（Thread、ExecutorService）
- 回调函数（Callback）
- Future/Promise
- 事件驱动模型（如 Reactor 模式）|
适用场景	- 操作必须按顺序执行（如数据库事务）
- 资源独占访问（如文件读写）
- 简单逻辑，无需并发优化	- I/O 密集型任务（如网络请求、文件读写）
- 耗时操作（如计算、渲染）
- 高并发场景（如 Web 服务器、消息队列）
优点	- 逻辑简单，易于理解和调试
- 资源访问可控，不易出现竞态条件	- 提高系统吞吐量和响应性
- 充分利用多核 CPU 资源
- 避免线程长时间阻塞
缺点	- 性能瓶颈（尤其在 I/O 密集型场景）
- 可能导致线程长时间等待	- 编程模型复杂（如回调地狱）
- 调试困难（如竞态条件、死锁）
- 资源管理需谨慎（如线程池溢出）
示例代码	java<br>public void syncOperation() {<br> String result = fetchData(); // 阻塞等待结果<br> process(result); // 依赖前一步结果<br>}<br>	java<br>public void asyncOperation() {<br> executor.submit(() -> {<br> String result = fetchData();<br> process(result); // 在另一个线程中执行<br> });<br> continueOtherWork(); // 无需等待<br>}<br>
