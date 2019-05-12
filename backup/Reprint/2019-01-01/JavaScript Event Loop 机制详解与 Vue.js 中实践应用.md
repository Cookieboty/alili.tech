---
title: 'JavaScript Event Loop 机制详解与 Vue.js 中实践应用' 
date: 2019-01-01 2:30:07
hidden: true
slug: o9kn7w1w6dm
categories: [reprint]
---

{{< raw >}}

                    
<blockquote><p><a href="https://zhuanlan.zhihu.com/p/28508795" rel="nofollow noreferrer" target="_blank">JavaScript Event Loop 机制详解与 Vue.js 中实践应用</a>归纳于笔者的<a href="https://parg.co/bjK" rel="nofollow noreferrer" target="_blank">现代 JavaScript 开发：语法基础与实践技巧</a>系列文章。本文依次介绍了函数调用栈、MacroTask 与 MicroTask 执行顺序、浅析 Vue.js 中 nextTick 实现等内容；本文中引用的参考资料统一声明在 <a href="https://parg.co/b2O" rel="nofollow noreferrer" target="_blank">JavaScript 学习与实践资料索引</a>。</p></blockquote>
<h1 id="articleHeader0">1. 事件循环机制详解与实践应用</h1>
<p>JavaScript 是典型的单线程单并发语言，即表示在同一时间片内其只能执行单个任务或者部分代码片。换言之，我们可以认为某个同域浏览器上下中 JavaScript 主线程拥有一个函数调用栈以及一个任务队列（参考 <a href="https://html.spec.whatwg.org/multipage/webappapis.html#task-queue" rel="nofollow noreferrer" target="_blank">whatwg 规范</a>）；主线程会依次执行代码，当遇到函数时，会先将函数入栈，函数运行完毕后再将该函数出栈，直到所有代码执行完毕。当函数调用栈为空时，运行时即会根据事件循环（Event Loop）机制来从任务队列中提取出待执行的回调并执行，执行的过程同样会进行函数帧的入栈出栈操作。每个线程有自己的事件循环，所以每个 Web Worker有自己的，所以它才可以独立执行。然而，所有同属一个 origin 的窗体都共享一个事件循环，所以它们可以同步交流。</p>
<p>Event Loop（事件循环）并不是 JavaScript 中独有的，其广泛应用于各个领域的异步编程实现中；所谓的 Event Loop 即是一系列回调函数的集合，在执行某个异步函数时，会将其回调压入队列中，JavaScript 引擎会在异步代码执行完毕后开始处理其关联的回调。</p>
<p><span class="img-wrap"><img data-src="/img/remote/1460000011044247" src="https://static.alili.tech/img/remote/1460000011044247" alt="" title="" style="cursor: pointer; display: inline;"></span></p>
<p>在 Web 开发中，我们常常会需要处理网络请求等相对较慢的操作，如果将这些操作全部以同步阻塞方式运行无疑会大大降低用户界面的体验。另一方面，我们点击某些按钮之后的响应事件可能会导致界面重渲染，如果因为响应事件的执行而阻塞了界面的渲染，同样会影响整体性能。实际开发中我们会采用异步回调来处理这些操作，这种调用者与响应之间的解耦保证了 JavaScript 能够在等待异步操作完成之前仍然能够执行其他的代码。Event Loop 正是负责执行队列中的回调并且将其压入到函数调用栈中，其基本的代码逻辑如下所示：</p>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="全选"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="while (queue.waitForMessage()) {
  queue.processNextMessage();
}" title="" data-original-title="复制"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="放进笔记"></span>
      </div>
      </div><pre class="hljs cpp"><code><span class="hljs-keyword">while</span> (<span class="hljs-built_in">queue</span>.waitForMessage()) {
  <span class="hljs-built_in">queue</span>.processNextMessage();
}</code></pre>
<p>完整的浏览器中 JavaScript 事件循环机制图解如下：</p>
<p><span class="img-wrap"><img data-src="/img/remote/1460000011044248" src="https://static.alili.tech/img/remote/1460000011044248" alt="" title="" style="cursor: pointer; display: inline;"></span></p>
<p>在 Web 浏览器中，任何时刻都有可能会有事件被触发，而仅有那些设置了回调的事件会将其相关的任务压入到任务队列中。回调函数被调用时即会在函数调用栈中创建初始帧，而直到整个函数调用栈清空之前任何产生的任务都会被压入到任务队列中延后执行；顺序的同步函数调用则会创建新的栈帧。总结而言，浏览器中的事件循环机制阐述如下：</p>
<ul>
<li><p>浏览器内核会在其它线程中执行异步操作，当操作完成后，将操作结果以及事先定义的回调函数放入 JavaScript 主线程的任务队列中。</p></li>
<li><p>JavaScript 主线程会在执行栈清空后，读取任务队列，读取到任务队列中的函数后，将该函数入栈，一直运行直到执行栈清空，再次去读取任务队列，不断循环。</p></li>
<li><p>当主线程阻塞时，任务队列仍然是能够被推入任务的。这也就是为什么当页面的 JavaScript 进程阻塞时，我们触发的点击等事件，会在进程恢复后依次执行。</p></li>
</ul>
<h1 id="articleHeader1">2. 函数调用栈与任务队列</h1>
<p>在<a href="https://parg.co/bT4" rel="nofollow noreferrer" target="_blank">变量作用域与提升</a>一节中我们介绍过所谓执行上下文（Execution Context）的概念，在 JavaScript 代码执行过程中，我们可能会拥有一个全局上下文，多个函数上下文或者块上下文；每个函数调用都会创造新的上下文与局部作用域。而这些执行上下文堆叠就形成了所谓的执行上下文栈（Execution Context Stack），便如上文介绍的 JavaScript 是单线程事件循环机制，同时刻仅会执行单个事件，而其他事件都在所谓的执行栈中排队等待：</p>
<p><span class="img-wrap"><img data-src="/img/remote/1460000011044249" src="https://static.alili.tech/img/remote/1460000011044249" alt="" title="" style="cursor: pointer; display: inline;"></span></p>
<p>而从 JavaScript 内存模型的角度，我们可以将内存划分为调用栈（Call Stack）、堆（Heap）以及队列（Queue）等几个部分：</p>
<p><span class="img-wrap"><img data-src="/img/remote/1460000011044250" src="https://static.alili.tech/img/remote/1460000011044250" alt="" title="" style="cursor: pointer; display: inline;"></span></p>
<p>其中的调用栈会记录所有的函数调用信息，当我们调用某个函数时，会将其参数与局部变量等压入栈中；在执行完毕后，会弹出栈首的元素。而堆则存放了大量的非结构化数据，譬如程序分配的变量与对象。队列则包含了一系列待处理的信息与相关联的回调函数，每个 JavaScript 运行时都必须包含一个任务队列。当调用栈为空时，运行时会从队列中取出某个消息并且执行其关联的函数（也就是创建栈帧的过程）；运行时会递归调用函数并创建调用栈，直到函数调用栈全部清空再从任务队列中取出消息。换言之，譬如按钮点击或者 HTTP 请求响应都会作为消息存放在任务队列中；需要注意的是，仅当这些事件的回调函数存在时才会被放入任务队列，否则会被直接忽略。</p>
<p>譬如对于如下的代码块：</p>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="全选"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="function fire() {
    const result = sumSqrt(3, 4)
    console.log(result);
}
function sumSqrt(x, y) {
    const s1 = square(x)
    const s2 = square(y)
    const sum = s1 + s2;
    return Math.sqrt(sum)
}
function square(x) {
    return x * x;
}

