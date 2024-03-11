参考资料：https://juejin.cn/post/7316539952475619362?utm_source=gold_browser_extension

> 在JavaScript编程中，异常处理是一个至关重要的概念。`try...catch`语句就是JavaScript中处理异常的主要手段。本文将详细介绍`try...catch`的用法、注意事项以及常见使用场景，帮助读者更好地理解和应用这一异常处理机制。

#### 用法

```javascript
try {
  // 有可能抛出异常的代码
} catch (error) {
  // 代码抛出异常，error 变量会保存抛出的异常对象
  // 可能会做的操作：上报或打印错误日志、针对异常采取提示
  console.error("An error occurred:", error.message);
} finally {
  // 不论 try 或 catch 是否出现异常，finally 块中的代码总会被执行（可选）
}
```

- **异常对象**：在 `catch` 块中，我们通常会声明一个变量（如上述示例中的 `error`）来接收抛出的异常对象。这个对象包含了有关异常的详细信息，例如错误类型、错误消息和堆栈跟踪。

#### 使用场景

1. **网络请求** 最常见的使用场景是调用后端接口时，当接口返回异常时，需要对这种情况做处理。
2. **文件操作**：在读取或写入文件时，也可能会因为文件不存在、权限不足等原因抛出异常。使用`try...catch`可以确保在出现异常时，程序能够给出合理的响应，而不是直接崩溃。

#### 无法捕获的情形

1. **同步代码中的异常**：`try...catch` 结构可以捕获同步代码块中抛出的异常，但对于异步操作（如 Promise、async/await）中抛出的异常，不能直接使用常规的 `try...catch` 结构捕获，需要使用 Promise 的 `.catch` 方法或者在 async 函数中使用 `try...catch`。
   `setTimeout`等异步操作无法捕获到异常，见下面的例子：

   ```javascript
   new Promise((resolve, reject) => {
     setTimeout(() => {
       try {
         throw new Error('err');
       } catch (err) {
         reject(err);
       }
     }, 200);
   })
     .then(() => {
       // 正常执行时的处理逻辑
     })
     .catch((err) => {
       console.log(err); // 这里会捕捉到错误
     });
   
   ```

   正确做法：在异步操作中直接处理错误 .catch(e)

   上面例子捕获的正确做法：

   ```javascript
   new Promise((resolve, reject) => {
     setTimeout(() => {
       try {
         throw new Error('err');
       } catch (err) {
         reject(err);
       }
     }, 200);
   })
     .then(() => {
       // 正常执行时的处理逻辑
     })
     .catch((err) => {
       console.log(err); // 这里会捕捉到错误
     });
   ```

   

2. **程序提前终止**：严重的致命错误（如 out-of-memory 错误、语法错误等）可能导致 JavaScript 解释器停止执行，这种情况下，即使存在 `try...catch` 结构，也无法捕获这些异常。

#### 业务中的实践

1. 把error对象进行一层包装，便于在业务使用
2. 会在catch中返回自定义错误码，在上层进行统一处理

