---
title: '算法系列——JavaScript中广度优先搜索思想实现' 
date: 2018-12-26 2:30:14
hidden: true
slug: qfdlek30m
categories: [reprint]
---

{{< raw >}}

                    
<h3 id="articleHeader0">什么是广度优先搜索？</h3>
<p>如果只是是背概念，幼儿园的小朋友都能背下来念给你听。</p>
<p>假设看这篇文章的都和我一样是个前端工程师，我们要从广度优先搜索（BFS）中学到什么？如果你看完这篇文章能够回答这个问题，那么你已经看懂了。</p>
<p>广度优先搜索不是排序算法，它和快速排序、选择排序、冒泡排序等不一样，你听过二分查找吗？<strong>广度优先搜索是一种查找算法。</strong></p>
<p><strong>它可以用来解决2类问题：</strong></p>
<p>1、节点A能不能到节点N？</p>
<p>2、如果能到，它的最短路径是什么？</p>
<h3 id="articleHeader1">我们将要了解到的知识</h3>
<p>1、图</p>
<p>2、散列表</p>
<p>3、队列</p>
<p>4、算法实现</p>
<h3 id="articleHeader2">图</h3>
<p>学过数据结构的同学对图比较了解了，没学过的也没关系，图表示的关系网络，你看过神经网络图、人际关系图、家族图谱图、以及最常见的地图吗？如果你都没见过，还是别学了......</p>
<p>下面我将展示一个简单的地图。</p>
<p><span class="img-wrap"><img data-src="/img/bVYqmW?w=1080&amp;h=1440" src="https://static.alili.tech/img/bVYqmW?w=1080&amp;h=1440" alt="地图" title="地图" style="cursor: pointer; display: inline;"></span></p>
<p>思考一个问题，假设你现在在北京，现在想跳槽到广州，行李以及收拾好了，跟老板辞职也通过了，现在你想将所有可以到达广州的路线找出来（这里忽略你搭地铁或者打的的时间，而且模拟北京不能直达广州的情况），都有那几条路线？</p>
<p>请思考1分钟....</p>
<p>确保你真的思考的前提下，我来猜一下你是如何找到北京到广州的所有路线的！</p>
<p>1、你眼睛先盯着北京，然后发现可以到达武汉，接着发现武汉可以到达广州，ok，第一条路线完成。</p>
<p>北京 -&gt; 武汉 -&gt; 广州</p>
<p>2、接着你又返回北京，你突然记得武汉可以到达上海，所以你又从北京到达了武汉，武汉去了上海，发现上海可以到达广州。第二条路线完成。</p>
<p>北京 -&gt; 武汉 -&gt; 上海 -&gt; 广州</p>
<p>3、再次回到北京，你记得武汉还有一条去往西藏的路线，但是走了一遍发现西藏不能到达广州。</p>
<p>4、回到北京，现在出发去上海，接着你发现上海直接到达了广州，第三条路线完成。</p>
<p>北京 -&gt; 上海 -&gt; 广州</p>
<p>5、回到北京，再次去上海，接着到武汉，哇塞，又能到广州了。第四条路线完成。</p>
<p>北京 -&gt; 上海 -&gt; 武汉 -&gt; 广州</p>
<p>现在找完了所有路线，一共4条，但是，这不是广度优先搜索的思路。不过已经很接近了，广度优先搜索没有那么深奥，你完全可以用正常逻辑来理解。</p>
<p>还记得上面我们说到广度优先搜索解决的问题吗？</p>
<p>1、节点A能不能到节点N？</p>
<p>2、如果能到，它的最短路径是什么？</p>
<p><strong>广度优先搜索判断北京到广州的路径：</strong></p>
<p>1、首先你在北京；</p>
<p>2、接着你问自己，北京能不能直接到达广州？你将地图搜索了一下，发现北京只能到达武汉和上海，这说明你完成了第一步搜索。上海和武汉属于北京的“一度空间”，具有优先搜索权；</p>
<p>3、西藏和广州属于北京的“二度空间”，当你在一度空间搜索不到目标时，就在二度空间搜索，如果还是搜索不到，就一直往N度空间搜索下去，直至搜索完整个地图。用正常人的理解就是，第2步时你搜索了武汉和上海都没有找到目标，就分别搜索武汉和上海的临近节点，发现武汉和上海都可以直接到达广州；</p>
<p>4、你根据这种方法很快就回答了广度优先搜索提出的2个问题，找到了北京到广州的路线，并且找到了2条可能是最短的路线：北京 -&gt; 武汉 -&gt; 广州，北京 -&gt; 上海 -&gt; 广州。实际问题中，我们需要计算的节点间的距离找到最短的路线，这里不做计算，只分析思路。</p>
<p>图本身的概念挺多，包括节点、边界、有向、无向，但不需要学习这些知识也能理解广度优先搜索的思想。</p>
<h3 id="articleHeader3">散列表</h3>
<p>上面的地图向我们展示了如何用广度优先搜索的思想找到北京到广州的最短路线。那么散列表是什么？它在广度优先搜索中的作用是什么？</p>
<p>为了回答这2个问题，我想请你回忆一下JavaScript中的Map，如果不了解Map，也没关系，回忆Object也行。<strong>Object近似的可以看成是散列表的数据结构。</strong></p>
<p>散列表也叫做哈希表，它的<strong>平均时间复杂度是O(1)</strong>，它长的也不奇怪，就是key，value结构。</p>
<p>我们可以用简单的Object结构来表示节点之间的关系：</p>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="全选"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="const map = {
  '武汉': {
    '广州': {},
    '西藏': {},
    '上海': {}
  },
  '上海': {
    '武汉': {},
    '广州': {}
  }
}" title="" data-original-title="复制"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="放进笔记"></span>
      </div>
      </div><pre class="javascript hljs"><code class="javascript"><span class="hljs-keyword">const</span> map = {
  <span class="hljs-string">'武汉'</span>: {
    <span class="hljs-string">'广州'</span>: {},
    <span class="hljs-string">'西藏'</span>: {},
    <span class="hljs-string">'上海'</span>: {}
  },
  <span class="hljs-string">'上海'</span>: {
    <span class="hljs-string">'武汉'</span>: {},
    <span class="hljs-string">'广州'</span>: {}
  }
}</code></pre>
<p>散列表的内部实现是一种链组结构，也就是链表和数组的复合体。使用散列表的时候，要注意，key尽量不要重复，要分散，如果有重复，就会造成冲突，导致时间复杂度不是O(1)了。</p>
<h3 id="articleHeader4">队列</h3>
<p>有了图的存储结构，就能用代码来实现查找操作，但是在这之前，我们还要了解队列的思想。</p>
<p>你应该有过在学校饭堂排队打饭的体验，在确保没人插队的前提下，排队越前的就越先打到饭，然后离开，新来的要打饭的人必须排队到队列的末尾。专业名词叫做“先进先出”。</p>
<p>在广度优先搜索中，我们需要用到队列的这种思想来实现查找。JavaScript可以用数组模拟队列，你不需要单独构建一个队列的数据结构。</p>
<h3 id="articleHeader5">算法实现</h3>
<p>那么，广度优先搜索是如何用队列实现的呢？</p>
<p>想要回答这个问题，我们结合前面讲过的图、散列表、队列一起来解答。</p>
<p>先要明白一点，广度优先搜索没有唯一的算法，不同的图实现的方法不一样，但是思想是一致的，主要跟你的图对应的存储结构有关。复杂的图可能使用多张表来存储数据。</p>
<p>这里我采用的方法是根据维度空间来建立数据模型。首先找到一维空间的路线，北京 -&gt; 武汉，北京 -&gt; 上海。然后是二维空间的路线。建立了下面这个模型：</p>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="全选"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="const map = {
  '武汉': {
    '广州': {},
    '西藏': {},
    '上海': {}
  },
  '上海': {
    '武汉': {},
    '广州': {}
  }
}" title="" data-original-title="复制"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="放进笔记"></span>
      </div>
      </div><pre class="javascript hljs"><code class="javascript"><span class="hljs-keyword">const</span> map = {
  <span class="hljs-string">'武汉'</span>: {
    <span class="hljs-string">'广州'</span>: {},
    <span class="hljs-string">'西藏'</span>: {},
    <span class="hljs-string">'上海'</span>: {}
  },
  <span class="hljs-string">'上海'</span>: {
    <span class="hljs-string">'武汉'</span>: {},
    <span class="hljs-string">'广州'</span>: {}
  }
}</code></pre>
<p><strong>JavaScript代码完整实现，利用递归和广度优先搜索的思想实现。</strong></p>
<p>思路：构造二度空间散列表，我们只需要遍历一度空间，然后用递归遍历二度甚至N度空间即可，但是递归要注意内存溢出的问题，前端不宜做大量数据的算法操作。</p>
<div class="widget-codetool" style="display:none;">
      <div class="widget-codetool--inner">
      <span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="全选"></span>
      <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="const map = {
  '武汉': {
    '广州': {},
    '西藏': {},
    '上海': {}
  },
  '上海': {
    '武汉': {},
    '广州': {}
  }
}
function breadthSearch(obj, goal, arr = ['北京']) {
  for(let key in obj) {
    //遍历一度空间
    if (arr.indexOf(key) < 0) {
      //如果数组中不存在当前的key，就push
      arr.push(key)
      if (key === goal) {
        //如果key是要查找的目标节点，直接返回
        return arr
      } else {
        //如果key不是要查找的目标节点，继续递归
        return breadthSearch(obj[key], goal, arr)
      }
    }
  }
}