fire()" title="" data-original-title="复制"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="放进笔记"></span>
      </div>
      </div><pre class="hljs javascript"><code><span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">fire</span>(<span class="hljs-params"></span>) </span>{
    <span class="hljs-keyword">const</span> result = sumSqrt(<span class="hljs-number">3</span>, <span class="hljs-number">4</span>)
    <span class="hljs-built_in">console</span>.log(result);
}
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">sumSqrt</span>(<span class="hljs-params">x, y</span>) </span>{
    <span class="hljs-keyword">const</span> s1 = square(x)
    <span class="hljs-keyword">const</span> s2 = square(y)
    <span class="hljs-keyword">const</span> sum = s1 + s2;
    <span class="hljs-keyword">return</span> <span class="hljs-built_in">Math</span>.sqrt(sum)
}
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">square</span>(<span class="hljs-params">x</span>) </span>{
    <span class="hljs-keyword">return</span> x * x;
}

fire()</code></pre>
<p>其对应的函数调用图（整理自<a href="https://github.com/ccforward/cc/issues/47" rel="nofollow noreferrer" target="_blank">这里</a>）为：</p>
<p><span class="img-wrap"><img data-src="/img/remote/1460000011044251" src="https://static.alili.tech/img/remote/1460000011044251" alt="" title="" style="cursor: pointer;"></span></p>
<p>这里还值得一提的是，Promise.then 是异步执行的，而创建 Promise 实例 （executor） 是同步执行的，譬如下述代码：</p>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="全选"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="(function test() {
    setTimeout(function() {console.log(4)}, 0);
    new Promise(function executor(resolve) {
        console.log(1);
        for( var i=0 ; i<10000 ; i++ ) {
            i == 9999 &amp;&amp; resolve();
        }
        console.log(2);
    }).then(function() {
        console.log(5);
    });
    console.log(3);
})()

