---
title: 拒绝烂大街——Flexbox布局演示站了解一下
hidden: true
categories: [reprint]
slug: b4bcc67f
date: 2018-10-30 02:30:12
---

{{< raw >}}
<h1 id="articleHeader0">&#x524D;&#x8A00;</h1><p>&#x6700;&#x8FD1;&#x5B66;&#x5230;Flexbox&#x5E03;&#x5C40;&#xFF0C;&#x5F53;&#x65F6;&#x5C31;&#x611F;&#x89C9;&#x771F;&#x662F;&#x4E00;&#x4E2A;&#x5E03;&#x5C40;&#x7684;&#x795E;&#x5668;&#x3002;&#x7EC8;&#x4E8E;&#x6446;&#x8131;&#x4E86;&#x5229;&#x7528;&#x5404;&#x79CD;&#x5B9A;&#x4F4D;&#x6D6E;&#x52A8;&#x5E03;&#x5C40;&#x7684;&#x65E5;&#x5B50;&#x3002;&#x60F3;&#x5199;&#x6587;&#x7AE0;&#x603B;&#x7ED3;&#x4E00;&#x4E0B;&#x5427;&#xFF0C;&#x53D1;&#x73B0;&#x4ECB;&#x7ECD;Flexbox&#x5E03;&#x5C40;&#x7C7B;&#x7684;&#x6587;&#x7AE0;&#x90FD;&#x88AB;&#x5199;&#x70C2;&#x4E86;&#xFF0C;&#x5404;&#x79CD;&#x5927;&#x795E;&#x5199;&#x7684;&#x4E5F;&#x662F;&#x751F;&#x52A8;&#x5F62;&#x8C61;&#xFF0C;&#x5355;&#x5355;&#x5199;&#x4E00;&#x4E2A;&#x5E03;&#x5C40;&#x7528;&#x6CD5;&#x611F;&#x89C9;&#x9664;&#x4E86;&#x81EA;&#x5DF1;&#x8BB0;&#x5F55;&#x65B9;&#x4FBF;&#x672C;&#x5730;&#x67E5;&#x5E76;&#x6CA1;&#x6709;&#x4EC0;&#x4E48;&#x610F;&#x4E49;&#xFF0C;&#x4E8E;&#x662F;&#x5C31;&#x60F3;&#x5230;&#x4E86;&#x4E4B;&#x524D;&#x5728;&#x4E00;&#x4E2A;&#x89C6;&#x9891;&#x4E2D;&#x770B;&#x5230;&#x4E86;&#x8FD9;&#x6837;&#x7684;&#x7F51;&#x7AD9;&#xFF0C;&#x4F46;&#x662F;&#x90A3;&#x4E2A;&#x7F51;&#x5740;&#x6211;&#x5F53;&#x65F6;&#x6253;&#x4E0D;&#x5F00;&#x5C31;&#x4EA7;&#x751F;&#x4E86;&#x81EA;&#x5DF1;&#x4E5F;&#x5199;&#x4E00;&#x4E2A;&#x7684;&#x60F3;&#x6CD5;&#x3002;&#x65E2;&#x80FD;&#x81EA;&#x5DF1;&#x5DE9;&#x56FA;&#x8FD8;&#x80FD;&#x7ED9;&#x521D;&#x5B66;&#x8005;&#x4F7F;&#x7528;&#x3002;</p><h1 id="articleHeader1">Flexbox&#x6F14;&#x793A;&#x7AD9;</h1><p>&#x5927;&#x6982;&#x5C31;&#x662F;&#x5F20;&#x8FD9;&#x4E2A;&#x6837;&#x5B50;&#xFF1A;<br><span class="img-wrap"><img data-src="/img/remote/1460000014296132?w=1907&amp;h=700" src="https://static.alili.tech/img/remote/1460000014296132?w=1907&amp;h=700" alt="Flexbox" title="Flexbox" style="cursor:pointer;display:inline"></span></p><ol><li>&#x70B9;&#x51FB;&#x8BBE;&#x7F6E;Flex&#x5BB9;&#x5668;&#x548C;Flex&#x9879;&#x76EE;&#x7684;&#x5404;&#x4E2A;&#x5C5E;&#x6027;&#x7684;&#x503C;&#x4EE5;&#x53CA;&#x9879;&#x76EE;&#x7684;&#x5BBD;&#x5EA6;&#xFF0C;&#x53F3;&#x8FB9;&#x5B9E;&#x65F6;&#x770B;&#x5230;&#x6548;&#x679C;&#x521D;&#x5B66;&#x65F6;&#x66F4;&#x5BB9;&#x6613;&#x7406;&#x89E3;&#x5404;&#x4E2A;&#x5C5E;&#x6027;&#x7684;&#x4F5C;&#x7528;&#x3002;</li><li>&#x53CB;&#x597D;&#x7684;&#x63D0;&#x793A;&#xFF1A;&#x521D;&#x5B66;&#x8005;&#x4E0D;&#x6613;&#x8BB0;&#x5168;&#x6240;&#x6709;&#x7684;&#x5C5E;&#x6027;&#x548C;&#x503C;&#x7684;&#x5DE6;&#x53F3;&#xFF0C;&#x9F20;&#x6807;&#x653E;&#x5728;&#x5C5E;&#x6027;&#x540D;&#x4E0A;&#x5373;&#x53EF;&#x663E;&#x793A;&#x76F8;&#x5E94;&#x5C5E;&#x6027;&#x7684;&#x4F5C;&#x7528;&#x3002;</li></ol><p><a href="https://xluos.github.io/demo/flexbox/" rel="nofollow noreferrer" target="_blank">&#x67E5;&#x770B;Flexbox&#x6F14;&#x793A;&#x7AD9;</a></p><p>&#x53EA;&#x662F;&#x7B80;&#x5355;&#x4E86;&#x5199;&#x4E86;&#x51E0;&#x4E2A;&#x54CD;&#x5E94;&#x5F0F;CSS&#xFF0C;&#x79FB;&#x52A8;&#x7AEF;&#x770B;&#x7684;&#x6548;&#x679C;&#x53EF;&#x80FD;&#x4E0D;&#x662F;&#x592A;&#x597D;&#xFF0C;&#x5EFA;&#x8BAE;PC&#x7AEF;&#x98DF;&#x7528;</p><p><a href="https://github.com/xluos/demo/tree/gh-pages/flexbox" rel="nofollow noreferrer" target="_blank">GitHub&#x5730;&#x5740;</a></p><h1 id="articleHeader2">&#x6700;&#x540E;</h1><p>&#x653E;&#x4E0A;&#x51E0;&#x4E2A;&#x6211;&#x5B66;Flexbox&#x5E03;&#x5C40;&#x65F6;&#x770B;&#x7684;&#x535A;&#x5BA2;&#xFF1A;<br><a href="http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html" rel="nofollow noreferrer" target="_blank">&#x962E;&#x4E00;&#x5CF0;&#x2014;&#x2014;Flex &#x5E03;&#x5C40;&#x6559;&#x7A0B;&#xFF1A;&#x8BED;&#x6CD5;&#x7BC7;</a><br><a href="http://www.ruanyifeng.com/blog/2015/07/flex-examples.html" rel="nofollow noreferrer" target="_blank">&#x962E;&#x4E00;&#x5CF0;&#x2014;&#x2014;Flex &#x5E03;&#x5C40;&#x6559;&#x7A0B;&#xFF1A;&#x5B9E;&#x4F8B;&#x7BC7;</a><br><a href="https://segmentfault.com/a/1190000008414812">&#x901A;&#x8FC7;&#x52A8;&#x56FE;&#x5F62;&#x8C61;&#x5730;&#x4E3A;&#x4F60;&#x4ECB;&#x7ECD; flexbox &#x662F;&#x5982;&#x4F55;&#x5DE5;&#x4F5C;&#x7684;&#xFF08;&#x4E00;&#xFF09;</a></p><p>&#x6700;&#x540E;&#x7684;&#x6700;&#x540E;&#xFF0C;&#x539A;&#x989C;&#x65E0;&#x803B;&#x6C42;Star&#xFF08;&#x9003;&#xFF09;<br>&#x5982;&#x679C;&#x6070;&#x597D;&#x4F60;&#x6B63;&#x5728;&#x5B66;Flexbox&#xFF0C;&#x8FD9;&#x4E2A;&#x5C0F;&#x7F51;&#x7AD9;&#x5BF9;&#x4F60;&#x6709;&#x90A3;&#x4E48;&#x4E00;&#x70B9;&#x513F;&#x5E2E;&#x52A9;&#x7ED9;&#x6211;&#x70B9;&#x4E00;&#x4E2A;Star&#x5427;</p>
{{< /raw >}}

# 版权声明
本文资源来源互联网，仅供学习研究使用，版权归该资源的合法拥有者所有，

本文仅用于学习、研究和交流目的。转载请注明出处、完整链接以及原作者。 

原作者若认为本站侵犯了您的版权，请联系我们，我们会立即删除！

## 原文标题
拒绝烂大街——Flexbox布局演示站了解一下

## 原文链接
[https://segmentfault.com/a/1190000014296127](https://segmentfault.com/a/1190000014296127)