const s = breadthSearch(map, '广州')

console.log(s) //[&quot;北京&quot;, &quot;武汉&quot;, &quot;广州&quot;]" title="" data-original-title="复制"></span>
      <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="放进笔记"></span>
      </div>
      </div><pre class="javascript hljs"><code class="javascript"><span class="hljs-keyword">const</span> map = {
  <span class="hljs-string">'武汉'</span>: {
    <span class="hljs-string">'广州'</span>: {},
    <span class="hljs-string">'西藏'</span>: {},
    <span class="hljs-string">'上海'</span>: {}
  },
  <span class="hljs-string">'上海'</span>: {
    <span class="hljs-string">'武汉'</span>: {},
    <span class="hljs-string">'广州'</span>: {}
  }
}
<span class="hljs-function"><span class="hljs-keyword">function</span> <span class="hljs-title">breadthSearch</span>(<span class="hljs-params">obj, goal, arr = [<span class="hljs-string">'北京'</span>]</span>) </span>{
  <span class="hljs-keyword">for</span>(<span class="hljs-keyword">let</span> key <span class="hljs-keyword">in</span> obj) {
    <span class="hljs-comment">//遍历一度空间</span>
    <span class="hljs-keyword">if</span> (arr.indexOf(key) &lt; <span class="hljs-number">0</span>) {
      <span class="hljs-comment">//如果数组中不存在当前的key，就push</span>
      arr.push(key)
      <span class="hljs-keyword">if</span> (key === goal) {
        <span class="hljs-comment">//如果key是要查找的目标节点，直接返回</span>
        <span class="hljs-keyword">return</span> arr
      } <span class="hljs-keyword">else</span> {
        <span class="hljs-comment">//如果key不是要查找的目标节点，继续递归</span>
        <span class="hljs-keyword">return</span> breadthSearch(obj[key], goal, arr)
      }
    }
  }
}