// 输出结果为：
// 1
// 2
// 3
// 5
// 4" title="" data-original-title="复制"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="放进笔记"></span>
      </div>
      </div><pre class="javascript hljs"><code class="javascript">(<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">test</span>(<span class="hljs-params"></span>) </span>{
    setTimeout(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>) </span>{<span class="hljs-built_in">console</span>.log(<span class="hljs-number">4</span>)}, <span class="hljs-number">0</span>);
    <span class="hljs-keyword">new</span> <span class="hljs-built_in">Promise</span>(<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">executor</span>(<span class="hljs-params">resolve</span>) </span>{
        <span class="hljs-built_in">console</span>.log(<span class="hljs-number">1</span>);
        <span class="hljs-keyword">for</span>( <span class="hljs-keyword">var</span> i=<span class="hljs-number">0</span> ; i&lt;<span class="hljs-number">10000</span> ; i++ ) {
            i == <span class="hljs-number">9999</span> &amp;&amp; resolve();
        }
        <span class="hljs-built_in">console</span>.log(<span class="hljs-number">2</span>);
    }).then(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>) </span>{
        <span class="hljs-built_in">console</span>.log(<span class="hljs-number">5</span>);
    });
    <span class="hljs-built_in">console</span>.log(<span class="hljs-number">3</span>);
})()

<span class="hljs-comment">// 输出结果为：</span>
<span class="hljs-comment">// 1</span>
<span class="hljs-comment">// 2</span>
<span class="hljs-comment">// 3</span>
<span class="hljs-comment">// 5</span>
<span class="hljs-comment">// 4</span></code></pre>
<p>我们可以参考 Promise 规范中有关于 promise.then 的部分：</p>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="全选"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="promise.then(onFulfilled, onRejected)

2.2.4 onFulfilled or onRejected must not be called until the execution context stack contains only platform code. [3.1].

Here “platform code” means engine, environment, and promise implementation code. In practice, this requirement ensures that onFulfilled and onRejected execute asynchronously, after the event loop turn in which then is called, and with a fresh stack. This can be implemented with either a “macro-task” mechanism such as setTimeout or setImmediate, or with a “micro-task” mechanism such as MutationObserver or process.nextTick. Since the promise implementation is considered platform code, it may itself contain a task-scheduling queue or “trampoline” in which the handlers are called." title="" data-original-title="复制"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="放进笔记"></span>
      </div>
      </div><pre class="hljs livecodeserver"><code>promise.<span class="hljs-keyword">then</span>(onFulfilled, onRejected)

<span class="hljs-number">2.2</span><span class="hljs-number">.4</span> onFulfilled <span class="hljs-keyword">or</span> onRejected must <span class="hljs-keyword">not</span> be called <span class="hljs-keyword">until</span> <span class="hljs-keyword">the</span> execution context stack <span class="hljs-keyword">contains</span> only <span class="hljs-built_in">platform</span> code. [<span class="hljs-number">3.1</span>].

Here “<span class="hljs-built_in">platform</span> code” means engine, environment, <span class="hljs-keyword">and</span> promise implementation code. In practice, this requirement ensures that onFulfilled <span class="hljs-keyword">and</span> onRejected execute asynchronously, <span class="hljs-keyword">after</span> <span class="hljs-keyword">the</span> event loop turn <span class="hljs-keyword">in</span> which <span class="hljs-keyword">then</span> is called, <span class="hljs-keyword">and</span> <span class="hljs-keyword">with</span> <span class="hljs-keyword">a</span> fresh stack. This can be implemented <span class="hljs-keyword">with</span> either <span class="hljs-keyword">a</span> “macro-task” mechanism such <span class="hljs-keyword">as</span> setTimeout <span class="hljs-keyword">or</span> setImmediate, <span class="hljs-keyword">or</span> <span class="hljs-keyword">with</span> <span class="hljs-keyword">a</span> “micro-task” mechanism such <span class="hljs-keyword">as</span> MutationObserver <span class="hljs-keyword">or</span> <span class="hljs-built_in">process</span>.nextTick. Since <span class="hljs-keyword">the</span> promise implementation is considered <span class="hljs-built_in">platform</span> code, <span class="hljs-keyword">it</span> may itself contain <span class="hljs-keyword">a</span> task-scheduling queue <span class="hljs-keyword">or</span> “trampoline” <span class="hljs-keyword">in</span> which <span class="hljs-keyword">the</span> handlers are called.</code></pre>
<p>规范要求，onFulfilled 必须在执行上下文栈（Execution Context Stack） 只包含 平台代码（platform code） 后才能执行。平台代码指引擎，环境，Promise 实现代码等。实践上来说，这个要求保证了 onFulfilled 的异步执行（以全新的栈），在 then 被调用的这个事件循环之后。</p>
<h1 id="articleHeader2">3. MacroTask（Task） 与 MicroTask（Job）</h1>
<p>在面试中我们常常会碰到如下的代码题，其主要就是考校 JavaScript 不同任务的执行先后顺序：</p>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="全选"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="// 测试代码
console.log('main1');

