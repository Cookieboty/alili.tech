---
title: 'Flex 布局教程' 
date: 2018-11-20 2:30:10
hidden: true
slug: o1yodyym19t
categories: [reprint]
---

{{< raw >}}
<h2 id="articleHeader0">&#x7B80;&#x4ECB;</h2><p>Flex &#x662F; Flexible Box &#x7684;&#x7F29;&#x5199;&#xFF0C;&#x610F;&#x4E3A;&quot;&#x5F39;&#x6027;&#x5E03;&#x5C40;&quot;&#xFF0C;&#x7528;&#x6765;&#x4E3A;&#x76D2;&#x72B6;&#x6A21;&#x578B;&#x63D0;&#x4F9B;&#x6700;&#x5927;&#x7684;&#x7075;&#x6D3B;&#x6027;&#x3002;</p><h2 id="articleHeader1">&#x517C;&#x5BB9;&#x6027;</h2><p>IE10+&#x3001;Chrom21+&#x3001;Firefox22+&#x3001;Safari6.1+</p><h2 id="articleHeader2">&#x57FA;&#x672C;&#x6982;&#x5FF5;</h2><div class="widget-codetool" style="display:none"><div class="widget-codetool--inner"><span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span> <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="//&#x4EFB;&#x4F55;&#x4E00;&#x4E2A;&#x5BB9;&#x5668;&#x90FD;&#x53EF;&#x4EE5;&#x6307;&#x5B9A;&#x4E3A; Flex &#x5E03;&#x5C40;&#x3002;
// &#x6CE8;&#x610F;&#xFF1A;Webkit &#x5185;&#x6838;&#x7684;&#x6D4F;&#x89C8;&#x5668;&#xFF0C;&#x5FC5;&#x987B;&#x52A0;&#x4E0A;-webkit&#x524D;&#x7F00;&#x3002;
// &#x8BBE;&#x4E3A; Flex &#x5E03;&#x5C40;&#x4EE5;&#x540E;&#xFF0C;&#x5B50;&#x5143;&#x7D20;&#x7684;float&#x3001;clear&#x548C;vertical-align&#x5C5E;&#x6027;&#x5C06;&#x5931;&#x6548;&#x3002;
.box {
    display: -webkit-flex; /* Safari */
    display: flex;
}
// &#x884C;&#x5185;&#x5143;&#x7D20;
.box {
    display: inline-flex
}" title="" data-original-title="&#x590D;&#x5236;"></span> <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span></div></div><pre class="hljs stylus"><code><span class="hljs-comment">//&#x4EFB;&#x4F55;&#x4E00;&#x4E2A;&#x5BB9;&#x5668;&#x90FD;&#x53EF;&#x4EE5;&#x6307;&#x5B9A;&#x4E3A; Flex &#x5E03;&#x5C40;&#x3002;</span>
<span class="hljs-comment">// &#x6CE8;&#x610F;&#xFF1A;Webkit &#x5185;&#x6838;&#x7684;&#x6D4F;&#x89C8;&#x5668;&#xFF0C;&#x5FC5;&#x987B;&#x52A0;&#x4E0A;-webkit&#x524D;&#x7F00;&#x3002;</span>
<span class="hljs-comment">// &#x8BBE;&#x4E3A; Flex &#x5E03;&#x5C40;&#x4EE5;&#x540E;&#xFF0C;&#x5B50;&#x5143;&#x7D20;&#x7684;float&#x3001;clear&#x548C;vertical-align&#x5C5E;&#x6027;&#x5C06;&#x5931;&#x6548;&#x3002;</span>
<span class="hljs-selector-class">.box</span> {
    <span class="hljs-attribute">display</span>: -webkit-flex; <span class="hljs-comment">/* Safari */</span>
    <span class="hljs-attribute">display</span>: flex;
}
<span class="hljs-comment">// &#x884C;&#x5185;&#x5143;&#x7D20;</span>
<span class="hljs-selector-class">.box</span> {
    <span class="hljs-attribute">display</span>: inline-flex
}</code></pre><p>&#x91C7;&#x7528; Flex &#x5E03;&#x5C40;&#x7684;&#x5143;&#x7D20;&#xFF0C;&#x79F0;&#x4E3A; Flex &#x5BB9;&#x5668;&#xFF08;flex container&#xFF09;&#xFF0C;&#x7B80;&#x79F0;&quot;&#x5BB9;&#x5668;&quot;&#x3002;&#x5B83;&#x7684;&#x6240;&#x6709;&#x5B50;&#x5143;&#x7D20;&#x81EA;&#x52A8;&#x6210;&#x4E3A;&#x5BB9;&#x5668;&#x6210;&#x5458;&#xFF0C;&#x79F0;&#x4E3A; Flex &#x9879;&#x76EE;&#xFF08;flex item&#xFF09;&#xFF0C;&#x7B80;&#x79F0;&quot;&#x9879;&#x76EE;&quot;&#x3002;</p><p><span class="img-wrap"><img data-src="/img/bVTiJQ?w=563&amp;h=333" src="https://static.alili.tech/img/bVTiJQ?w=563&amp;h=333" alt="clipboard.png" title="clipboard.png" style="cursor:pointer"></span><br>&#x5BB9;&#x5668;&#x9ED8;&#x8BA4;&#x5B58;&#x5728;&#x4E24;&#x6839;&#x8F74;&#xFF1A;&#x6C34;&#x5E73;&#x7684;&#x4E3B;&#x8F74;&#xFF08;main axis&#xFF09;&#x548C;&#x5782;&#x76F4;&#x7684;&#x4EA4;&#x53C9;&#x8F74;&#xFF08;cross axis&#xFF09;&#x3002;&#x4E3B;&#x8F74;&#x7684;&#x5F00;&#x59CB;&#x4F4D;&#x7F6E;&#xFF08;&#x4E0E;&#x8FB9;&#x6846;&#x7684;&#x4EA4;&#x53C9;&#x70B9;&#xFF09;&#x53EB;&#x505A;main start&#xFF0C;&#x7ED3;&#x675F;&#x4F4D;&#x7F6E;&#x53EB;&#x505A;main end&#xFF1B;&#x4EA4;&#x53C9;&#x8F74;&#x7684;&#x5F00;&#x59CB;&#x4F4D;&#x7F6E;&#x53EB;&#x505A;cross start&#xFF0C;&#x7ED3;&#x675F;&#x4F4D;&#x7F6E;&#x53EB;&#x505A;cross end&#x3002;</p><p>&#x9879;&#x76EE;&#x9ED8;&#x8BA4;&#x6CBF;&#x4E3B;&#x8F74;&#x6392;&#x5217;&#x3002;&#x5355;&#x4E2A;&#x9879;&#x76EE;&#x5360;&#x636E;&#x7684;&#x4E3B;&#x8F74;&#x7A7A;&#x95F4;&#x53EB;&#x505A;main size&#xFF0C;&#x5360;&#x636E;&#x7684;&#x4EA4;&#x53C9;&#x8F74;&#x7A7A;&#x95F4;&#x53EB;&#x505A;cross size&#x3002;</p><h2 id="articleHeader3">&#x5BB9;&#x5668;&#x7684;&#x5C5E;&#x6027;</h2><p>1.flex-direction</p><div class="widget-codetool" style="display:none"><div class="widget-codetool--inner"><span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span> <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="// flex-direction&#x5C5E;&#x6027;&#x51B3;&#x5B9A;&#x4E3B;&#x8F74;&#x7684;&#x65B9;&#x5411;&#xFF08;&#x5373;&#x9879;&#x76EE;&#x7684;&#x6392;&#x5217;&#x65B9;&#x5411;&#xFF09;&#x3002;
// &#x4ED6;&#x53EF;&#x80FD;&#x6709;&#x56DB;&#x4E2A;&#x503C;
// row&#xFF08;&#x9ED8;&#x8BA4;&#x503C;&#xFF09;&#xFF1A;&#x4E3B;&#x8F74;&#x4E3A;&#x6C34;&#x5E73;&#x65B9;&#x5411;&#xFF0C;&#x8D77;&#x70B9;&#x5728;&#x5DE6;&#x7AEF;&#x3002;
// row-reverse&#xFF1A;&#x4E3B;&#x8F74;&#x4E3A;&#x6C34;&#x5E73;&#x65B9;&#x5411;&#xFF0C;&#x8D77;&#x70B9;&#x5728;&#x53F3;&#x7AEF;&#x3002;
// column&#xFF1A;&#x4E3B;&#x8F74;&#x4E3A;&#x5782;&#x76F4;&#x65B9;&#x5411;&#xFF0C;&#x8D77;&#x70B9;&#x5728;&#x4E0A;&#x6CBF;&#x3002;
// column-reverse&#xFF1A;&#x4E3B;&#x8F74;&#x4E3A;&#x5782;&#x76F4;&#x65B9;&#x5411;&#xFF0C;&#x8D77;&#x70B9;&#x5728;&#x4E0B;&#x6CBF;&#x3002;
.box {
  flex-direction: row | row-reverse | column | column-reverse;
} " title="" data-original-title="&#x590D;&#x5236;"></span> <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span></div></div><pre class="hljs maxima"><code>// flex-direction&#x5C5E;&#x6027;&#x51B3;&#x5B9A;&#x4E3B;&#x8F74;&#x7684;&#x65B9;&#x5411;&#xFF08;&#x5373;&#x9879;&#x76EE;&#x7684;&#x6392;&#x5217;&#x65B9;&#x5411;&#xFF09;&#x3002;
// &#x4ED6;&#x53EF;&#x80FD;&#x6709;&#x56DB;&#x4E2A;&#x503C;
// <span class="hljs-built_in">row</span>&#xFF08;&#x9ED8;&#x8BA4;&#x503C;&#xFF09;&#xFF1A;&#x4E3B;&#x8F74;&#x4E3A;&#x6C34;&#x5E73;&#x65B9;&#x5411;&#xFF0C;&#x8D77;&#x70B9;&#x5728;&#x5DE6;&#x7AEF;&#x3002;
// <span class="hljs-built_in">row</span>-<span class="hljs-built_in">reverse</span>&#xFF1A;&#x4E3B;&#x8F74;&#x4E3A;&#x6C34;&#x5E73;&#x65B9;&#x5411;&#xFF0C;&#x8D77;&#x70B9;&#x5728;&#x53F3;&#x7AEF;&#x3002;
// column&#xFF1A;&#x4E3B;&#x8F74;&#x4E3A;&#x5782;&#x76F4;&#x65B9;&#x5411;&#xFF0C;&#x8D77;&#x70B9;&#x5728;&#x4E0A;&#x6CBF;&#x3002;
// column-<span class="hljs-built_in">reverse</span>&#xFF1A;&#x4E3B;&#x8F74;&#x4E3A;&#x5782;&#x76F4;&#x65B9;&#x5411;&#xFF0C;&#x8D77;&#x70B9;&#x5728;&#x4E0B;&#x6CBF;&#x3002;
.<span class="hljs-built_in">box</span> {
  flex-direction: <span class="hljs-built_in">row</span> | <span class="hljs-built_in">row</span>-<span class="hljs-built_in">reverse</span> | column | column-<span class="hljs-built_in">reverse</span>;
} </code></pre><p><span class="img-wrap"><img data-src="/img/bVTiKE?w=796&amp;h=203" src="https://static.alili.tech/img/bVTiKE?w=796&amp;h=203" alt="clipboard.png" title="clipboard.png" style="cursor:pointer"></span></p><p>2.flex-wrap<br>&#x9ED8;&#x8BA4;&#x60C5;&#x51B5;&#x4E0B;&#xFF0C;&#x9879;&#x76EE;&#x90FD;&#x6392;&#x5728;&#x4E00;&#x6761;&#x7EBF;&#xFF08;&#x53C8;&#x79F0;&quot;&#x8F74;&#x7EBF;&quot;&#xFF09;&#x4E0A;&#x3002;flex-wrap&#x5C5E;&#x6027;&#x5B9A;&#x4E49;&#xFF0C;&#x5982;&#x679C;&#x4E00;&#x6761;&#x8F74;&#x7EBF;&#x6392;&#x4E0D;&#x4E0B;&#xFF0C;&#x5982;&#x4F55;&#x6362;&#x884C;&#x3002;</p><p><span class="img-wrap"><img data-src="/img/bVTiKL?w=798&amp;h=276" src="https://static.alili.tech/img/bVTiKL?w=798&amp;h=276" alt="clipboard.png" title="clipboard.png" style="cursor:pointer"></span></p><div class="widget-codetool" style="display:none"><div class="widget-codetool--inner"><span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span> <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text="// nowrap&#xFF08;&#x9ED8;&#x8BA4;&#xFF09;&#xFF1A;&#x4E0D;&#x6362;&#x884C;&#x3002;
// wrap&#xFF1A;&#x6362;&#x884C;&#xFF0C;&#x7B2C;&#x4E00;&#x884C;&#x5728;&#x4E0A;&#x65B9;&#x3002;
// wrap-reverse&#xFF1A;&#x6362;&#x884C;&#xFF0C;&#x7B2C;&#x4E00;&#x884C;&#x5728;&#x4E0B;&#x65B9;&#x3002;
.box{
  flex-wrap: nowrap | wrap | wrap-reverse;
}" title="" data-original-title="&#x590D;&#x5236;"></span> <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span></div></div><pre class="hljs lua"><code>// nowrap&#xFF08;&#x9ED8;&#x8BA4;&#xFF09;&#xFF1A;&#x4E0D;&#x6362;&#x884C;&#x3002;
// <span class="hljs-built_in">wrap</span>&#xFF1A;&#x6362;&#x884C;&#xFF0C;&#x7B2C;&#x4E00;&#x884C;&#x5728;&#x4E0A;&#x65B9;&#x3002;
// <span class="hljs-built_in">wrap</span>-reverse&#xFF1A;&#x6362;&#x884C;&#xFF0C;&#x7B2C;&#x4E00;&#x884C;&#x5728;&#x4E0B;&#x65B9;&#x3002;
.box{
  flex-<span class="hljs-built_in">wrap</span>: nowrap | <span class="hljs-built_in">wrap</span> | <span class="hljs-built_in">wrap</span>-reverse;
}</code></pre><p>3.flex-flow<br>flex-flow&#x5C5E;&#x6027;&#x662F;flex-direction&#x5C5E;&#x6027;&#x548C;flex-wrap&#x5C5E;&#x6027;&#x7684;&#x7B80;&#x5199;&#x5F62;&#x5F0F;&#xFF0C;&#x9ED8;&#x8BA4;&#x503C;&#x4E3A;row nowrap&#x3002;</p><div class="widget-codetool" style="display:none"><div class="widget-codetool--inner"><span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span> <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text=".box {
  flex-flow: &lt;flex-direction&gt; || &lt;flex-wrap&gt;;
}" title="" data-original-title="&#x590D;&#x5236;"></span> <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span></div></div><pre class="hljs css"><code><span class="hljs-selector-class">.box</span> {
  <span class="hljs-attribute">flex-flow</span>: &lt;flex-direction&gt; || &lt;flex-wrap&gt;;
}</code></pre><p>4.justify-content<br>justify-content&#x5C5E;&#x6027;&#x5B9A;&#x4E49;&#x4E86;&#x9879;&#x76EE;&#x5728;&#x4E3B;&#x8F74;&#x4E0A;&#x7684;&#x5BF9;&#x9F50;&#x65B9;&#x5F0F;&#x3002;</p><div class="widget-codetool" style="display:none"><div class="widget-codetool--inner"><span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span> <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text=".box {
  justify-content: flex-start | flex-end | center | space-between | space-around;
}
// &#x5B83;&#x53EF;&#x80FD;&#x53D6;5&#x4E2A;&#x503C;&#xFF0C;&#x5177;&#x4F53;&#x5BF9;&#x9F50;&#x65B9;&#x5F0F;&#x4E0E;&#x8F74;&#x7684;&#x65B9;&#x5411;&#x6709;&#x5173;&#x3002;&#x4E0B;&#x9762;&#x5047;&#x8BBE;&#x4E3B;&#x8F74;&#x4E3A;&#x4ECE;&#x5DE6;&#x5230;&#x53F3;&#x3002;
// flex-start&#xFF08;&#x9ED8;&#x8BA4;&#x503C;&#xFF09;&#xFF1A;&#x5DE6;&#x5BF9;&#x9F50;
// flex-end&#xFF1A;&#x53F3;&#x5BF9;&#x9F50;
// center&#xFF1A; &#x5C45;&#x4E2D;
// space-between&#xFF1A;&#x4E24;&#x7AEF;&#x5BF9;&#x9F50;&#xFF0C;&#x9879;&#x76EE;&#x4E4B;&#x95F4;&#x7684;&#x95F4;&#x9694;&#x90FD;&#x76F8;&#x7B49;&#x3002;
// space-around&#xFF1A;&#x6BCF;&#x4E2A;&#x9879;&#x76EE;&#x4E24;&#x4FA7;&#x7684;&#x95F4;&#x9694;&#x76F8;&#x7B49;&#x3002;&#x6240;&#x4EE5;&#xFF0C;&#x9879;&#x76EE;&#x4E4B;&#x95F4;&#x7684;&#x95F4;&#x9694;&#x6BD4;&#x9879;&#x76EE;&#x4E0E;&#x8FB9;&#x6846;&#x7684;&#x95F4;&#x9694;&#x5927;&#x4E00;&#x500D;&#x3002;" title="" data-original-title="&#x590D;&#x5236;"></span> <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span></div></div><pre class="hljs stylus"><code><span class="hljs-selector-class">.box</span> {
  <span class="hljs-attribute">justify-content</span>: flex-start | flex-end | center | space-between | space-around;
}
<span class="hljs-comment">// &#x5B83;&#x53EF;&#x80FD;&#x53D6;5&#x4E2A;&#x503C;&#xFF0C;&#x5177;&#x4F53;&#x5BF9;&#x9F50;&#x65B9;&#x5F0F;&#x4E0E;&#x8F74;&#x7684;&#x65B9;&#x5411;&#x6709;&#x5173;&#x3002;&#x4E0B;&#x9762;&#x5047;&#x8BBE;&#x4E3B;&#x8F74;&#x4E3A;&#x4ECE;&#x5DE6;&#x5230;&#x53F3;&#x3002;</span>
<span class="hljs-comment">// flex-start&#xFF08;&#x9ED8;&#x8BA4;&#x503C;&#xFF09;&#xFF1A;&#x5DE6;&#x5BF9;&#x9F50;</span>
<span class="hljs-comment">// flex-end&#xFF1A;&#x53F3;&#x5BF9;&#x9F50;</span>
<span class="hljs-comment">// center&#xFF1A; &#x5C45;&#x4E2D;</span>
<span class="hljs-comment">// space-between&#xFF1A;&#x4E24;&#x7AEF;&#x5BF9;&#x9F50;&#xFF0C;&#x9879;&#x76EE;&#x4E4B;&#x95F4;&#x7684;&#x95F4;&#x9694;&#x90FD;&#x76F8;&#x7B49;&#x3002;</span>
<span class="hljs-comment">// space-around&#xFF1A;&#x6BCF;&#x4E2A;&#x9879;&#x76EE;&#x4E24;&#x4FA7;&#x7684;&#x95F4;&#x9694;&#x76F8;&#x7B49;&#x3002;&#x6240;&#x4EE5;&#xFF0C;&#x9879;&#x76EE;&#x4E4B;&#x95F4;&#x7684;&#x95F4;&#x9694;&#x6BD4;&#x9879;&#x76EE;&#x4E0E;&#x8FB9;&#x6846;&#x7684;&#x95F4;&#x9694;&#x5927;&#x4E00;&#x500D;&#x3002;</span></code></pre><p><span class="img-wrap"><img data-src="/img/bVTiKY?w=637&amp;h=763" src="https://static.alili.tech/img/bVTiKY?w=637&amp;h=763" alt="clipboard.png" title="clipboard.png" style="cursor:pointer"></span></p><p>5.align-items<br>align-items&#x5C5E;&#x6027;&#x5B9A;&#x4E49;&#x9879;&#x76EE;&#x5728;&#x4EA4;&#x53C9;&#x8F74;&#x4E0A;&#x5982;&#x4F55;&#x5BF9;&#x9F50;&#x3002;</p><div class="widget-codetool" style="display:none"><div class="widget-codetool--inner"><span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span> <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text=".box {
  align-items: flex-start | flex-end | center | baseline | stretch;
}
// &#x5B83;&#x53EF;&#x80FD;&#x53D6;5&#x4E2A;&#x503C;&#x3002;&#x5177;&#x4F53;&#x7684;&#x5BF9;&#x9F50;&#x65B9;&#x5F0F;&#x4E0E;&#x4EA4;&#x53C9;&#x8F74;&#x7684;&#x65B9;&#x5411;&#x6709;&#x5173;&#xFF0C;&#x4E0B;&#x9762;&#x5047;&#x8BBE;&#x4EA4;&#x53C9;&#x8F74;&#x4ECE;&#x4E0A;&#x5230;&#x4E0B;&#x3002;
// flex-start&#xFF1A;&#x4EA4;&#x53C9;&#x8F74;&#x7684;&#x8D77;&#x70B9;&#x5BF9;&#x9F50;&#x3002;
// flex-end&#xFF1A;&#x4EA4;&#x53C9;&#x8F74;&#x7684;&#x7EC8;&#x70B9;&#x5BF9;&#x9F50;&#x3002;
// center&#xFF1A;&#x4EA4;&#x53C9;&#x8F74;&#x7684;&#x4E2D;&#x70B9;&#x5BF9;&#x9F50;&#x3002;
// baseline: &#x9879;&#x76EE;&#x7684;&#x7B2C;&#x4E00;&#x884C;&#x6587;&#x5B57;&#x7684;&#x57FA;&#x7EBF;&#x5BF9;&#x9F50;&#x3002;
// stretch&#xFF08;&#x9ED8;&#x8BA4;&#x503C;&#xFF09;&#xFF1A;&#x5982;&#x679C;&#x9879;&#x76EE;&#x672A;&#x8BBE;&#x7F6E;&#x9AD8;&#x5EA6;&#x6216;&#x8BBE;&#x4E3A;auto&#xFF0C;&#x5C06;&#x5360;&#x6EE1;&#x6574;&#x4E2A;&#x5BB9;&#x5668;&#x7684;&#x9AD8;&#x5EA6;&#x3002;
" title="" data-original-title="&#x590D;&#x5236;"></span> <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span></div></div><pre class="hljs stylus"><code><span class="hljs-selector-class">.box</span> {
  <span class="hljs-attribute">align-items</span>: flex-start | flex-end | center | baseline | stretch;
}
<span class="hljs-comment">// &#x5B83;&#x53EF;&#x80FD;&#x53D6;5&#x4E2A;&#x503C;&#x3002;&#x5177;&#x4F53;&#x7684;&#x5BF9;&#x9F50;&#x65B9;&#x5F0F;&#x4E0E;&#x4EA4;&#x53C9;&#x8F74;&#x7684;&#x65B9;&#x5411;&#x6709;&#x5173;&#xFF0C;&#x4E0B;&#x9762;&#x5047;&#x8BBE;&#x4EA4;&#x53C9;&#x8F74;&#x4ECE;&#x4E0A;&#x5230;&#x4E0B;&#x3002;</span>
<span class="hljs-comment">// flex-start&#xFF1A;&#x4EA4;&#x53C9;&#x8F74;&#x7684;&#x8D77;&#x70B9;&#x5BF9;&#x9F50;&#x3002;</span>
<span class="hljs-comment">// flex-end&#xFF1A;&#x4EA4;&#x53C9;&#x8F74;&#x7684;&#x7EC8;&#x70B9;&#x5BF9;&#x9F50;&#x3002;</span>
<span class="hljs-comment">// center&#xFF1A;&#x4EA4;&#x53C9;&#x8F74;&#x7684;&#x4E2D;&#x70B9;&#x5BF9;&#x9F50;&#x3002;</span>
<span class="hljs-comment">// baseline: &#x9879;&#x76EE;&#x7684;&#x7B2C;&#x4E00;&#x884C;&#x6587;&#x5B57;&#x7684;&#x57FA;&#x7EBF;&#x5BF9;&#x9F50;&#x3002;</span>
<span class="hljs-comment">// stretch&#xFF08;&#x9ED8;&#x8BA4;&#x503C;&#xFF09;&#xFF1A;&#x5982;&#x679C;&#x9879;&#x76EE;&#x672A;&#x8BBE;&#x7F6E;&#x9AD8;&#x5EA6;&#x6216;&#x8BBE;&#x4E3A;auto&#xFF0C;&#x5C06;&#x5360;&#x6EE1;&#x6574;&#x4E2A;&#x5BB9;&#x5668;&#x7684;&#x9AD8;&#x5EA6;&#x3002;</span>
</code></pre><p><span class="img-wrap"><img data-src="/img/bVTiLp?w=617&amp;h=786" src="https://static.alili.tech/img/bVTiLp?w=617&amp;h=786" alt="clipboard.png" title="clipboard.png" style="cursor:pointer"></span></p><p>6.align-content<br>align-content&#x5C5E;&#x6027;&#x5B9A;&#x4E49;&#x4E86;&#x591A;&#x6839;&#x8F74;&#x7EBF;&#x7684;&#x5BF9;&#x9F50;&#x65B9;&#x5F0F;&#x3002;&#x5982;&#x679C;&#x9879;&#x76EE;&#x53EA;&#x6709;&#x4E00;&#x6839;&#x8F74;&#x7EBF;&#xFF0C;&#x8BE5;&#x5C5E;&#x6027;&#x4E0D;&#x8D77;&#x4F5C;&#x7528;&#x3002;</p><div class="widget-codetool" style="display:none"><div class="widget-codetool--inner"><span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span> <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text=".box {
  align-content: flex-start | flex-end | center | space-between | space-around | stretch;
} 
// &#x8BE5;&#x5C5E;&#x6027;&#x53EF;&#x80FD;&#x53D6;6&#x4E2A;&#x503C;&#x3002;
// flex-start&#xFF1A;&#x4E0E;&#x4EA4;&#x53C9;&#x8F74;&#x7684;&#x8D77;&#x70B9;&#x5BF9;&#x9F50;&#x3002;
// flex-end&#xFF1A;&#x4E0E;&#x4EA4;&#x53C9;&#x8F74;&#x7684;&#x7EC8;&#x70B9;&#x5BF9;&#x9F50;&#x3002;
// center&#xFF1A;&#x4E0E;&#x4EA4;&#x53C9;&#x8F74;&#x7684;&#x4E2D;&#x70B9;&#x5BF9;&#x9F50;&#x3002;
// space-between&#xFF1A;&#x4E0E;&#x4EA4;&#x53C9;&#x8F74;&#x4E24;&#x7AEF;&#x5BF9;&#x9F50;&#xFF0C;&#x8F74;&#x7EBF;&#x4E4B;&#x95F4;&#x7684;&#x95F4;&#x9694;&#x5E73;&#x5747;&#x5206;&#x5E03;&#x3002;
// space-around&#xFF1A;&#x6BCF;&#x6839;&#x8F74;&#x7EBF;&#x4E24;&#x4FA7;&#x7684;&#x95F4;&#x9694;&#x90FD;&#x76F8;&#x7B49;&#x3002;&#x6240;&#x4EE5;&#xFF0C;&#x8F74;&#x7EBF;&#x4E4B;&#x95F4;&#x7684;&#x95F4;&#x9694;&#x6BD4;&#x8F74;&#x7EBF;&#x4E0E;&#x8FB9;&#x6846;&#x7684;&#x95F4;&#x9694;&#x5927;&#x4E00;&#x500D;&#x3002;
// stretch&#xFF08;&#x9ED8;&#x8BA4;&#x503C;&#xFF09;&#xFF1A;&#x8F74;&#x7EBF;&#x5360;&#x6EE1;&#x6574;&#x4E2A;&#x4EA4;&#x53C9;&#x8F74;&#x3002;
" title="" data-original-title="&#x590D;&#x5236;"></span> <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span></div></div><pre class="hljs stylus"><code><span class="hljs-selector-class">.box</span> {
  <span class="hljs-attribute">align-content</span>: flex-start | flex-end | center | space-between | space-around | stretch;
} 
<span class="hljs-comment">// &#x8BE5;&#x5C5E;&#x6027;&#x53EF;&#x80FD;&#x53D6;6&#x4E2A;&#x503C;&#x3002;</span>
<span class="hljs-comment">// flex-start&#xFF1A;&#x4E0E;&#x4EA4;&#x53C9;&#x8F74;&#x7684;&#x8D77;&#x70B9;&#x5BF9;&#x9F50;&#x3002;</span>
<span class="hljs-comment">// flex-end&#xFF1A;&#x4E0E;&#x4EA4;&#x53C9;&#x8F74;&#x7684;&#x7EC8;&#x70B9;&#x5BF9;&#x9F50;&#x3002;</span>
<span class="hljs-comment">// center&#xFF1A;&#x4E0E;&#x4EA4;&#x53C9;&#x8F74;&#x7684;&#x4E2D;&#x70B9;&#x5BF9;&#x9F50;&#x3002;</span>
<span class="hljs-comment">// space-between&#xFF1A;&#x4E0E;&#x4EA4;&#x53C9;&#x8F74;&#x4E24;&#x7AEF;&#x5BF9;&#x9F50;&#xFF0C;&#x8F74;&#x7EBF;&#x4E4B;&#x95F4;&#x7684;&#x95F4;&#x9694;&#x5E73;&#x5747;&#x5206;&#x5E03;&#x3002;</span>
<span class="hljs-comment">// space-around&#xFF1A;&#x6BCF;&#x6839;&#x8F74;&#x7EBF;&#x4E24;&#x4FA7;&#x7684;&#x95F4;&#x9694;&#x90FD;&#x76F8;&#x7B49;&#x3002;&#x6240;&#x4EE5;&#xFF0C;&#x8F74;&#x7EBF;&#x4E4B;&#x95F4;&#x7684;&#x95F4;&#x9694;&#x6BD4;&#x8F74;&#x7EBF;&#x4E0E;&#x8FB9;&#x6846;&#x7684;&#x95F4;&#x9694;&#x5927;&#x4E00;&#x500D;&#x3002;</span>
<span class="hljs-comment">// stretch&#xFF08;&#x9ED8;&#x8BA4;&#x503C;&#xFF09;&#xFF1A;&#x8F74;&#x7EBF;&#x5360;&#x6EE1;&#x6574;&#x4E2A;&#x4EA4;&#x53C9;&#x8F74;&#x3002;</span>
</code></pre><p><span class="img-wrap"><img data-src="/img/bVTiLD?w=620&amp;h=786" src="https://static.alili.tech/img/bVTiLD?w=620&amp;h=786" alt="clipboard.png" title="clipboard.png" style="cursor:pointer"></span></p><h2 id="articleHeader4">&#x9879;&#x76EE;&#x7684;&#x5C5E;&#x6027;</h2><p>1.order<br>order&#x5C5E;&#x6027;&#x5B9A;&#x4E49;&#x9879;&#x76EE;&#x7684;&#x6392;&#x5217;&#x987A;&#x5E8F;&#x3002;&#x6570;&#x503C;&#x8D8A;&#x5C0F;&#xFF0C;&#x6392;&#x5217;&#x8D8A;&#x9760;&#x524D;&#xFF0C;&#x9ED8;&#x8BA4;&#x4E3A;0&#x3002;</p><div class="widget-codetool" style="display:none"><div class="widget-codetool--inner"><span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span> <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text=".item {
  order: &lt;integer&gt;;
}
" title="" data-original-title="&#x590D;&#x5236;"></span> <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span></div></div><pre class="hljs css"><code><span class="hljs-selector-class">.item</span> {
  <span class="hljs-attribute">order</span>: &lt;integer&gt;;
}
</code></pre><p><span class="img-wrap"><img data-src="/img/bVTiMw?w=751&amp;h=480" src="https://static.alili.tech/img/bVTiMw?w=751&amp;h=480" alt="clipboard.png" title="clipboard.png" style="cursor:pointer"></span></p><p>2.flex-grow<br>flex-grow&#x5C5E;&#x6027;&#x5B9A;&#x4E49;&#x9879;&#x76EE;&#x7684;&#x653E;&#x5927;&#x6BD4;&#x4F8B;&#xFF0C;&#x9ED8;&#x8BA4;&#x4E3A;0&#xFF0C;&#x5373;&#x5982;&#x679C;&#x5B58;&#x5728;&#x5269;&#x4F59;&#x7A7A;&#x95F4;&#xFF0C;&#x4E5F;&#x4E0D;&#x653E;&#x5927;&#x3002;<br>&#x5982;&#x679C;&#x6240;&#x6709;&#x9879;&#x76EE;&#x7684;flex-grow&#x5C5E;&#x6027;&#x90FD;&#x4E3A;1&#xFF0C;&#x5219;&#x5B83;&#x4EEC;&#x5C06;&#x7B49;&#x5206;&#x5269;&#x4F59;&#x7A7A;&#x95F4;&#xFF08;&#x5982;&#x679C;&#x6709;&#x7684;&#x8BDD;&#xFF09;&#x3002;&#x5982;&#x679C;&#x4E00;&#x4E2A;&#x9879;&#x76EE;&#x7684;flex-grow&#x5C5E;&#x6027;&#x4E3A;2&#xFF0C;&#x5176;&#x4ED6;&#x9879;&#x76EE;&#x90FD;&#x4E3A;1&#xFF0C;&#x5219;&#x524D;&#x8005;&#x5360;&#x636E;&#x7684;&#x5269;&#x4F59;&#x7A7A;&#x95F4;&#x5C06;&#x6BD4;&#x5176;&#x4ED6;&#x9879;&#x591A;&#x4E00;&#x500D;&#x3002;</p><div class="widget-codetool" style="display:none"><div class="widget-codetool--inner"><span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span> <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text=".item {
  flex-grow: &lt;number&gt;; /* default 0 */
}
" title="" data-original-title="&#x590D;&#x5236;"></span> <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span></div></div><pre class="hljs css"><code><span class="hljs-selector-class">.item</span> {
  <span class="hljs-attribute">flex-grow</span>: &lt;number&gt;; <span class="hljs-comment">/* default 0 */</span>
}
</code></pre><p><span class="img-wrap"><img data-src="/img/bVTiSr?w=802&amp;h=211" src="https://static.alili.tech/img/bVTiSr?w=802&amp;h=211" alt="clipboard.png" title="clipboard.png" style="cursor:pointer"></span></p><p>3.flex-shrink<br>flex-shrink&#x5C5E;&#x6027;&#x5B9A;&#x4E49;&#x4E86;&#x9879;&#x76EE;&#x7684;&#x7F29;&#x5C0F;&#x6BD4;&#x4F8B;&#xFF0C;&#x9ED8;&#x8BA4;&#x4E3A;1&#xFF0C;&#x5373;&#x5982;&#x679C;&#x7A7A;&#x95F4;&#x4E0D;&#x8DB3;&#xFF0C;&#x8BE5;&#x9879;&#x76EE;&#x5C06;&#x7F29;&#x5C0F;&#x3002;<br>&#x5982;&#x679C;&#x6240;&#x6709;&#x9879;&#x76EE;&#x7684;flex-shrink&#x5C5E;&#x6027;&#x90FD;&#x4E3A;1&#xFF0C;&#x5F53;&#x7A7A;&#x95F4;&#x4E0D;&#x8DB3;&#x65F6;&#xFF0C;&#x90FD;&#x5C06;&#x7B49;&#x6BD4;&#x4F8B;&#x7F29;&#x5C0F;&#x3002;&#x5982;&#x679C;&#x4E00;&#x4E2A;&#x9879;&#x76EE;&#x7684;flex-shrink&#x5C5E;&#x6027;&#x4E3A;0&#xFF0C;&#x5176;&#x4ED6;&#x9879;&#x76EE;&#x90FD;&#x4E3A;1&#xFF0C;&#x5219;&#x7A7A;&#x95F4;&#x4E0D;&#x8DB3;&#x65F6;&#xFF0C;&#x524D;&#x8005;&#x4E0D;&#x7F29;&#x5C0F;&#x3002;</p><p>&#x8D1F;&#x503C;&#x5BF9;&#x8BE5;&#x5C5E;&#x6027;&#x65E0;&#x6548;</p><div class="widget-codetool" style="display:none"><div class="widget-codetool--inner"><span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span> <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text=".item {
  flex-shrink: &lt;number&gt;; /* default 1 */
}
" title="" data-original-title="&#x590D;&#x5236;"></span> <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span></div></div><pre class="hljs css"><code><span class="hljs-selector-class">.item</span> {
  <span class="hljs-attribute">flex-shrink</span>: &lt;number&gt;; <span class="hljs-comment">/* default 1 */</span>
}
</code></pre><p>4.flex-basis<br>flex-basis&#x5C5E;&#x6027;&#x5B9A;&#x4E49;&#x4E86;&#x5728;&#x5206;&#x914D;&#x591A;&#x4F59;&#x7A7A;&#x95F4;&#x4E4B;&#x524D;&#xFF0C;&#x9879;&#x76EE;&#x5360;&#x636E;&#x7684;&#x4E3B;&#x8F74;&#x7A7A;&#x95F4;&#xFF08;main size&#xFF09;&#x3002;&#x6D4F;&#x89C8;&#x5668;&#x6839;&#x636E;&#x8FD9;&#x4E2A;&#x5C5E;&#x6027;&#xFF0C;&#x8BA1;&#x7B97;&#x4E3B;&#x8F74;&#x662F;&#x5426;&#x6709;&#x591A;&#x4F59;&#x7A7A;&#x95F4;&#x3002;&#x5B83;&#x7684;&#x9ED8;&#x8BA4;&#x503C;&#x4E3A;auto&#xFF0C;&#x5373;&#x9879;&#x76EE;&#x7684;&#x672C;&#x6765;&#x5927;&#x5C0F;&#x3002;<br>&#x5B83;&#x53EF;&#x4EE5;&#x8BBE;&#x4E3A;&#x8DDF;width&#x6216;height&#x5C5E;&#x6027;&#x4E00;&#x6837;&#x7684;&#x503C;&#xFF08;&#x6BD4;&#x5982;350px&#xFF09;&#xFF0C;&#x5219;&#x9879;&#x76EE;&#x5C06;&#x5360;&#x636E;&#x56FA;&#x5B9A;&#x7A7A;&#x95F4;&#x3002;</p><div class="widget-codetool" style="display:none"><div class="widget-codetool--inner"><span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span> <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text=".item {
  flex-basis: &lt;length&gt; | auto; /* default auto */
}" title="" data-original-title="&#x590D;&#x5236;"></span> <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span></div></div><pre class="hljs css"><code><span class="hljs-selector-class">.item</span> {
  <span class="hljs-attribute">flex-basis</span>: &lt;length&gt; | auto; <span class="hljs-comment">/* default auto */</span>
}</code></pre><p>5.flex<br>flex&#x5C5E;&#x6027;&#x662F;flex-grow, flex-shrink &#x548C; flex-basis&#x7684;&#x7B80;&#x5199;&#xFF0C;&#x9ED8;&#x8BA4;&#x503C;&#x4E3A;0 1 auto&#x3002;&#x540E;&#x4E24;&#x4E2A;&#x5C5E;&#x6027;&#x53EF;&#x9009;&#x3002;<br>&#x8BE5;&#x5C5E;&#x6027;&#x6709;&#x4E24;&#x4E2A;&#x5FEB;&#x6377;&#x503C;&#xFF1A;auto (1 1 auto) &#x548C; none (0 0 auto)&#x3002;<br>&#x5EFA;&#x8BAE;&#x4F18;&#x5148;&#x4F7F;&#x7528;&#x8FD9;&#x4E2A;&#x5C5E;&#x6027;&#xFF0C;&#x800C;&#x4E0D;&#x662F;&#x5355;&#x72EC;&#x5199;&#x4E09;&#x4E2A;&#x5206;&#x79BB;&#x7684;&#x5C5E;&#x6027;&#xFF0C;&#x56E0;&#x4E3A;&#x6D4F;&#x89C8;&#x5668;&#x4F1A;&#x63A8;&#x7B97;&#x76F8;&#x5173;&#x503C;&#x3002;</p><div class="widget-codetool" style="display:none"><div class="widget-codetool--inner"><span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span> <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text=".item {
  flex: none | [ &lt;&apos;flex-grow&apos;&gt; &lt;&apos;flex-shrink&apos;&gt;? || &lt;&apos;flex-basis&apos;&gt; ]
}" title="" data-original-title="&#x590D;&#x5236;"></span> <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span></div></div><pre class="hljs css"><code><span class="hljs-selector-class">.item</span> {
  <span class="hljs-attribute">flex</span>: none | [ &lt;<span class="hljs-string">&apos;flex-grow&apos;</span>&gt; &lt;<span class="hljs-string">&apos;flex-shrink&apos;</span>&gt;? || &lt;<span class="hljs-string">&apos;flex-basis&apos;</span>&gt; ]
}</code></pre><p>6.align-self<br>align-self&#x5C5E;&#x6027;&#x5141;&#x8BB8;&#x5355;&#x4E2A;&#x9879;&#x76EE;&#x6709;&#x4E0E;&#x5176;&#x4ED6;&#x9879;&#x76EE;&#x4E0D;&#x4E00;&#x6837;&#x7684;&#x5BF9;&#x9F50;&#x65B9;&#x5F0F;&#xFF0C;&#x53EF;&#x8986;&#x76D6;align-items&#x5C5E;&#x6027;&#x3002;&#x9ED8;&#x8BA4;&#x503C;&#x4E3A;auto&#xFF0C;&#x8868;&#x793A;&#x7EE7;&#x627F;&#x7236;&#x5143;&#x7D20;&#x7684;align-items&#x5C5E;&#x6027;&#xFF0C;&#x5982;&#x679C;&#x6CA1;&#x6709;&#x7236;&#x5143;&#x7D20;&#xFF0C;&#x5219;&#x7B49;&#x540C;&#x4E8E;stretch&#x3002;<br>&#x8BE5;&#x5C5E;&#x6027;&#x53EF;&#x80FD;&#x53D6;6&#x4E2A;&#x503C;&#xFF0C;&#x9664;&#x4E86;auto&#xFF0C;&#x5176;&#x4ED6;&#x90FD;&#x4E0E;align-items&#x5C5E;&#x6027;&#x5B8C;&#x5168;&#x4E00;&#x81F4;&#x3002;</p><div class="widget-codetool" style="display:none"><div class="widget-codetool--inner"><span class="selectCode code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x5168;&#x9009;"></span> <span type="button" class="copyCode code-tool" data-toggle="tooltip" data-placement="top" data-clipboard-text=".item {
  align-self: auto | flex-start | flex-end | center | baseline | stretch;
}
" title="" data-original-title="&#x590D;&#x5236;"></span> <span type="button" class="saveToNote code-tool" data-toggle="tooltip" data-placement="top" title="" data-original-title="&#x653E;&#x8FDB;&#x7B14;&#x8BB0;"></span></div></div><pre class="hljs coq"><code>.item {
  align-self: <span class="hljs-built_in">auto</span> | <span class="hljs-type">flex</span>-start | <span class="hljs-type">flex</span>-<span class="hljs-keyword">end</span> | <span class="hljs-type">center</span> | <span class="hljs-type">baseline</span> | <span class="hljs-type">stretch</span>;
}
</code></pre><p><span class="img-wrap"><img data-src="/img/bVTiTV?w=743&amp;h=390" src="https://static.alili.tech/img/bVTiTV?w=743&amp;h=390" alt="clipboard.png" title="clipboard.png" style="cursor:pointer"></span></p><p>&#x5907;&#x6CE8;&#xFF1A;&#x8282;&#x9009;&#x81EA;Flex &#x5E03;&#x5C40;&#x6559;&#x7A0B;&#xFF1A;&#x8BED;&#x6CD5;&#x7BC7; &#x962E;&#x4E00;&#x5CF0;</p>
{{< /raw >}}

# 版权声明
本文资源来源互联网，仅供学习研究使用，版权归该资源的合法拥有者所有，

本文仅用于学习、研究和交流目的。转载请注明出处、完整链接以及原作者。

原作者若认为本站侵犯了您的版权，请联系我们，我们会立即删除！

## 原文标题
Flex 布局教程

## 原文链接
[https://segmentfault.com/a/1190000015796799](https://segmentfault.com/a/1190000015796799)