<span class="hljs-keyword">const</span> s = breadthSearch(map, <span class="hljs-string">'广州'</span>)

<span class="hljs-built_in">console</span>.log(s) <span class="hljs-comment">//["北京", "武汉", "广州"]</span></code></pre>
<h3 id="articleHeader6">总结</h3>
<p>看到这里，广度优先搜索的思想以及JavaScript模拟实现到这里就结束了，前端工程师不需要完全掌握它，而是学会分析这种问题，思维比算法的实现更重要，如果给你换一个图，你就不会用JavaScript实现也没有关系，能用文字表达出思路就够了。</p>
<p>广度优先针对的是无权图的搜索，如果给节点之间的边加上权重距离，就要用到其他算法了，后面我会讲到狄克斯特拉算法和贪婪算法等思想的实现。</p>
<p>与广度优先搜索相对的，就是深度优先搜索，我不打算在这一章讲，回到文章一开始的问题，你从广度优先搜索（BFS）中学到了什么？现在能回答了吗？</p>

                
{{< /raw >}}

# 版权声明
本文资源来源互联网，仅供学习研究使用，版权归该资源的合法拥有者所有，

本文仅用于学习、研究和交流目的。转载请注明出处、完整链接以及原作者。

原作者若认为本站侵犯了您的版权，请联系我们，我们会立即删除！

## 原文标题
算法系列——JavaScript中广度优先搜索思想实现

## 原文链接
[https://segmentfault.com/a/1190000011983269](https://segmentfault.com/a/1190000011983269)