// 该函数仅在 Node.js 环境下可以使用
process.nextTick(function() {
    console.log('process.nextTick1');
});

setTimeout(function() {
    console.log('setTimeout');
    process.nextTick(function() {
        console.log('process.nextTick2');
    });
}, 0);

new Promise(function(resolve, reject) {
    console.log('promise');
    resolve();
}).then(function() {
    console.log('promise then');
});

console.log('main2');

// 执行结果
main1
promise
main2
process.nextTick1
promise then
setTimeout
process.nextTick2" title="" data-original-title="复制"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="放进笔记"></span>
      </div>
      </div><pre class="hljs javascript"><code><span class="hljs-comment">// 测试代码</span>
<span class="hljs-built_in">console</span>.log(<span class="hljs-string">'main1'</span>);

<span class="hljs-comment">// 该函数仅在 Node.js 环境下可以使用</span>
process.nextTick(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>) </span>{
    <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'process.nextTick1'</span>);
});

setTimeout(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>) </span>{
    <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'setTimeout'</span>);
    process.nextTick(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>) </span>{
        <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'process.nextTick2'</span>);
    });
}, <span class="hljs-number">0</span>);

<span class="hljs-keyword">new</span> <span class="hljs-built_in">Promise</span>(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params">resolve, reject</span>) </span>{
    <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'promise'</span>);
    resolve();
}).then(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>) </span>{
    <span class="hljs-built_in">console</span>.log(<span class="hljs-string">'promise then'</span>);
});

<span class="hljs-built_in">console</span>.log(<span class="hljs-string">'main2'</span>);

<span class="hljs-comment">// 执行结果</span>
main1
promise
main2
process.nextTick1
promise then
setTimeout
process.nextTick2</code></pre>
<p>我们在前文中已经介绍过 JavaScript 的主线程在遇到异步调用时，这些异步调用会立刻返回某个值，从而让主线程不会在此处阻塞。而真正的异步操作会由浏览器执行，主线程则会在清空当前调用栈后，按照先入先出的顺序读取任务队列里面的任务。而 JavaScript 中的任务又分为 MacroTask 与 MicroTask 两种，在 ES2015 中 MacroTask 即指 Task，而 MicroTask 则是指代 Job。典型的 MacroTask 包含了 setTimeout, setInterval, setImmediate, requestAnimationFrame, I/O, UI rendering 等，MicroTask 包含了 process.nextTick, Promises, Object.observe, MutationObserver 等。 二者的关系可以图示如下：</p>
<p><span class="img-wrap"><img data-src="/img/remote/1460000011044252" src="https://static.alili.tech/img/remote/1460000011044252" alt="" title="" style="cursor: pointer; display: inline;"></span></p>
<p>参考 <a href="https://html.spec.whatwg.org/multipage/webappapis.html#task-queue" rel="nofollow noreferrer" target="_blank">whatwg 规范</a> 中的描述：一个事件循环(Event Loop)会有一个或多个任务队列(Task Queue，又称 Task Source)，这里的 Task Queue 就是 MacroTask Queue，而 Event Loop 仅有一个 MicroTask Queue。每个 Task Queue 都保证自己按照回调入队的顺序依次执行，所以浏览器可以从内部到JS/DOM，保证动作按序发生。而在 Task 的执行之间则会清空已有的 MicroTask 队列，在 MacroTask 或者 MicroTask 中产生的 MicroTask 同样会被压入到 MicroTask 队列中并执行。参考如下代码：</p>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="全选"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="function foo() {
  console.log(&quot;Start of queue&quot;);
  bar();
  setTimeout(function() {
    console.log(&quot;Middle of queue&quot;);
  }, 0);
  Promise.resolve().then(function() {
    console.log(&quot;Promise resolved&quot;);
    Promise.resolve().then(function() {
      console.log(&quot;Promise resolved again&quot;);
    });
  });
  console.log(&quot;End of queue&quot;);
}

