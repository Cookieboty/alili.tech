---
title: React key值的作用和使用
hidden: true
categories: [reprint]
slug: af80725b
date: 2018-11-15 02:30:08
---

{{< raw >}}
<p>&#x5728;react&#x9879;&#x76EE;&#x4E2D;&#x603B;&#x4F1A;&#x9047;&#x5230;&#x8FD9;&#x6837;&#x4E00;&#x4E2A;&#x7684;&#x5751;<br><span class="img-wrap"><img data-src="/img/bVbfKuj?w=386&amp;h=137" src="https://static.alili.tech/img/bVbfKuj?w=386&amp;h=137" alt="clipboard.png" title="clipboard.png"></span></p><p>&#x8FD9;&#x662F;&#x8B66;&#x544A;&#x6570;&#x7EC4;&#x904D;&#x5386;&#x5B50;&#x5143;&#x7D20;&#x8981;&#x6709;&#x4E00;&#x4E2A;&#x552F;&#x4E00;&#x7684;key&#x503C;&#xFF0C;&#x4F46;&#x662F;key&#x5230;&#x5E95;&#x662F;&#x4EC0;&#x4E48;&#xFF0C;&#x5728;&#x4EE3;&#x7801;&#x4E2D;&#x5230;&#x5E95;&#x8D77;&#x4E86;&#x4EC0;&#x4E48;&#x4F5C;&#x7528;&#xFF1F;</p><h2>key&#x6982;&#x8FF0;</h2><p>react&#x4E2D;&#x7684;key&#x5C5E;&#x6027;&#xFF0C;&#x5B83;&#x662F;&#x4E00;&#x4E2A;&#x7279;&#x6B8A;&#x7684;&#x5C5E;&#x6027;&#xFF0C;&#x5B83;&#x7684;&#x51FA;&#x73B0;&#x4E0D;&#x662F;&#x7ED9;&#x5F00;&#x53D1;&#x8005;&#x7528;&#x7684;&#xFF08;&#x4F8B;&#x5982;&#x4F60;&#x4E3A;&#x4E00;&#x4E2A;&#x7EC4;&#x4EF6;&#x8BBE;&#x7F6E;key&#x4E4B;&#x540E;&#xFF0C;&#x4E5F;&#x4ECD;&#x65E0;&#x6CD5;&#x83B7;&#x53D6;&#x8FD9;&#x4E2A;&#x7EC4;&#x4EF6;&#x7684;key&#x503C;&#xFF09;&#xFF0C;&#x800C;&#x662F;&#x7ED9;react&#x81EA;&#x5DF1;&#x7528;&#x7684;&#x3002;<br>&#x7B80;&#x5355;&#x6765;&#x8BF4;&#xFF0C;react&#x5229;&#x7528;key&#x6765;&#x8BC6;&#x522B;&#x7EC4;&#x4EF6;&#xFF0C;&#x5B83;&#x662F;&#x4E00;&#x79CD;&#x8EAB;&#x4EFD;&#x6807;&#x8BC6;&#x6807;&#x8BC6;&#xFF0C;&#x5C31;&#x50CF;&#x6211;&#x4EEC;&#x7684;&#x8EAB;&#x4EFD;&#x8BC1;&#x7528;&#x6765;&#x8FA8;&#x8BC6;&#x4E00;&#x4E2A;&#x4EBA;&#x4E00;&#x6837;&#x3002;&#x6BCF;&#x4E2A;key&#x5BF9;&#x5E94;&#x4E00;&#x4E2A;&#x7EC4;&#x4EF6;&#xFF0C;&#x76F8;&#x540C;&#x7684;key react&#x8BA4;&#x4E3A;&#x662F;&#x540C;&#x4E00;&#x4E2A;&#x7EC4;&#x4EF6;&#xFF0C;&#x8FD9;&#x6837;&#x540E;&#x7EED;&#x76F8;&#x540C;&#x7684;key&#x5BF9;&#x5E94;&#x7EC4;&#x4EF6;&#x90FD;&#x4E0D;&#x4F1A;&#x88AB;&#x521B;&#x5EFA;&#x3002;</p><h2>key&#x7684;&#x4F7F;&#x7528;&#x573A;&#x666F;</h2><p>&#x5728;&#x9879;&#x76EE;&#x5F00;&#x53D1;&#x4E2D;&#xFF0C;key&#x5C5E;&#x6027;&#x7684;&#x4F7F;&#x7528;&#x573A;&#x666F;&#x6700;&#x591A;&#x7684;&#x8FD8;&#x662F;&#x7531;&#x6570;&#x7EC4;&#x52A8;&#x6001;&#x521B;&#x5EFA;&#x7684;&#x5B50;&#x7EC4;&#x4EF6;&#x7684;&#x60C5;&#x51B5;&#xFF0C;&#x9700;&#x8981;&#x4E3A;&#x6BCF;&#x4E2A;&#x5B50;&#x7EC4;&#x4EF6;&#x6DFB;&#x52A0;&#x552F;&#x4E00;&#x7684;key&#x5C5E;&#x6027;&#x503C;&#x3002;&#x90A3;&#x4F1A;&#x6709;&#x7684;&#x4EBA;&#x5C31;&#x4F1A;&#x81EA;&#x7136;&#x800C;&#x7136;&#x60F3;&#x5230;&#xFF0C;key&#x548C;&#x52A8;&#x6001;&#x6E32;&#x67D3;&#x7684;&#x5B50;&#x5143;&#x7D20;&#x83B7;&#x53D6;&#x7684;index&#x4F4D;&#x7F6E;&#x7684;&#x503C;&#x5F88;&#x63A5;&#x8FD1;&#xFF0C;&#x90A3;&#x4E0D;&#x662F;&#x53EF;&#x4EE5;&#x76F4;&#x63A5;&#x7528;index&#x9644;&#x4E0A;key&#x7684;&#x503C;&#x5462;key={index}?</p><pre><code>&#x4F8B;&#x5982;&#xFF1A;
{dataList.map((item,index)=&gt;{
        return &lt;div style={mystyle} key={index}&gt;{item.name}&lt;/div&gt;
        })
}</code></pre><p>&#x5728;&#x4F60;&#x5C1D;&#x8BD5;&#x8FC7;&#x540E;&#x4F1A;&#x53D1;&#x73B0;&#xFF0C;&#x62A5;&#x9519;&#x6CA1;&#x4E86;&#xFF0C;&#x6E32;&#x67D3;&#x4E5F;&#x6CA1;&#x95EE;&#x9898;&#x4E0D;&#x662F;&#x5F88;&#x6B63;&#x5E38;&#x561B;&#xFF1F;&#xFF01;&#x4F46;&#x662F;&#x5F3A;&#x70C8;&#x4E0D;&#x63A8;&#x8350;&#x7528;&#x6570;&#x7EC4;index&#x6765;&#x4F5C;&#x4E3A;key&#x3002;<br>&#x5982;&#x679C;&#x6570;&#x636E;&#x66F4;&#x65B0;&#x4EC5;&#x4EC5;&#x662F;&#x6570;&#x7EC4;&#x91CD;&#x65B0;&#x6392;&#x5E8F;&#x6216;&#x5728;&#x5176;&#x4E2D;&#x95F4;&#x4F4D;&#x7F6E;&#x63D2;&#x5165;&#x65B0;&#x5143;&#x7D20;&#xFF0C;&#x90A3;&#x4E48;&#x89C6;&#x56FE;&#x5143;&#x7D20;&#x90FD;&#x5C06;&#x91CD;&#x65B0;&#x6E32;&#x67D3;&#x3002;</p><p>&#x4F8B;&#x5982;&#xFF1A;<br>&#x672C;&#x6765;index=2&#x7684;&#x5143;&#x7D20;&#x5411;&#x524D;&#x79FB;&#x52A8;&#x540E;&#xFF0C;&#x90A3;&#x8BE5;&#x5143;&#x7D20;&#x7684;key&#x4E0D;&#x4E5F;&#x540C;&#x6837;&#x53D1;&#x751F;&#x4E86;&#x6539;&#x53D8;&#x90A3;&#x8FD9;&#x6837;&#x4F1A;&#x6539;&#x53D8;&#x7684;Key&#x5C31;&#x6CA1;&#x6709;&#x4EFB;&#x4F55;&#x7684;&#x5B58;&#x5728;&#x610F;&#x4E49;&#xFF0C;&#x65E2;&#x7136;&#x662F;&#x4F5C;&#x4E3A;&#x201C;&#x8EAB;&#x4EFD;&#x8BC1;&#x201D;&#x4E00;&#x6837;&#x7684;&#x5B58;&#x5728;&#xFF0C;&#x90A3;&#x5C31;&#x4E0D;&#x5BB9;&#x6709;&#x5931;&#x3002;&#x5F53;&#x7136;&#xFF0C;&#x5728;&#x4F60;&#x7528;key&#x503C;&#x521B;&#x5EFA;&#x5B50;&#x7EC4;&#x4EF6;&#x7684;&#x65F6;&#x5019;&#xFF0C;&#x82E5;&#x6570;&#x7EC4;&#x7684;&#x5185;&#x5BB9;&#x53EA;&#x662F;&#x4F5C;&#x4E3A;&#x7EAF;&#x5C55;&#x793A;&#xFF0C;&#x800C;&#x4E0D;&#x6D89;&#x53CA;&#x5230;&#x6570;&#x7EC4;&#x7684;&#x52A8;&#x6001;&#x53D8;&#x66F4;&#xFF0C;&#x5176;&#x5B9E;&#x662F;&#x53EF;&#x4EE5;&#x4F7F;&#x7528;index&#x4F5C;&#x4E3A;key&#x7684;&#x3002;</p><h2>key&#x7684;&#x503C;&#x5FC5;&#x987B;&#x4FDD;&#x8BC1;&#x552F;&#x4E00;&#x4E14;&#x7A33;&#x5B9A;</h2><p>&#x6211;&#x5728;&#x4E0E;Key&#x503C;&#x6253;&#x8FC7;&#x51E0;&#x6B21;&#x4EA4;&#x9053;&#x8FC7;&#x540E;&#xFF0C;&#x89C9;&#x5F97;key&#x503C;&#x5C31;&#x7C7B;&#x4F3C;&#x4E8E;&#x6570;&#x636E;&#x5E93;&#x4E2D;&#x7684;&#x4E3B;&#x952E;id&#x4E00;&#x6837;&#xFF0C;&#x6709;&#x4E14;&#x552F;&#x4E00;&#x3002;</p><pre><code>//this.state.users&#x5185;&#x5BB9;&#x3002;&#x6CE8;&#x610F;&#xFF1A;&#x674E;&#x56DB;&#x548C;&#x738B;&#x4E94;&#x7684;id&#x76F8;&#x540C;&#xFF01;&#xFF01;&#xFF01;
this.state = {
 users: [{id:1,name: &apos;&#x5F20;&#x4E09;&apos;}, {id:2, name: &apos;&#x674E;&#x56DB;&apos;}, {id: 2, name: &quot;&#x738B;&#x4E94;&quot;}],
 ....//&#x7701;&#x7565;
}
render()
 return(
  &lt;div&gt;
    &lt;h3&gt;&#x7528;&#x6237;&#x5217;&#x8868;&lt;/h3&gt;
    {this.state.users.map(u =&gt; &lt;div key={u.id}&gt;{u.id}:{u.name}&lt;/div&gt;)}
  &lt;/div&gt;
 )
);</code></pre><p>&#x6CE8;&#x610F;&#x4EE5;&#x4E0A;&#x8303;&#x4F8B;&#x4E2D;&#xFF0C;&#x52A8;&#x6001;&#x6E32;&#x67D3;&#x7684;&#x6570;&#x636E;&#x4E2D;&#xFF0C;key&#x4EE5;&#x6570;&#x636E;&#x7684;id&#x6765;&#x5B9A;&#xFF0C;&#x800C;&#x674E;&#x56DB;&#x3001;&#x738B;&#x4E94;&#x7684;id&#x76F8;&#x540C;&#x800C;&#x5BFC;&#x81F4;Key&#x7684;&#x96F7;&#x540C;&#xFF0C;&#x6700;&#x540E;&#x7684;&#x6E32;&#x67D3;&#x7ED3;&#x679C;&#x4E3A;&#x5F20;&#x4E09;&#x548C;&#x674E;&#x56DB;&#xFF0C;&#x738B;&#x4E94;&#x5E76;&#x6CA1;&#x6709;&#x5C55;&#x793A;&#x51FA;&#x6765;&#x3002;&#x4E3B;&#x8981;&#x662F;&#x56E0;&#x4E3A; react&#x6839;&#x636E;key&#x8BA4;&#x4E3A;&#x674E;&#x56DB;&#x548C;&#x738B;&#x4E94;&#x662F;&#x540C;&#x4E00;&#x4E2A;&#x7EC4;&#x4EF6;&#xFF08;&#x674E;&#x56DB;&#x548C;&#x738B;&#x4E94;&#x7684;key&#x503C;&#x76F8;&#x540C;&#xFF09;&#xFF0C;&#x5BFC;&#x81F4;&#x7B2C;&#x4E00;&#x4E2A;&#x88AB;&#x6E32;&#x67D3;&#xFF0C;&#x540E;&#x7EED;&#x7684;&#x4F1A;&#x88AB;&#x4E22;&#x5F03;&#x6389;&#x3002;</p><p>&#x8FD9;&#x6837;&#xFF0C;&#x6709;&#x4E86;key&#x5C5E;&#x6027;&#x540E;&#xFF0C;&#x5C31;&#x53EF;&#x4EE5;&#x4E0E;&#x7EC4;&#x4EF6;&#x5EFA;&#x7ACB;&#x4E86;&#x4E00;&#x79CD;&#x5BF9;&#x5E94;&#x5173;&#x7CFB;&#xFF0C;react&#x6839;&#x636E;key&#x6765;&#x51B3;&#x5B9A;&#x662F;&#x9500;&#x6BC1;&#x91CD;&#x65B0;&#x521B;&#x5EFA;&#x7EC4;&#x4EF6;&#x8FD8;&#x662F;&#x66F4;&#x65B0;&#x7EC4;&#x4EF6;&#x3002;</p><hr><p>&#x5E76;&#x4E14;&#xFF0C;Key&#x4E5F;&#x8981;&#x4FDD;&#x8BC1;&#x503C;&#x7684;&#x7A33;&#x5B9A;&#x6027;&#xFF0C;&#x4F8B;&#x5982;&#xFF1A;</p><pre><code>{dataList.map((item,index)=&gt;{
        return &lt;div style={mystyle} key={Math.random()}&gt;{item.name}&lt;/div&gt;
        })
}</code></pre><p>&#x5C24;&#x5176;&#x5982;&#x4EE5;&#x4E0A;&#x8303;&#x4F8B;&#x4E2D;&#x6240;&#x793A;&#xFF0C;key&#x7684;&#x503C;&#x4EE5;<strong>Math.random()</strong>&#x968F;&#x673A;&#x751F;&#x6210;&#x800C;&#x5B9A;&#xFF0C;&#x8FD9;&#x4F7F;&#x5F97;&#x6570;&#x7EC4;&#x5143;&#x7D20;&#x4E2D;&#x7684;&#x6BCF;&#x9879;&#x90FD;&#x91CD;&#x65B0;&#x9500;&#x6BC1;&#x7136;&#x540E;&#x91CD;&#x65B0;&#x521B;&#x5EFA;&#xFF0C;&#x6709;&#x4E00;&#x5B9A;&#x7684;&#x6027;&#x80FD;&#x5F00;&#x9500;&#xFF1B;&#x53E6;&#x5916;&#x53EF;&#x80FD;&#x5BFC;&#x81F4;&#x4E00;&#x4E9B;&#x610F;&#x60F3;&#x4E0D;&#x5230;&#x7684;&#x95EE;&#x9898;&#x51FA;&#x73B0;&#x3002;</p><blockquote><strong>&#x6240;&#x4EE5;&#xFF0C;Key&#x7684;&#x503C;&#x5FC5;&#x987B;&#x4FDD;&#x8BC1;&#x5176;&#x552F;&#x4E00;&#x548C;&#x7A33;&#x5B9A;&#x6027;</strong></blockquote>
{{< /raw >}}

# 版权声明
本文资源来源互联网，仅供学习研究使用，版权归该资源的合法拥有者所有，

本文仅用于学习、研究和交流目的。转载请注明出处、完整链接以及原作者。 

原作者若认为本站侵犯了您的版权，请联系我们，我们会立即删除！

## 原文标题
React key值的作用和使用

## 原文链接
[https://segmentfault.com/a/1190000016123227](https://segmentfault.com/a/1190000016123227)