function bar() {
  setTimeout(function() {
    console.log(&quot;Start of next queue&quot;);
  }, 0);
  setTimeout(function() {
    console.log(&quot;End of next queue&quot;);
  }, 0);
}

foo();

// 输出
Start of queue
End of queue
Promise resolved
Promise resolved again
Start of next queue
End of next queue
Middle of queue" title="" data-original-title="复制"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="放进笔记"></span>
      </div>
      </div><pre class="hljs javascript"><code><span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">foo</span>(<span class="hljs-params"></span>) </span>{
  <span class="hljs-built_in">console</span>.log(<span class="hljs-string">"Start of queue"</span>);
  bar();
  setTimeout(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>) </span>{
    <span class="hljs-built_in">console</span>.log(<span class="hljs-string">"Middle of queue"</span>);
  }, <span class="hljs-number">0</span>);
  <span class="hljs-built_in">Promise</span>.resolve().then(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>) </span>{
    <span class="hljs-built_in">console</span>.log(<span class="hljs-string">"Promise resolved"</span>);
    <span class="hljs-built_in">Promise</span>.resolve().then(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>) </span>{
      <span class="hljs-built_in">console</span>.log(<span class="hljs-string">"Promise resolved again"</span>);
    });
  });
  <span class="hljs-built_in">console</span>.log(<span class="hljs-string">"End of queue"</span>);
}

<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">bar</span>(<span class="hljs-params"></span>) </span>{
  setTimeout(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>) </span>{
    <span class="hljs-built_in">console</span>.log(<span class="hljs-string">"Start of next queue"</span>);
  }, <span class="hljs-number">0</span>);
  setTimeout(<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>) </span>{
    <span class="hljs-built_in">console</span>.log(<span class="hljs-string">"End of next queue"</span>);
  }, <span class="hljs-number">0</span>);
}

foo();

<span class="hljs-comment">// 输出</span>
Start <span class="hljs-keyword">of</span> queue
End <span class="hljs-keyword">of</span> queue
<span class="hljs-built_in">Promise</span> resolved
<span class="hljs-built_in">Promise</span> resolved again
Start <span class="hljs-keyword">of</span> next queue
End <span class="hljs-keyword">of</span> next queue
Middle <span class="hljs-keyword">of</span> queue</code></pre>
<p>上述代码中首个 TaskQueue 即为 foo()，foo() 又调用了 bar() 构建了新的 TaskQueue，bar() 调用之后 foo() 又产生了 MicroTask 并被压入了唯一的 MicroTask 队列。我们最后再总计下 JavaScript MacroTask 与 MicroTask 的执行顺序，当执行栈(call stack)为空的时候，开始依次执行：</p>
<ol>
<li><p>把最早的任务(task A)放入任务队列</p></li>
<li><p>如果 task A 为null (那任务队列就是空)，直接跳到第6步</p></li>
<li><p>将 currently running task 设置为 task A</p></li>
<li><p>执行 task A (也就是执行回调函数)</p></li>
<li><p>将 currently running task 设置为 null 并移出 task A</p></li>
<li>
<p>执行 microtask 队列</p>
<ul>
<li><p>a: 在 microtask 中选出最早的任务 task X</p></li>
<li><p>b: 如果 task X 为null (那 microtask 队列就是空)，直接跳到 g</p></li>
<li><p>c: 将 currently running task 设置为 task X</p></li>
<li><p>d: 执行 task X</p></li>
<li><p>e: 将 currently running task 设置为 null 并移出 task X</p></li>
<li><p>f: 在 microtask 中选出最早的任务 , 跳到 b</p></li>
<li><p>g: 结束 microtask 队列</p></li>
</ul>
</li>
<li><p>跳到第一步</p></li>
</ol>
<h1 id="articleHeader3">4. 浅析 Vue.js 中 nextTick 的实现</h1>
<p>在 Vue.js 中，其会异步执行 DOM 更新；当观察到数据变化时，Vue 将开启一个队列，并缓冲在同一事件循环中发生的所有数据改变。如果同一个 watcher 被多次触发，只会一次推入到队列中。这种在缓冲时去除重复数据对于避免不必要的计算和 DOM 操作上非常重要。然后，在下一个的事件循环“tick”中，Vue 刷新队列并执行实际（已去重的）工作。Vue 在内部尝试对异步队列使用原生的 <code>Promise.then</code> 和 <code>MutationObserver</code>，如果执行环境不支持，会采用 <code>setTimeout(fn, 0)</code> 代替。</p>
<p>《因为本人失误，原来此处内容拷贝了 <a href="https://www.zhihu.com/question/55364497" rel="nofollow noreferrer" target="_blank">https://www.zhihu.com/questio...</a> 这个回答，造成了侵权，深表歉意，已经删除，后续我会在 github 链接上重写本段》</p>
<p>而当我们希望在数据更新之后执行某些 DOM 操作，就需要使用 <code>nextTick</code> 函数来添加回调：</p>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="全选"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="// HTML
<div id=&quot;example&quot;>"{{"message"}}"</div>

// JS
var vm = new Vue({
  el: '#example',
  data: {
    message: '123'
  }
})
vm.message = 'new message' // 更改数据
vm.$el.textContent === 'new message' // false
Vue.nextTick(function () {
  vm.$el.textContent === 'new message' // true
})" title="" data-original-title="复制"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="放进笔记"></span>
      </div>
      </div><pre class="hljs php"><code><span class="hljs-comment">// HTML</span>
&lt;div id=<span class="hljs-string">"example"</span>&gt;"{{"message"}}"&lt;/div&gt;

<span class="hljs-comment">// JS</span>
<span class="hljs-keyword">var</span> vm = <span class="hljs-keyword">new</span> Vue({
  el: <span class="hljs-string">'#example'</span>,
  data: {
    message: <span class="hljs-string">'123'</span>
  }
})
vm.message = <span class="hljs-string">'new message'</span> <span class="hljs-comment">// 更改数据</span>
vm.$el.textContent === <span class="hljs-string">'new message'</span> <span class="hljs-comment">// false</span>
Vue.nextTick(<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-params">()</span> </span>{
  vm.$el.textContent === <span class="hljs-string">'new message'</span> <span class="hljs-comment">// true</span>
})</code></pre>
<p>在组件内使用 vm.$nextTick() 实例方法特别方便，因为它不需要全局 Vue ，并且回调函数中的 this 将自动绑定到当前的 Vue 实例上：</p>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="全选"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="Vue.component('example', {
  template: '<span>"{{" message "}}"</span>',
  data: function () {
    return {
      message: '没有更新'
    }
  },
  methods: {
    updateMessage: function () {
      this.message = '更新完成'
      console.log(this.$el.textContent) // => '没有更新'
      this.$nextTick(function () {
        console.log(this.$el.textContent) // => '更新完成'
      })
    }
  }
})" title="" data-original-title="复制"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="放进笔记"></span>
      </div>
      </div><pre class="hljs javascript"><code>Vue.component(<span class="hljs-string">'example'</span>, {
  <span class="hljs-attr">template</span>: <span class="hljs-string">'&lt;span&gt;"{{" message "}}"&lt;/span&gt;'</span>,
  <span class="hljs-attr">data</span>: <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params"></span>) </span>{
    <span class="hljs-keyword">return</span> {
      <span class="hljs-attr">message</span>: <span class="hljs-string">'没有更新'</span>
    }
  },
  <span class="hljs-attr">methods</span>: {
    <span class="hljs-attr">updateMessage</span>: <span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params"></span>) </span>{
      <span class="hljs-keyword">this</span>.message = <span class="hljs-string">'更新完成'</span>
      <span class="hljs-built_in">console</span>.log(<span class="hljs-keyword">this</span>.$el.textContent) <span class="hljs-comment">// =&gt; '没有更新'</span>
      <span class="hljs-keyword">this</span>.$nextTick(<span class="hljs-function"><span class="hljs-keyword">function</span> (<span class="hljs-params"></span>) </span>{
        <span class="hljs-built_in">console</span>.log(<span class="hljs-keyword">this</span>.$el.textContent) <span class="hljs-comment">// =&gt; '更新完成'</span>
      })
    }
  }
})</code></pre>
<p>src/core/util/env</p>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="全选"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="
/**
 * 使用 MicroTask 来异步执行批次任务
 */
export const nextTick = (function() {
  // 需要执行的回调列表
  const callbacks = [];

  // 是否处于挂起状态
  let pending = false;

  // 时间函数句柄
  let timerFunc;

  // 执行并且清空所有的回调列表
  function nextTickHandler() {
    pending = false;
    const copies = callbacks.slice(0);
    callbacks.length = 0;
    for (let i = 0; i < copies.length; i++) {
      copies[i]();
    }
  }

  // nextTick 的回调会被加入到 MicroTask 队列中，这里我们主要通过原生的 Promise 与 MutationObserver 实现
  /* istanbul ignore if */
  if (typeof Promise !== 'undefined' &amp;&amp; isNative(Promise)) {
    let p = Promise.resolve();
    let logError = err => {
      console.error(err);
    };
    timerFunc = () => {
      p.then(nextTickHandler).catch(logError);

      // 在部分 iOS 系统下的 UIWebViews 中，Promise.then 可能并不会被清空，因此我们需要添加额外操作以触发
      if (isIOS) setTimeout(noop);
    };
  } else if (
    typeof MutationObserver !== 'undefined' &amp;&amp;
    (isNative(MutationObserver) ||
      // PhantomJS and iOS 7.x
      MutationObserver.toString() === '[object MutationObserverConstructor]')
  ) {
    // 当 Promise 不可用时候使用 MutationObserver
    // e.g. PhantomJS IE11, iOS7, Android 4.4
    let counter = 1;
    let observer = new MutationObserver(nextTickHandler);
    let textNode = document.createTextNode(String(counter));
    observer.observe(textNode, {
      characterData: true
    });
    timerFunc = () => {
      counter = (counter + 1) % 2;
      textNode.data = String(counter);
    };
  } else {
    // 如果都不存在，则回退使用 setTimeout
    /* istanbul ignore next */
    timerFunc = () => {
      setTimeout(nextTickHandler, 0);
    };
  }

  return function queueNextTick(cb?: Function, ctx?: Object) {
    let _resolve;
    callbacks.push(() => {
      if (cb) {
        try {
          cb.call(ctx);
        } catch (e) {
          handleError(e, ctx, 'nextTick');
        }
      } else if (_resolve) {
        _resolve(ctx);
      }
    });
    if (!pending) {
      pending = true;
      timerFunc();
    }

    // 如果没有传入回调，则表示以异步方式调用
    if (!cb &amp;&amp; typeof Promise !== 'undefined') {
      return new Promise((resolve, reject) => {
        _resolve = resolve;
      });
    }
  };
})();" title="" data-original-title="复制"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="放进笔记"></span>
      </div>
      </div><pre class="hljs javascript"><code>
<span class="hljs-comment">/**
 * 使用 MicroTask 来异步执行批次任务
 */</span>
<span class="hljs-keyword">export</span> <span class="hljs-keyword">const</span> nextTick = (<span class="hljs-function"><span class="hljs-keyword">function</span>(<span class="hljs-params"></span>) </span>{
  <span class="hljs-comment">// 需要执行的回调列表</span>
  <span class="hljs-keyword">const</span> callbacks = [];

  <span class="hljs-comment">// 是否处于挂起状态</span>
  <span class="hljs-keyword">let</span> pending = <span class="hljs-literal">false</span>;

  <span class="hljs-comment">// 时间函数句柄</span>
  <span class="hljs-keyword">let</span> timerFunc;

  <span class="hljs-comment">// 执行并且清空所有的回调列表</span>
  <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">nextTickHandler</span>(<span class="hljs-params"></span>) </span>{
    pending = <span class="hljs-literal">false</span>;
    <span class="hljs-keyword">const</span> copies = callbacks.slice(<span class="hljs-number">0</span>);
    callbacks.length = <span class="hljs-number">0</span>;
    <span class="hljs-keyword">for</span> (<span class="hljs-keyword">let</span> i = <span class="hljs-number">0</span>; i &lt; copies.length; i++) {
      copies[i]();
    }
  }

  <span class="hljs-comment">// nextTick 的回调会被加入到 MicroTask 队列中，这里我们主要通过原生的 Promise 与 MutationObserver 实现</span>
  <span class="hljs-comment">/* istanbul ignore if */</span>
  <span class="hljs-keyword">if</span> (<span class="hljs-keyword">typeof</span> <span class="hljs-built_in">Promise</span> !== <span class="hljs-string">'undefined'</span> &amp;&amp; isNative(<span class="hljs-built_in">Promise</span>)) {
    <span class="hljs-keyword">let</span> p = <span class="hljs-built_in">Promise</span>.resolve();
    <span class="hljs-keyword">let</span> logError = <span class="hljs-function"><span class="hljs-params">err</span> =&gt;</span> {
      <span class="hljs-built_in">console</span>.error(err);
    };
    timerFunc = <span class="hljs-function"><span class="hljs-params">()</span> =&gt;</span> {
      p.then(nextTickHandler).catch(logError);

      <span class="hljs-comment">// 在部分 iOS 系统下的 UIWebViews 中，Promise.then 可能并不会被清空，因此我们需要添加额外操作以触发</span>
      <span class="hljs-keyword">if</span> (isIOS) setTimeout(noop);
    };
  } <span class="hljs-keyword">else</span> <span class="hljs-keyword">if</span> (
    <span class="hljs-keyword">typeof</span> MutationObserver !== <span class="hljs-string">'undefined'</span> &amp;&amp;
    (isNative(MutationObserver) ||
      <span class="hljs-comment">// PhantomJS and iOS 7.x</span>
      MutationObserver.toString() === <span class="hljs-string">'[object MutationObserverConstructor]'</span>)
  ) {
    <span class="hljs-comment">// 当 Promise 不可用时候使用 MutationObserver</span>
    <span class="hljs-comment">// e.g. PhantomJS IE11, iOS7, Android 4.4</span>
    <span class="hljs-keyword">let</span> counter = <span class="hljs-number">1</span>;
    <span class="hljs-keyword">let</span> observer = <span class="hljs-keyword">new</span> MutationObserver(nextTickHandler);
    <span class="hljs-keyword">let</span> textNode = <span class="hljs-built_in">document</span>.createTextNode(<span class="hljs-built_in">String</span>(counter));
    observer.observe(textNode, {
      <span class="hljs-attr">characterData</span>: <span class="hljs-literal">true</span>
    });
    timerFunc = <span class="hljs-function"><span class="hljs-params">()</span> =&gt;</span> {
      counter = (counter + <span class="hljs-number">1</span>) % <span class="hljs-number">2</span>;
      textNode.data = <span class="hljs-built_in">String</span>(counter);
    };
  } <span class="hljs-keyword">else</span> {
    <span class="hljs-comment">// 如果都不存在，则回退使用 setTimeout</span>
    <span class="hljs-comment">/* istanbul ignore next */</span>
    timerFunc = <span class="hljs-function"><span class="hljs-params">()</span> =&gt;</span> {
      setTimeout(nextTickHandler, <span class="hljs-number">0</span>);
    };
  }

  <span class="hljs-keyword">return</span> <span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">queueNextTick</span>(<span class="hljs-params">cb?: Function, ctx?: Object</span>) </span>{
    <span class="hljs-keyword">let</span> _resolve;
    callbacks.push(<span class="hljs-function"><span class="hljs-params">()</span> =&gt;</span> {
      <span class="hljs-keyword">if</span> (cb) {
        <span class="hljs-keyword">try</span> {
          cb.call(ctx);
        } <span class="hljs-keyword">catch</span> (e) {
          handleError(e, ctx, <span class="hljs-string">'nextTick'</span>);
        }
      } <span class="hljs-keyword">else</span> <span class="hljs-keyword">if</span> (_resolve) {
        _resolve(ctx);
      }
    });
    <span class="hljs-keyword">if</span> (!pending) {
      pending = <span class="hljs-literal">true</span>;
      timerFunc();
    }

    <span class="hljs-comment">// 如果没有传入回调，则表示以异步方式调用</span>
    <span class="hljs-keyword">if</span> (!cb &amp;&amp; <span class="hljs-keyword">typeof</span> <span class="hljs-built_in">Promise</span> !== <span class="hljs-string">'undefined'</span>) {
      <span class="hljs-keyword">return</span> <span class="hljs-keyword">new</span> <span class="hljs-built_in">Promise</span>(<span class="hljs-function">(<span class="hljs-params">resolve, reject</span>) =&gt;</span> {
        _resolve = resolve;
      });
    }
  };
})();</code></pre>
<h1 id="articleHeader4">5. 延伸阅读</h1>
<ul><li><p><a href="https://parg.co/b2s" rel="nofollow noreferrer" target="_blank">深入浅出 Node.js 全栈架构 - Node.js 事件循环机制详解与实践</a></p></li></ul>

                
{{< /raw >}}

# 版权声明
本文资源来源互联网，仅供学习研究使用，版权归该资源的合法拥有者所有，

本文仅用于学习、研究和交流目的。转载请注明出处、完整链接以及原作者。

原作者若认为本站侵犯了您的版权，请联系我们，我们会立即删除！

## 原文标题
JavaScript Event Loop 机制详解与 Vue.js 中实践应用

## 原文链接
[https://segmentfault.com/a/1190000011044242](https://segmentfault.com/a/1190000011044242)

